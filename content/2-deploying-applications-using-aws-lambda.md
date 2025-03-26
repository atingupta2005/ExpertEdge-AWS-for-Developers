**Deploying Applications with AWS Lambda: Hands-on Guide**

---

### **1. Sign in to the AWS Management Console**

- Go to the [AWS Management Console](https://aws.amazon.com/console/).
- Log in with your AWS account credentials.

---

### **2. Create a Lambda Function**

**Step 1: Navigate to AWS Lambda**
- In the AWS Management Console, search for **Lambda** and select **AWS Lambda** from the results.
  
**Step 2: Create a New Lambda Function**
- Click **Create function**.
- Choose **Author from scratch**.
- Enter a **Function name** (e.g., `webinar-api`).
- Choose **Python 3.x** for the runtime.

**Step 3: Create the Function**
- Click **Create function** to proceed. This will create your Lambda function.

---

### **3. Write the Lambda Function Code**

**Step 1: Edit the Lambda Function Code**
- After the function is created, scroll down to the **Function code** section.
- You’ll see an editor with some default code. Replace the code with the following simple "webinar-api" function:

```python
import json

def lambda_handler(event, context):
    # Extract API endpoint from the event
    path = event.get('path', '')

    if path == '/register':
        return {
            'statusCode': 200,
            'body': json.dumps({
                'message': 'Click below to register for the webinar',
                'registration_link': 'https://zoom.us/webinar/register/7317411552853/WN_zVywNSChQJeXfxYmpb8QUg'
            })
        }

    elif path == '/youtube':
        return {
            'statusCode': 200,
            'body': json.dumps({
                'message': 'Watch the webinar live on YouTube',
                'youtube_link': 'https://www.youtube.com/watch?v=N50HDBRjrAE'
            })
        }

    elif path == '/linkedin':
        return {
            'statusCode': 200,
            'body': json.dumps({
                'message': 'Join the webinar event on LinkedIn',
                'linkedin_link': 'https://www.linkedin.com/events/7309835931727892480/comments/'
            })
        }

    elif path == '/webinar-details':
        return {
            'statusCode': 200,
            'body': json.dumps({
                'title': 'Getting Started with AWS for Developers: Deploying Applications with EC2, Lambda, and RDS',
                'date': 'March 26th',
                'time': '11:30 AM – 01:00 PM',
                'description': 'This webinar will walk you through the steps of deploying applications on AWS using EC2, Lambda, and RDS.'
            })
        }

    else:
        return {
            'statusCode': 404,
            'body': json.dumps({
                'message': 'API endpoint not found.'
            })
        }
```

**Step 2: Save the Code**
- After entering the code, click the **Deploy** button to save and deploy the function.

---

### **Deploy API Gateway**

#### 1. **Create a New API in API Gateway**:
   - **Navigate to API Gateway** in the AWS Management Console.
   - Select **Create API** → **REST API** → **Build**.
   - **API Name**: `webinar-api`.
   - **Endpoint Type**: **Regional**.
   - Click **Create API**.

#### 2. **Create Resources and Methods**:
   - **Add Resource**:
     - Go to **Resources** → **Create Resource**.
     - **Resource Name**: `register` (or any other endpoint like `/youtube`).
     - Click **Create Resource**.
   
   - **Add Method** (e.g., GET for `/register`):
     - Select the resource (e.g., `/register`) → **Actions** → **Create Method** → **GET**.
     - **Integration Type**: **Lambda Function** → Choose your Lambda function.
     - Click **Save**.

#### 3. **Deploy the API**:
   - Go to **Actions** → **Deploy API**.
   - **Deployment Stage**: Select or create a stage (e.g., `prod`).
   - Click **Deploy**.
   - The **Invoke URL** will be provided (e.g., `https://xyz12345.execute-api.us-west-2.amazonaws.com/prod`).

#### 4. **Replicate for Other APIs**:
   - To add additional resources (e.g., `/youtube`), repeat **Step 2** for each new endpoint.
   - Each resource should have a method (e.g., GET) linked to the Lambda function.

#### 5. **Test the API**:
   - **Postman or Browser**: Test endpoints like:
     - `https://xyz12345.execute-api.us-west-2.amazonaws.com/prod/register`
     - `https://xyz12345.execute-api.us-west-2.amazonaws.com/prod/youtube`

---
