Perfect — here is a **complete, GitHub-ready README.md** that you can **directly copy–paste**.
It is written like a **serious open-source ML project**, with **step-by-step flow + diagrams + architecture**.

---

# 📧 Synthetic ATS Email Generator — Client Feedback Module

A production-grade **synthetic HR email dataset generator** powered by a locally hosted LLM (Ollama).
This module generates **Client Feedback Update emails**, a critical stage in real-world Applicant Tracking Systems (ATS).

Built for **training NLP classifiers, ATS automation systems, and LLM fine-tuning pipelines**.

---

## 🧠 What This Project Does

This system automatically generates **hundreds of unique, realistic HR emails** where recruiters update candidates after receiving feedback from a client.

Each email is structured into machine-learning-ready fields:

* `SUBJECT`
* `BODY`
* `TONE`
* `INTENT`

The output is a **clean CSV dataset** directly usable for model training.

---

## 🏗 High-Level System Architecture

```
+----------------------+
|  Random Role Picker  |
+----------------------+
            |
            v
+----------------------+
| Random Adjective Gen |
+----------------------+
            |
            v
+----------------------+
|  Prompt Constructor  |
+----------------------+
            |
            v
+----------------------+
|   Ollama LLM Server  |
| llama3.2:3b-instruct |
+----------------------+
            |
            v
+----------------------+
|  Structured Response |
|  SUBJECT/BODY/TONE   |
+----------------------+
            |
            v
+----------------------+
|   Regex Field Parser |
+----------------------+
            |
            v
+----------------------+
| Duplicate Detection  |
|    (MD5 Hashing)     |
+----------------------+
            |
            v
+----------------------+
|   CSV Dataset Store  |
+----------------------+
```

---

## 🔁 Step-by-Step Email Generation Flow

```
START
  |
  v
Select Random Role + Adjective
  |
  v
Insert into BASE_USER_PROMPT
  |
  v
Send Prompt to Ollama API
  |
  v
Receive Raw LLM Output
  |
  v
Regex Parse SUBJECT, BODY, TONE, INTENT
  |
  +-----> Parse Failed? → Save to debug/
  |
  v
Generate MD5 Hash of Email Body
  |
  +-----> Duplicate Found? → Discard & Retry
  |
  v
Write Clean Row to CSV
  |
  v
Log Success
  |
  v
NEXT EMAIL
```

---

## 🧬 Position in Real ATS Workflow

This module models a real recruitment pipeline stage:

```
Candidate Applies
       |
       v
Profile Submitted to Client
       |
       v
Client Reviews Profile
       |
       v
CLIENT FEEDBACK RECEIVED   <--- (THIS MODULE)
       |
       v
Next Steps (Interview / Hold / Reject)
```

This is why the class is called **client_feedback**.

---

## 🗂 Folder Structure

```
client-feedback/
│
├── client_feedback.csv
├── client_feedback_history.log
└── debug/
    ├── fail_21_att1.txt
    ├── fail_76_att2.txt
```

---

## 📊 Output CSV Schema

```
+----+------------------+------------------+----------------------+-------------------------------+
| id | subject           | body             | tone                 | intent                        |
+----+------------------+------------------+----------------------+-------------------------------+
| 1  | Client Feedback...| Dear Rohan...     | Professional, neutral| Inform candidate feedback ... |
+----+------------------+------------------+----------------------+-------------------------------+
```

Each row is a **fully labeled training example**.

---

## ⚙️ Step 1 — Install Requirements

### Install Ollama

Download from: [https://ollama.com](https://ollama.com)

Then pull the model:

```bash
ollama pull llama3.2:3b-instruct-q4_0
```

---

## ⚙️ Step 2 — Start Ollama Server

```bash
ollama serve
```

Your script connects to:

```
http://localhost:11434/api/generate
```

---

## ⚙️ Step 3 — Configure Script

Edit these values at the top of the file:

```python
MODEL_NAME = "llama3.2:3b-instruct-q4_0"

OUTPUT_CSV = "E:\\Synthetic-Email-Generation-tool-main\\client-feedback\\client_feedback.csv"
DEBUG_DIR = "E:\\Synthetic-Email-Generation-tool-main\\client-feedback\\debug"
LOG_FILE = "E:\\Synthetic-Email-Generation-tool-main\\client-feedback\\client_feedback_history.log"

NUM_EMAILS = 700
DELAY_SECONDS = 0.1
MAX_RETRIES = 3
```

---

## ▶️ Step 4 — Run the Generator

```bash
python client_feedback_generator.py
```

Live output:

```
Generating ID 214/700... ✅ Saved
```

---

## 🧠 Internal Components Explained

### 1. Prompt Controller

```
ROLE + ADJECTIVE
        |
        v
+------------------------+
| BASE_USER_PROMPT       |
| Strict ATS constraints |
+------------------------+
```

Forces consistent, clean structure.

---

### 2. Regex Parser

```
RAW LLM TEXT
     |
     v
SUBJECT:
BODY:
TONE:
INTENT:
```

Regex ensures **schema stability for ML pipelines**.

---

### 3. Duplicate Protection Engine

```
EMAIL BODY
    |
    v
MD5 HASH
    |
    +-- Exists? → Reject
    |
    v
Store as Unique
```

Prevents dataset poisoning by repeated samples.

---

## 🔄 Crash-Proof Resume System

If the script stops:

```
Last ID = 388
```

On restart:

```
RESUMING from ID 389
```

No duplicates, no data loss.

---

## 🛑 Graceful Stop System

Create a file:

```
stop.txt
```

Flow:

```
stop.txt detected
        |
        v
Finish current email
        |
        v
Exit safely
```

---

## 🧪 Full ATS Dataset Coverage

This module fits into a complete pipeline:

```
job_application
candidate_application
client_submission
client_feedback
interview_scheduling
interview_confirmation
interview_followup
candidate_selection
offer_sent
offer_response
```

This mirrors real ATS systems used in enterprises.

---

## 📈 Production-Grade Features

| Feature                | Included |
| ---------------------- | -------- |
| Large-scale generation | ✅        |
| Deduplication          | ✅        |
| Resume-safe execution  | ✅        |
| Failure logging        | ✅        |
| Structured output      | ✅        |
| ATS tone control       | ✅        |

---

## 🎯 Designed For

* ATS email classification models
* Recruitment automation systems
* NLP research datasets
* LLM fine-tuning corpora

---


