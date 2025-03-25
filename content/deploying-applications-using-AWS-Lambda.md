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
- Enter a **Function name** (e.g., `helloWorldFunction`).
- Choose **Python 3.x** for the runtime.
- For **Role**, select **Create a new role with basic Lambda permissions**. This allows the Lambda function to be triggered by basic events, like direct invocations or CloudWatch logs.

**Step 3: Create the Function**
- Click **Create function** to proceed. This will create your Lambda function.

---

### **3. Write the Lambda Function Code**

**Step 1: Edit the Lambda Function Code**
- After the function is created, scroll down to the **Function code** section.
- You’ll see an editor with some default code. Replace the code with the following simple "Hello World" function:

```python
import json

def lambda_handler(event, context):
    # Simple Hello World Response
    return {
        'statusCode': 200,
        'body': json.dumps('Hello, World!')
    }
```

**Explanation:**
- `lambda_handler` is the main function AWS Lambda uses to execute your code.
- The function simply returns a JSON response with a **Hello, World!** message.

**Step 2: Save the Code**
- After entering the code, click the **Deploy** button to save and deploy the function.

---

### **4. Test the Lambda Function**

**Step 1: Create a Test Event**
- Scroll to the **Test** section at the top of the Lambda function page.
- Click **Test** to create a new test event.
- Choose **Hello World** as the event template (it provides a simple structure).
- You can leave the default event data as it is (or modify it if you want).

**Step 2: Invoke the Function**
- Click **Test** to invoke the Lambda function.
- The function will execute, and you’ll see the result in the **Execution results** section.
- You should see the response:
  ```json
  {
      "statusCode": 200,
      "body": "\"Hello, World!\""
  }
  ```

---

### **5. Monitoring the Lambda Function**

**Step 1: View Logs in CloudWatch**
- AWS Lambda automatically integrates with CloudWatch for logging.
- In the **Monitoring** section of the Lambda function page, click **View logs in CloudWatch**.
- This will take you to the CloudWatch Logs section, where you can see the execution logs for your Lambda function.

**Step 2: Check CloudWatch Metrics**
- You can also monitor Lambda performance and invocations through CloudWatch metrics. These metrics can help you track things like the number of invocations and duration of function execution.

---

