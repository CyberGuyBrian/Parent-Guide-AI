# Parent-Guide-AI
AI-powered digital safety assistant helping parents set smarter online boundaries

# 👨‍👩‍👧‍👦 Parent Guide AI

**Parent Guide AI** is a privacy and digital-safety assistant built on **AWS Bedrock** and **Anthropic Claude 3 Haiku**.  
It helps parents set clear, healthy digital boundaries for their children by guiding them through privacy settings, app controls, and screen-time rules — all in plain, supportive language.

---

## 🧠 Overview

Parent Guide AI gives parents the confidence to manage their family’s online world safely — without needing to be tech experts.

Example questions it answers:
- “How can I make my child’s TikTok account private?”
- “What are safe screen time limits for a 10-year-old?”
- “How do I turn off location sharing on my kid’s iPhone?”

The system analyzes the question and responds with step-by-step, parent-friendly guidance — all processed securely through AWS.

---

## 🧩 MVP Goals (Phase 1)

- Accept text input through AWS Lambda and API Gateway  
- Process the message with **Amazon Bedrock (Anthropic Haiku)**  
- Return short, actionable safety guidance as JSON  
- Log all requests in **CloudWatch** for transparency and debugging  

---

## ⚙️ Architecture Overview

| Layer | AWS Service | Purpose |
|-------|--------------|----------|
| Compute | **AWS Lambda (Python 3.11)** | Executes text requests and AI responses |
| AI Model | **Amazon Bedrock – Anthropic Haiku** | Generates parent-friendly guidance |
| API Gateway | **REST endpoint** | Connects web or chat frontends to Lambda |
| Logging | **Amazon CloudWatch** | Monitors logs and performance |
| IAM Roles | **Least privilege** | Grants Bedrock access safely |

---

## 🧰 Tech Stack

- **Language:** Python 3.11  
- **AI Model:** Anthropic Haiku (via Amazon Bedrock)  
- **Platform:** AWS Serverless  
- **Logging:** CloudWatch  
- **Security:** IAM Roles + Encrypted Environment Variables  

---

## ⚙️ Setup Instructions

### 1. Enable Anthropic Model Access
- In the AWS Console → **Amazon Bedrock → Model Access**
- Request access for **Anthropic Claude 3 Haiku**
- Region: **us-east-1**

### 2. Create Lambda Function
- Name: `parentguide-bedrock-helper`
- Runtime: **Python 3.11**
- Paste the code from `/lambda/bedrock_helper.py`
- Click **Deploy**

### 3. Attach IAM Policy
Attach the following inline policy to your Lambda’s execution role:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BedrockInvokeModelPermission",
      "Effect": "Allow",
      "Action": ["bedrock:InvokeModel"],
      "Resource": [
        "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-haiku-20240307-v1:0"
      ]
    }
  ]
}
