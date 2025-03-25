**Deploying a Python Flask Application on EC2: Hands-on Guide**

---

### **1. Launch an EC2 Instance**

**Step 1: Sign in to the AWS Management Console**
- Go to the [AWS Management Console](https://aws.amazon.com/console/).
- Log in with your AWS account credentials.

**Step 2: Launch a New EC2 Instance**
- Navigate to **EC2** under the **Compute** section.
- Click on the **Launch Instance** button.

**Step 3: Choose an Amazon Machine Image (AMI)**
- Choose an **Amazon Linux 2 AMI** or **Ubuntu** AMI. Both work well with Flask.
- Click **Select** to proceed.

**Step 4: Choose an Instance Type**
- Select an instance type (e.g., **t2.micro** for a lightweight app and free-tier eligible).
- Click **Next: Configure Instance Details**.

**Step 5: Configure Instance**
- Leave the default settings for now. If needed, configure network and subnet.
- Click **Next: Add Storage**.

**Step 6: Add Storage**
- You can leave the default storage settings unless more disk space is required.
- Click **Next: Add Tags**.

**Step 7: Add Tags**
- You can tag your instance (e.g., Name: FlaskApp).
- Click **Next: Configure Security Group**.

**Step 8: Configure Security Group**
- Add a new security group (e.g., **FlaskApp-SG**).
  - Allow **SSH** (port 22) for remote access from your IP.
  - Allow **HTTP** (port 80) for web traffic to your Flask application.
- Click **Review and Launch**.

**Step 9: Launch the Instance**
- Review the configuration and click **Launch**.
- When prompted, select **Create a new key pair**, name it (e.g., **FlaskApp-Key**), and download the key pair. This will be used to SSH into your instance.
- Click **Launch Instances**.

---

### **2. Access the EC2 Instance via SSH**

**Step 1: Find Your Instance’s Public IP**
- After launching, go to the **Instances** section of the EC2 Dashboard.
- Select your instance and note the **Public IP** address under the **Description** tab.

**Step 2: Access via SSH**
- Open your terminal (Linux/Mac) or a tool like **PuTTY** (Windows).
- Change the permissions of your key file to make it secure:
  ```bash
  chmod 400 /path/to/FlaskApp-Key.pem
  ```
- Connect to your EC2 instance via SSH:
  ```bash
  ssh -i /path/to/FlaskApp-Key.pem ec2-user@<Your_Public_IP>
  ```
  Replace `<Your_Public_IP>` with your instance's public IP address.

---

### **3. Install Python and Flask on the EC2 Instance**

**Step 1: Update the Instance**
- Once you’re logged into the instance, update the package lists:
  ```bash
  sudo yum update -y     # For Amazon Linux
  sudo apt-get update -y # For Ubuntu
  ```

**Step 2: Install Python and Pip**
- Check if Python is already installed:
  ```bash
  python3 --version
  ```
- If Python is not installed, install it:
  ```bash
  sudo yum install python3 -y  # For Amazon Linux
  sudo apt-get install python3 python3-pip -y  # For Ubuntu
  ```
- Install pip (Python's package installer) if needed:
  ```bash
  sudo yum install python3-pip -y  # For Amazon Linux
  sudo apt-get install python3-pip -y  # For Ubuntu
  ```

**Step 3: Install Flask**
- Install Flask using pip:
  ```bash
  pip3 install flask
  ```

---

### **4. Create a Simple Flask Application**

**Step 1: Create a Flask Application Directory**
- Create a directory for your Flask app:
  ```bash
  git clone https://github.com/atingupta2005/flask-hello-world
  cd flask-hello-world
  ```

---

### **5. Run the Flask Application**

**Step 1: Run the Flask App**
- Run the Flask app by executing the following:
  ```bash
  pip install -r requirements.txt
  python3 app.py
  ```

**Step 2: Test the Application**
- Open a browser and navigate to your EC2 instance's public IP address:
  ```
  http://<Your_Public_IP>/
  ```
- You should see the "Hello, World!" message displayed.

---

