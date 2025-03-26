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
- Choose an **Ubuntu** AMI

**Step 4: Choose an Instance Type**
- Select an instance type (e.g., **t3.micro** for a lightweight app).

**Step 5: Configure Instance**
- Leave the default settings for now. If needed, configure network and subnet.

**Step 6: Add Storage**
- You can leave the default storage settings unless more disk space is required.

**Step 7: Add Tags**
- You can tag your instance (e.g., Name: FlaskApp).

**Step 8: Configure Security Group**
  - Allow **SSH** (port 22) for remote access from your IP.
  - Allow port 5000 for web traffic to your Flask application.

**Step 9: Launch the Instance**
- Review the configuration and click **Launch**.


---

### **2. Access the EC2 Instance via SSH**

### **3. Install Python and Flask on the EC2 Instance**

**Step 1: Update the Instance**
- Once you’re logged into the instance, update the package lists:
  ```bash
  sudo apt-get update -y # For Ubuntu
  ```

**Step 2: Install Python and Pip**
- Check if Python is already installed:
  ```bash
  python3 --version
  ```
- If Python is not installed, install it:
  ```bash
  sudo apt-get install python3 python3-pip -y  # For Ubuntu
  ```
- Install pip (Python's package installer) if needed:
  ```bash
  sudo apt-get install python3-pip -y  # For Ubuntu
  ```

---

### **4. Create a Simple Flask Application**

**Step 1: Create a Flask Application Directory**
- Create a directory for your Flask app:
  ```bash
  cd ~
  git clone https://github.com/atingupta2005/flask-hello-world
  cd ~/flask-hello-world
  ```

---

### **5. Run the Flask Application**

**Step 1: Run the Flask App**
- Run the Flask app by executing the following:
  ```bash
  sudo apt install python3.12-venv -y
  python3 -m venv ~/venv
  source ~/venv/bin/activate
  cd ~/flask-hello-world
  pip install -r requirements.txt
  python app.py
  ```

**Step 2: Test the Application**
- Open a browser and navigate to your EC2 instance's public IP address:
  ```
  http://<Your_Public_IP>:5000/
  ```
- You should see the "Hello, World!" message displayed.

---

