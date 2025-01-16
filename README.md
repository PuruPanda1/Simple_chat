# Steps to Run the Simple Chat Django Web Socket Project

## 1. Create a Virtual Environment
```bash
python3 -m venv env
```
## 2. Activate the Virtual Environment
```bash
source env/bin/activate
```
## 3. Navigate to project files
```bash
cd chat_app
```
## 4. Install Dependencies
```bash
pip install -r requirements.txt
```
## 5. Apply migrations
```bash
python manage.py migrate
```
## 6. Run the development server
```bash
python manage.py runserver
```

## Video Demo of the Simple Chat


https://github.com/user-attachments/assets/6dd75075-8cec-4798-8cfc-60415bcd8f81



# AWS Codes

## 1. Add two numbers and return the result
```
exports.handler = async (event) => {
    try {
        const { num1, num2 } = JSON.parse(event.body);

        if (typeof num1 !== 'number' || typeof num2 !== 'number') {
            return {
                statusCode: 400,
                body: JSON.stringify({ message: "Invalid input. num1 and num2 must be numbers." }),
            };
        }

        const result = num1 + num2;

        return {
            statusCode: 200,
            body: JSON.stringify({ result }),
        };
    } catch (error) {
        return {
            statusCode: 500,
            body: JSON.stringify({ message: "Internal Server Error", error: error.message }),
        };
    }
};
```

## 2. Store a Document file in an S3 Bucket
```
const AWS = require('aws-sdk');
const s3 = new AWS.S3();

exports.handler = async (event) => {
    try {
        const bucketName = "your-s3-bucket-name";
        const { fileName, fileContent } = JSON.parse(event.body);

        if (!fileName || !fileContent) {
            return {
                statusCode: 400,
                body: JSON.stringify({ message: "Missing fileName or fileContent in request." }),
            };
        }

        const buffer = Buffer.from(fileContent, 'base64');

        const params = {
            Bucket: bucketName,
            Key: fileName,
            Body: buffer,
            ContentType: "application/pdf", // Change this if the file type differs
        };

        await s3.upload(params).promise();

        return {
            statusCode: 200,
            body: JSON.stringify({ message: "File uploaded successfully." }),
        };
    } catch (error) {
        return {
            statusCode: 500,
            body: JSON.stringify({ message: "File upload failed.", error: error.message }),
        };
    }
};
```
