# Serverless Contact Form with AWS Lambda, API Gateway, and DynamoDB

## 🚀 Project Overview

This project is a **fully serverless contact form**, built using AWS Lambda (Python), API Gateway, and DynamoDB. The frontend is a simple HTML file that can be opened in any browser—**no hosting or domain required**. Form submissions are securely processed and stored in DynamoDB with robust validation and error handling.

---

## 📝 Features

✅ 100% Serverless Architecture — No server management
✅ Secure data storage in DynamoDB with unique IDs and timestamps
✅ API Gateway securely exposes Lambda as a REST API
✅ Input validation on both client and server sides
✅ CORS enabled — works from any browser, locally or hosted
✅ User-friendly error handling with backend logging
✅ AWS portfolio use

---

## 📁 Project Structure

```
/
├── FrontendForm.html         # The HTML contact form
├── lambda/
│   └── lambda_function.py    # Python code for AWS Lambda
├── Screenshots/              # Project images
└── README.md                 # This documentation
```

---

## 🏗️ Architecture

```
[HTML Form] 
     |
     |  (POST JSON)
     v
[API Gateway] 
     |
     v
[AWS Lambda (Python)] 
     |
     v
[DynamoDB Table]
```

**Components:**

* **Frontend:** Static HTML form using JavaScript `fetch` to call API Gateway
* **API Gateway:** REST API endpoint with CORS enabled
* **Lambda:** Python function for validation, error handling, and DynamoDB integration
* **DynamoDB:** Stores submissions with `id`, `name`, `email`, `message`, and `submittedAt`

---

## ⚙️ Setup Instructions

### 1. DynamoDB Table

* **Table Name:** `ContactForm`
* **Partition Key:** `id` (String)

---

### 2. IAM Role for Lambda

* Create a new IAM Role
* Attach these policies:

  * `AmazonDynamoDBFullAccess`
  * `AWSLambdaBasicExecutionRole`

---

### 3. Lambda Function (Python)

* Use the code from `lambda/lambda_function.py`
* Set environment variables if needed:
* Select Previously Created IAM role

  ```
  Key: DYNAMODB_TABLE  
  Value: Your DynamoDB table name  
  ```

---

### 4. API Gateway

* Create a **REST API**
* Resource: `/contact`
* Method: `POST` (integrated with Lambda)
* Enable CORS for the resource
* Deploy the API and copy the **Invoke URL**

---

### 5. Frontend HTML Setup — Correct Steps & Common Mistakes

✅ **Update the Fetch URL:**
In `FrontendForm.html`, update the API `fetch` URL to your correct API Gateway endpoint (from API Gateway → Stages → Invoke URL).

---

### ⚠️ **Common Mistake: Do NOT open the HTML file directly via double-click (file:// path)**

Opening the file directly may cause form submissions to fail due to browser security restrictions like CORS blocking API calls.

---

### ✅ **Correct Way to Run the HTML (Local Server Setup):**

1. **Ensure Python is installed:**

   * If not, download from [https://www.python.org/downloads/](https://www.python.org/downloads/)
   * During installation, check **Add Python to PATH**

2. **Open Command Prompt and navigate to the folder containing your HTML file:**

   ```bash
   cd path\to\your\folder
   ```

3. **Run a simple local server using Python:**

   ```bash
   python -m http.server 5500
   ```

4. **Access the form in your browser:**

   ```
   http://localhost:5500/FrontendForm.html
   ```

   This ensures the form works properly and API calls function as expected.

---

## 💡 Advanced Features

* Unique IDs generated using UUIDs
* Submissions timestamped with ISO format
* Robust validation to prevent empty or invalid inputs
* Clear, user-friendly error messages for users
* Backend logging for easy debugging
* IAM Roles ensure least-privilege security

---

## 🛡️ Security & Best Practices

✅ IAM roles restrict Lambda access to only required AWS services
✅ No secrets or credentials in frontend code
✅ Backend handles all sensitive logic
✅ CORS configured with necessary restrictions
✅ DynamoDB properly structured with secure access

---

## 📚 Technologies Used

* **AWS Lambda** (Python 3.12)
* **AWS API Gateway** (REST API)
* **AWS DynamoDB**
* **HTML5 & JavaScript** (Fetch API)

---

## 📦 How to Run Locally

1. Clone this repository
2. Set up AWS resources as described above
3. Update the API endpoint in `FrontendForm.html`
4. Run a local server and open the form in your browser as shown in the steps

---

## 🎯 This Project Demonstrates:

✅ Practical AWS serverless skills
✅ Secure, scalable, and production-ready architecture
✅ Real-world validation and error handling
✅ Clean, professional code and clear documentation

---
