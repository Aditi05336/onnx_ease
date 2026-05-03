# 🚀 AI Model Hosting & Execution Platform (AWS Serverless)

A fully serverless platform to **upload, store, manage, and run ONNX machine learning models** using AWS services.  
Built for seamless integration with modern frontends (e.g., Vercel), this system allows users to deploy ML models as APIs without managing infrastructure.

---

## 🧠 System Architecture & Flow

```mermaid
flowchart TD

    User[User / Client] --> Frontend[Vercel Frontend]

    Frontend --> APIGW[Amazon API Gateway]

    APIGW --> L1[Lambda: Get Upload URL]
    APIGW --> L2[Lambda: Upload Model Metadata]
    APIGW --> L3[Lambda: Run Model]
    APIGW --> L4[Lambda: Get Models]
    APIGW --> L5[Lambda: Delete Model]

    S3[(Amazon S3 Bucket)]
    CW[CloudWatch Logs]

    %% Upload Flow
    L1 -->|Generate Pre-signed URL| S3
    Frontend -->|Upload ONNX via URL| S3
    L2 -->|Store metadata| S3

    %% Run Flow
    L3 -->|Fetch model| S3
    L3 -->|Run inference (ONNX Runtime)| L3

    %% List & Delete
    L4 -->|Fetch models| S3
    L5 -->|Delete model| S3

    %% Monitoring
    L1 --> CW
    L2 --> CW
    L3 --> CW
    L4 --> CW
    L5 --> CW
```

---

## 📦 Features

- 📤 Upload ONNX models using secure pre-signed URLs  
- ☁️ Store models in Amazon S3  
- ▶️ Run models via API (serverless inference)  
- 📄 Fetch all user models  
- 🗑️ Delete models anytime  
- 📊 Logging & monitoring with CloudWatch  
- ⚡ Fully serverless and scalable  

---

## 🔗 API Endpoints

### 📤 Get Upload URL

**GET /get-upload-url**

```
arn:aws:execute-api:us-east-1:761288222364:quqjmkt1sc/*/GET/get-upload-url
```

Generates a pre-signed URL for uploading your ONNX model.

**Response**
```json
{
  "uploadUrl": "https://s3.amazonaws.com/...",
  "fileKey": "models/user123/model.onnx"
}
```

---

### 📥 Upload Model

**POST /upload-model**

```
arn:aws:execute-api:us-east-1:761288222364:quqjmkt1sc/*/POST/upload-model
```

Registers the uploaded model.

**Request**
```json
{
  "userId": "user123",
  "modelName": "my-model",
  "fileKey": "models/user123/model.onnx"
}
```

---

### 📄 Get User Models

**GET /models/{userid}**

```
arn:aws:execute-api:us-east-1:761288222364:quqjmkt1sc/*/GET/models/{userid}
```

Returns all models for a user.

---

### ▶️ Run Model

**POST /run-model/{userid}/{modelid}**

```
arn:aws:execute-api:us-east-1:761288222364:quqjmkt1sc/*/POST/run-model/{userid}/{modelid}
```

Runs inference using the selected ONNX model.

**Request**
```json
{
  "input": [1.0, 2.0, 3.0]
}
```

**Response**
```json
{
  "output": [0.87]
}
```

---

### 🗑️ Delete Model

**DELETE /models/{userid}/{modelid}**

```
arn:aws:execute-api:us-east-1:761288222364:quqjmkt1sc/*/DELETE/models/{userid}/{modelid}
```

Deletes the model from storage and system.

---

## 🔄 Workflow

1. Call `/get-upload-url`  
2. Upload `.onnx` file to S3 using pre-signed URL  
3. Register model using `/upload-model`  
4. Fetch models using `/models/{userid}`  
5. Run model via `/run-model/{userid}/{modelid}`  
6. Delete model when needed  

---

## ⚙️ Tech Stack

- AWS Lambda (Serverless compute)  
- Amazon S3 (Storage)  
- API Gateway (API management)  
- CloudWatch (Logging & monitoring)  
- Vercel (Frontend hosting)  
- ONNX Runtime (Model inference)  

---

## 📊 Monitoring

All system activity is logged via CloudWatch:
- API request logs  
- Lambda execution logs  
- Error tracking and debugging  

---

## 🔐 Security

- Pre-signed URLs for secure file uploads  
- IAM roles for restricted access  
- API Gateway for controlled endpoint exposure  

---

## 🚧 Future Improvements

- 🔐 Authentication (JWT / AWS Cognito)  
- 📦 Model versioning  
- ⚡ Batch inference support  
- 🧠 GPU-based execution  
- 📊 Usage analytics dashboard  

---

## 🧑‍💻 Author

Built as a **serverless AI model deployment platform** using AWS.  
Designed to simplify ML model serving and make deployment accessible without infrastructure management.

---

## ⭐ Contribute / Feedback

Feel free to fork, improve, or suggest features!  
If you found this useful, consider giving it a ⭐
