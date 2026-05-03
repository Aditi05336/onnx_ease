# 🚀 AI Model Hosting & Execution Platform (AWS Serverless)

A fully serverless platform to **upload, store, manage, and run ONNX machine learning models** using AWS.  
This system allows you to deploy ML models as APIs without managing infrastructure.

---

## 🧠 Architecture Overview

```mermaid
flowchart LR

    %% Client Layer
    subgraph Client
        U[User]
        FE[Vercel Frontend]
        U --> FE
    end

    %% API Layer
    subgraph API Layer
        APIGW[API Gateway]
    end

    %% Compute Layer
    subgraph Compute (AWS Lambda)
        L1[Get Upload URL]
        L2[Upload Model]
        L3[Run Model]
        L4[Get Models]
        L5[Delete Model]
    end

    %% Storage
    subgraph Storage
        S3[(S3 Bucket)]
    end

    %% Monitoring
    subgraph Monitoring
        CW[CloudWatch]
    end

    %% Connections
    FE --> APIGW

    APIGW --> L1
    APIGW --> L2
    APIGW --> L3
    APIGW --> L4
    APIGW --> L5

    %% Core Flows
    L1 --> S3
    FE -->|Upload file| S3
    L2 --> S3

    L3 --> S3
    L4 --> S3
    L5 --> S3

    %% Logging
    L1 --> CW
    L2 --> CW
    L3 --> CW
    L4 --> CW
    L5 --> CW
```

---

## 📦 Features

- Upload ONNX models using pre-signed URLs  
- Store models securely in S3  
- Run models via API (serverless inference)  
- Fetch all user models  
- Delete models anytime  
- Logging with CloudWatch  
- Fully serverless and scalable  

---

## 🔗 API Endpoints

### 📤 Get Upload URL
`GET /get-upload-url`

Generates a pre-signed URL for uploading your ONNX model.

---

### 📥 Upload Model
`POST /upload-model`

Registers uploaded model metadata.

---

### 📄 Get Models
`GET /models/{userid}`

Returns all models for a user.

---

### ▶️ Run Model
`POST /run-model/{userid}/{modelid}`

Runs inference using ONNX Runtime.

---

### 🗑️ Delete Model
`DELETE /models/{userid}/{modelid}`

Deletes model from storage.

---

## 🔄 Workflow

1. Request upload URL  
2. Upload `.onnx` file to S3  
3. Register model  
4. Fetch available models  
5. Run model via API  
6. Delete model if needed  

---

## ⚙️ Tech Stack

- AWS Lambda  
- Amazon S3  
- API Gateway  
- CloudWatch  
- Vercel  
- ONNX Runtime  

---

## 🔐 Security

- Pre-signed URLs for secure uploads  
- IAM roles for controlled permissions  
- API Gateway for request validation  

---

## 📊 Monitoring

- CloudWatch logs for all Lambda executions  
- Error tracking and debugging  

---

## 🚧 Future Improvements

- Authentication (JWT / Cognito)  
- Model versioning  
- Batch inference  
- GPU-based execution  

---

## 🧑‍💻 Author

Serverless ML deployment platform built using AWS.
