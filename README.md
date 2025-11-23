# Student Registration System

A simple **Flask** web application to manage student records with **MongoDB** as the backend database. Users can **add, view, update, and delete** student details.

---

## Features

* List all students on the home page
* Add a new student
* Update existing student details
* Delete a student with confirmation
* Simple and responsive UI using Bootstrap

---

## Tech Stack

* **Backend:** Python, Flask
* **Database:** MongoDB (via Flask-PyMongo)
* **Frontend:** HTML, Jinja2 templates, Bootstrap 5
* **Environment Variables:** Managed via `.env` file

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <repo-folder>
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
# Activate venv
# Windows:
venv\Scripts\activate
# Linux / Mac:
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

**`requirements.txt` example:**

```
Flask
Flask-PyMongo
python-dotenv
bson
```

### 4. Configure environment variables

Create a `.env` file in the project root:

```
MONGO_URI=<your-mongodb-connection-string>
SECRET_KEY=<your-secret-key>
```

### 5. Run the application

```bash
python app.py
```

Open your browser at: [http://localhost:8000](http://localhost:8000)

---

## Project Structure

```
project/
│
├── templates/
│   ├── base.html
│   ├── index.html
│   ├── add_student.html
│   ├── update_student.html
│
├── app.py
├── requirements.txt
└── .env
```

---

## Screenshots

**Home Page**
Lists all students with Edit/Delete buttons.
- <img width="1902" height="607" alt="image" src="https://github.com/user-attachments/assets/a58a6a6d-4978-4769-8074-232e4d31e69d" />


**Add Student**
Form to add a new student.
- <img width="1897" height="801" alt="image" src="https://github.com/user-attachments/assets/d65d25c3-ebb5-410a-adb1-e130ad7c5878" />


**Update Student**
Form pre-filled with student details.
- <img width="1905" height="897" alt="image" src="https://github.com/user-attachments/assets/04febf01-879f-431f-ab07-abcfb993acf1" />



---

## Notes

* Make sure MongoDB is running and accessible via the URI in `.env`
* Delete action includes a confirmation page to prevent accidental deletion
* Uses `ObjectId` from `bson` to work with MongoDB document IDs

---

## License

MIT License

---


------------------------------------------------------------------------------------------------
1. Jenkins CI CD pipeline for flask application

. AWS EC2 SETUP
1.1 Launch EC2 Instance
•	OS: Ubuntu 22.04
•	Instance type: t2.micro
•	Open the following ports in the security group:
o	22 (SSH)
o	8080 (Jenkins)
o	5000 (Flask app staging environment)

<img width="940" height="408" alt="image" src="https://github.com/user-attachments/assets/f198bc3a-dd8e-403c-915e-b6fa71a10953" />

 

2.1 Install Java (required for Jenkins)
sudo apt update
sudo apt install openjdk-17-jdk -y

<img width="940" height="475" alt="image" src="https://github.com/user-attachments/assets/78b1dc89-de32-4c3e-89c1-3e7a0a896991" />

 
Login to Jenkins by getting the password 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

 <img width="940" height="486" alt="image" src="https://github.com/user-attachments/assets/26ca922a-5a0a-49b7-a2dc-cf1a31d00f83" />


Install Suggested plugins

You will be promted to a form to update username password 

http://35.179.183.102:8080/
<img width="940" height="452" alt="image" src="https://github.com/user-attachments/assets/a2ccbb48-3fdc-4922-8a3c-71a13484fcc8" />

 

3. CONFIGURE JENKINS WITH PYTHON

Install Python + pip:

sudo apt install python3 python3-pip -y

Install necessary plugins in Jenkins:
•	Git plugin
•	Pipeline plugin
•	Email Extension plugin
Create a Python virtual environment (optional but recommended):
sudo pip3 install virtualenv
Check for necessary plugins in jenkins
•  Git plugin
•  Pipeline plugin
•  Email Extension plugin

4. FORK SAMPLE FLASK APPLICATION and after forking clone it as below: 
 <img width="940" height="284" alt="image" src="https://github.com/user-attachments/assets/70ce700c-3e76-49a2-9513-7f81dd00b6b4" />


CREATE THE JENKINSFILE at root of your repo project and push it to your githhub repo.

6. CONFIGURE GITHUB WEBHOOK TRIGGERS
1.	In Jenkins → Job → Configure:
o	Check GitHub hook trigger for GITScm polling
2.	Pipeline Section
Select:
Definition: Pipeline script from SCM
SCM: Git
Branch: main
Script Path: Jenkinsfile
o	
3.	In your GitHub repo:
Settings → Webhooks → Add webhook
Payload URL: http://EC2-PUBLIC-IP:8080/github-webhook/
Content type: application/json
Trigger: Just the push event
This ensures every push to main branch triggers the pipeline.


 <img width="940" height="313" alt="image" src="https://github.com/user-attachments/assets/0927dab0-128c-4a3b-8467-77ff2951b207" />

7. SETUP EMAIL NOTIFICATIONS
In Jenkins:
Manage Jenkins → Configure System → Email Notification
SMTP example for Gmail:
SMTP server: smtp.gmail.com
Port: 587
Use SSL: Yes
Username: your-email@gmail.com
App Password: xxxxxxxx (from Google App Passwords)


 <img width="940" height="509" alt="image" src="https://github.com/user-attachments/assets/27f3159f-5dd7-4e6b-8edb-dad739c9df78" />

________________________________________
8. DEPLOYMENT ON EC2 (STAGING ENVIRONMENT)
Flask app runs automatically from Jenkins:
nohup python app.py &
Access the Flask app via:
http://EC2-PUBLIC-IP:5000

 


 <img width="940" height="673" alt="image" src="https://github.com/user-attachments/assets/2b15707a-e17b-4cf1-b171-a15f926d1bdf" />


<img width="940" height="640" alt="image" src="https://github.com/user-attachments/assets/d77a8577-f603-4ee2-bd0c-9937b3bd4417" />


 





