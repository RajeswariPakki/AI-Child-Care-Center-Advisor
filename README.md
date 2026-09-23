# AI Child Care Center Advisor

An AI-powered solution built with Dynamics 365 and Dataverse to analyze child care center data, identify centers that may require additional support, evaluate training impact, and provide actionable recommendations.

> **Note:** This is a personal portfolio project built in a trial Dynamics 365 environment using sample data. No client or production data is used.

---

## 📌 Overview

The **AI Child Care Center Advisor** analyzes information related to a child care center, including:

* Training performance
* Goals and goal achievement
* Trainer visits and unresolved issues
* Funding and utilization
* Center capacity and enrollment

The system combines a **deterministic JavaScript scoring engine** with an **AI analysis layer**.

The numerical scores are calculated using JavaScript-based business logic so that the same CRM data consistently produces the same scores. The AI layer uses these calculated scores and CRM information to explain the situation and provide recommendations.

---

## 🎯 Problem Statement

Child care centers may have different levels of training performance, goal achievement, support requirements, and funding utilization.

Manually reviewing all this information can make it difficult to quickly identify:

* Which centers require attention
* Whether training is producing the expected impact
* What factors are contributing to a center's priority
* What type of follow-up action may be appropriate

This project provides a centralized way to analyze these factors and generate actionable insights.

---

## 💡 Solution

The solution consists of:

1. **Dynamics 365 / Dataverse**
   Stores child care center and related information.

2. **Custom HTML Web Resource**
   Provides the conversational interface inside the Dynamics 365 model-driven application.

3. **JavaScript Scoring Engine**
   Retrieves CRM data and calculates deterministic Priority and Training Impact scores.

4. **AI Analysis Layer**
   Receives the CRM data and authoritative scores and generates explanations and recommendations.

5. **CRM Write-back**
   The calculated scores and AI recommendation can be written back to the Child Care Site record.

---

## 🏗️ How It Works

```text
Dynamics 365 Model-Driven App
            │
            ▼
    HTML Web Resource
            │
            ▼
      Dataverse Web API
            │
            ▼
     Retrieve CRM Data
            │
            ▼
  JavaScript Scoring Engine
       │             │
       ▼             ▼
Priority Score   Training Impact
       │             │
       └──────┬──────┘
              ▼
        AI Analysis
              │
              ▼
       Recommendation
              │
              ▼
       CRM Record Update
```

---

## 📊 Scoring Approach

The project uses JavaScript to calculate the numerical scores rather than asking the AI model to calculate them.

### Priority Score

The Priority Score considers multiple risk factors:

| Factor                | Weight |
| --------------------- | -----: |
| Goal Risk             |    30% |
| Training Risk         |    25% |
| Support Risk          |    20% |
| Improvement Risk      |    15% |
| Resource/Funding Risk |    10% |

The resulting score is categorized as:

| Score  | Priority Level |
| ------ | -------------- |
| 0–39   | Low            |
| 40–69  | Medium         |
| 70–100 | High           |

### Training Impact Score

Training Impact considers:

* Goal improvement
* Training assessment performance
* Training application
* Training completion

The score is categorized as:

| Score  | Training Impact |
| ------ | --------------- |
| 0–39   | Low             |
| 40–69  | Moderate        |
| 70–100 | High            |

### Why deterministic scoring?

The scoring logic is intentionally separated from AI generation.

The AI model is instructed to treat the JavaScript-generated scores as **authoritative** and not recalculate or modify them.

This ensures that the same CRM data produces consistent numerical scores while AI is used primarily for analysis, explanation, and recommendations.

---

## 🗂️ Dataverse Data Model

The project uses five main entities:

### Child Care Site

Stores information about the child care center, including:

* Site name
* Status
* Capacity
* Current enrollment
* Priority Score
* Priority Level
* Training Impact Score
* AI Recommendation

### Training

Stores training-related information for each center, including:

* Training name
* Completion
* Assessment
* Application
* Training status

### Goals

Stores center goals and progress, including:

* Goal name
* Target
* Achievement
* Previous achievement
* Goal status

### Trainer Visit

Stores trainer support information, including:

* Trainer
* Unresolved issues
* Follow-up requirement
* Follow-up date

### Funding

Stores funding information, including:

* Funding name
* Amount received
* Amount utilized
* Utilization
* Funding purpose

---

## 🤖 AI Analysis

The AI component acts as an analysis and recommendation layer.

It receives:

* Center information
* JavaScript-calculated scores
* Training information
* Goal information
* Trainer visit information
* Funding information

The AI is instructed to:

* Use only the provided CRM information
* Avoid inventing information
* Focus only on the selected center
* Explain the factors contributing to the scores
* Provide practical next actions
* Treat the JavaScript-generated scores as authoritative

The AI does **not** replace the deterministic scoring logic.

---

## 🖥️ CRM Interface

The solution is implemented as a custom HTML web resource inside a Dynamics 365 model-driven application.

The Child Care Site record contains related information across areas such as:

* Training
* Goals
* Trainer Visits
* Funding

The conversational advisor can retrieve this information through the Dataverse Web API.

---

## 🛠️ Technology Stack

* **Microsoft Dynamics 365**
* **Microsoft Dataverse**
* **Power Apps Model-Driven App**
* **HTML**
* **CSS**
* **JavaScript**
* **Dataverse Web API**
* **Azure Functions**
* **AI / LLM**

---

## 📁 Project Structure

```text
AI-Child-Care-Center-Advisor/
│
├── README.md
│
├── web-resource/
│   └── center-advisor.html
│
├── sample-data/
│   ├── child-care-site.png
│   ├── training.png
│   ├── goals.png
│   ├── trainer-visits.png
│   └── funding.png
│
└── docs/
    └── data-model.md
```

---

## 🔐 Data & Security Disclaimer

This repository contains a **personal portfolio implementation** created using a trial Dynamics 365 environment.

* No client data is included.
* No production CRM data is included.
* Sample data was created specifically for demonstration purposes.
* Credentials, API keys, function keys, and other secrets should not be committed to this repository.
* Any Azure Function endpoint or authentication information should be configured securely outside the public source code.

---

## 🚀 Key Features

* Conversational interface inside Dynamics 365
* Dataverse Web API integration
* Automatic CRM data retrieval
* Deterministic Priority Score calculation
* Deterministic Training Impact Score calculation
* AI-powered analysis
* AI-generated recommendations
* CRM record write-back
* Multi-factor center prioritization
* Training effectiveness analysis

---

## 📌 Purpose

This project demonstrates how **Dynamics 365, Dataverse, JavaScript-based business logic, Azure Functions, and AI** can be combined to create an intelligent CRM-based decision-support solution.
