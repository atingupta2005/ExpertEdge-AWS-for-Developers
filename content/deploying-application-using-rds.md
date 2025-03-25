### **Creating a Simple API CRUD Application using AWS RDS and AWS Lambda**

#### **Overview:**
In this guide, we will walk you through the steps to create a simple CRUD (Create, Read, Update, Delete) API using Flask (Python) with AWS RDS (Relational Database Service) and AWS Lambda. The API will interact with an RDS database for storing and retrieving data, while AWS Lambda will handle the requests without using any additional AWS services unless required.

You will use Postman to test the API endpoints after deploying your Lambda functions.

#### **Prerequisites:**
1. **AWS Account**: Ensure you have access to an AWS account.
2. **AWS CLI**: Ensure you have AWS CLI installed and configured.
3. **Postman**: Install Postman for API testing.
4. **Flask**: Install Flask in your local environment for local testing before deploying it to Lambda.

---

### **Steps:**

#### **Step 1: Set Up AWS RDS Instance**
1. **Create an RDS instance:**
   - Go to the **AWS Management Console** and navigate to **RDS**.
   - Click **Create database**, select **MySQL** or **PostgreSQL** (depending on preference), and proceed with the default configurations.
   - Make sure the instance is publicly accessible if you want to connect from your local system.
   - Save the **endpoint** of the database instance, along with the **username** and **password** for later use.

2. **Set Up Database:**
   - Use MySQL Workbench or a similar database client to connect to the RDS instance using the provided credentials.
   - Create a new database and a table for the application. Here's an example for creating a `users` table:

   ```sql
   CREATE DATABASE flask_app;
   USE flask_app;

   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       email VARCHAR(100) NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

---

#### **Step 2: Set Up AWS Lambda**
1. **Create a Lambda Function:**
   - Navigate to **AWS Lambda** in the AWS console and create a new function.
   - Choose **Author from scratch** and select Python 3.x as the runtime.
   - Set the execution role with **AWS Lambda Basic Execution Role** for logging purposes.

2. **Lambda Function to Connect to RDS:**
   We'll write Lambda functions to handle CRUD operations. Each Lambda function will use the `pymysql` library (for MySQL) or `psycopg2` (for PostgreSQL) to interact with the RDS instance.

   Install the required libraries in your local environment:

   ```bash
   pip install pymysql requests
   ```

3. **Lambda Function Code for CRUD Operations:**

   Example Lambda function for **Creating a User**:

   ```python
   import json
   import pymysql

   # RDS settings
   RDS_HOST = 'your-rds-endpoint'
   USERNAME = 'your-username'
   PASSWORD = 'your-password'
   DATABASE = 'flask_app'

   # Database connection
   connection = pymysql.connect(host=RDS_HOST, user=USERNAME, password=PASSWORD, database=DATABASE)

   def lambda_handler(event, context):
       try:
           name = event['name']
           email = event['email']
           
           with connection.cursor() as cursor:
               cursor.execute("INSERT INTO users (name, email) VALUES (%s, %s)", (name, email))
               connection.commit()
               
           return {
               'statusCode': 200,
               'body': json.dumps(f"User {name} created successfully!")
           }
       except Exception as e:
           return {
               'statusCode': 400,
               'body': json.dumps(f"Error: {str(e)}")
           }
   ```

   Similarly, you can create Lambda functions for **Read**, **Update**, and **Delete** operations.

---

#### **Step 3: Deploy Lambda Function**
1. **Zip your Python code** (including dependencies like `pymysql`):
   - Create a directory for your Lambda function and the required libraries.
   - Install libraries locally:
     ```bash
     pip install pymysql -t ./lambda_package
     ```
   - Add your function code into the `lambda_package` directory and zip everything.

     ```bash
     zip -r function.zip .
     ```

2. **Upload ZIP file** to AWS Lambda.
   - In the **Lambda** console, select your function, and under **Function code**, upload the ZIP file.

3. **Test Lambda Function**:
   - Create a test event for your Lambda function with a sample payload:
     ```json
     {
       "name": "John Doe",
       "email": "johndoe@example.com"
     }
     ```

   - Save and test the function. If everything is correct, it should return a success message.

---

#### **Step 4: Set Up API Gateway to Trigger Lambda**
1. **Create a New API:**
   - Go to **API Gateway** and create a new REST API.
   - Create a new resource, e.g., `/users`, and then create HTTP methods (GET, POST, PUT, DELETE) to trigger the corresponding Lambda functions.

2. **Integrate API with Lambda**:
   - For each method (GET, POST, PUT, DELETE), set the integration type to **Lambda Function** and select the respective Lambda function.
   - Enable **Lambda Proxy Integration** to pass the event directly from the API Gateway to the Lambda function.

3. **Deploy API**:
   - Create a new **stage** (e.g., `dev`) and deploy your API.
   - Note the **Invoke URL** for testing.

---

#### **Step 5: Test with Postman**
1. **Test Create User**:
   - Open Postman and send a POST request to your API Gateway endpoint (`POST /users`).
   - Example body:
     ```json
     {
       "name": "Alice",
       "email": "alice@example.com"
     }
     ```

2. **Test Get User**:
   - Send a GET request (`GET /users/{id}`) to retrieve the user by ID.

3. **Test Update User**:
   - Send a PUT request (`PUT /users/{id}`) with updated data.

4. **Test Delete User**:
   - Send a DELETE request (`DELETE /users/{id}`) to delete the user.

---

#### **Step 6: Monitor and Debug**
- Use **CloudWatch Logs** to monitor the output of your Lambda functions and debug any issues.
- You can add logging in the Lambda function like this:
  
  ```python
  import logging
  logger = logging.getLogger()
  logger.setLevel(logging.INFO)
  
  logger.info("This is a log message.")
  ```

---
