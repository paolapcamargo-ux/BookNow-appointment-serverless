import json

def lambda_handler(event, context):
    
    path = event.get("rawPath", "")
    method = event.get("requestContext", {}).get("http", {}).get("method", "")

    # ROOT PATH: /prod
    if path == "/prod" or path == "/":
        return {
            "statusCode": 200,
            "headers": {
                "Content-Type": "application/json"
            },
            "body": json.dumps({
                "message": "Welcome to BookNow API 🚀",
                "status": "running"
            })
        }

    # Example test route
    if path.endswith("/test"):
        return {
            "statusCode": 200,
            "body": json.dumps({"message": "Test successful"})
        }

    return {
        "statusCode": 404,
        "body": json.dumps({"error": "Route not found"})
    }
    import json
import boto3
import uuid
from datetime import datetime

dynamodb = boto3.resource('dynamodb', region_name='us-east-1')
table = dynamodb.Table('BookNow_appoint')

def lambda_handler(event, context):
    try:
        appointment_id = str(uuid.uuid4())

        item = {
            "appointmentID": appointment_id,
            "patientName": event.get("patientName"),
            "patientEmail": event.get("patientEmail"),
            "doctorName": event.get("doctorName"),
            "appointmentDate": event.get("appointmentDate"),
            "appointmentTime": event.get("appointmentTime"),
            "reason": event.get("reason"),
            "createdAt": datetime.utcnow().isoformat()
        }

        table.put_item(Item=item)

        return {
            "statusCode": 200,
            "body": json.dumps({
                "message": "Doctor appointment created",
                "appointmentID": appointment_id
            })
        }

    except Exception as e:
        print("ERROR:", str(e))
        return {
            "statusCode": 500,
            "body": json.dumps(str(e))
        }
