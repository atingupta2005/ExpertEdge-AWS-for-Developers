### **Creating a Simple API CRUD Application using AWS RDS and AWS Lambda**

#### **Overview:**
In this guide, we will walk you through the steps to create a simple CRUD (Create, Read, Update, Delete) API using Flask (Python) with AWS RDS (Relational Database Service) and AWS Lambda. The API will interact with an RDS database for storing and retrieving data, while AWS Lambda will handle the requests without using any additional AWS services unless required.

You will use Postman to test the API endpoints after deploying your Lambda functions.

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
   USE flask_app;
   ```

   ```sql
   CREATE TABLE users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(100) NOT NULL,
      email VARCHAR(100) NOT NULL,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

---

### Steps to deploy Python CRUD App:

#### 1. **Set up the virtual environment**:

Create a Python virtual environment and install required libraries.

1. **Create a project folder**:
   ```bash
   cd ~
   git clone https://github.com/atingupta2005/aws-rds-python-flask-crud
   cd aws-rds-python-flask-crud
   ```

2. **Create and activate the virtual environment**:
   ```bash
   sudo apt-get install python3 python3-pip -y 
   sudo apt-get install python3-pip -y 
   sudo apt install python3.12-venv -y
   python3 -m venv ~/venv
   source ~/venv/bin/activate
   ```

3. **Install necessary Python libraries**:
   ```bash
   pip install -r requirements.txt
   ```

#### 2. **Create the Flask App**:
 - Refer: 
   - https://github.com/atingupta2005/aws-rds-python-flask-crud
#### 5. **Run the Flask Application**:

1. **Activate the Virtual Environment** (if it's not activated):
   ```bash
   source ~/venv/bin/activate
   ```

2. **Run the Flask App**:
   ```bash
   cd ~/aws-rds-python-flask-crud
   python app.py
   ```

3. Open your web browser and go to `http://127.0.0.1:5000` to see the CRUD application in action.

---

### Summary of Features:

1. **Create** a new user via a form.
2. **Read** the list of users from the MySQL database.
3. **Update** a user's information via the edit page.
4. **Delete** a user from the database.

---
