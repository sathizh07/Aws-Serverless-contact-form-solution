import json
import boto3
import uuid
import re
import os
from datetime import datetime

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table(os.environ['DYNAMODB_TABLE'])

def validate_email(email):
    return re.match(r"[^@]+@[^@]+\.[^@]+", email)

def lambda_handler(event, context):
    try:
        body = json.loads(event['body'])
        name = body.get('name')
        email = body.get('email')
        message = body.get('message')

        # Validate required fields
        if not name or not email or not message:
            return {
                "statusCode": 400,
                "body": json.dumps({"error": "All fields are required."})
            }
        
        # Validate email format
        if not validate_email(email):
            return {
                "statusCode": 400,
                "body": json.dumps({"error": "Invalid email address."})
            }

        submission_id = str(uuid.uuid4())
        timestamp = datetime.utcnow().isoformat()

        # Store in DynamoDB
        table.put_item(
            Item={
                'submissionId': submission_id,
                'name': name,
                'email': email,
                'message': message,
                'submittedAt': timestamp
            }
        )

        return {
            "statusCode": 200,
            "headers": {"Access-Control-Allow-Origin": "*"},
            "body": json.dumps({"message": "Submission successful."})
        }

    except Exception as e:
        return {
            "statusCode": 500,
            "body": json.dumps({"error": str(e)})
        }
