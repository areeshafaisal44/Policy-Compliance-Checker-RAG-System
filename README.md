# Policy-Compliance-Checker-RAG-System

## 📌 Overview

The **Policy Compliance Checker RAG System** is a Retrieval-Augmented Generation (RAG) pipeline built using **LangChain**, **Gemini**, and the **CUAD dataset**. Its purpose is to automatically evaluate whether corporate documents — such as company policies, HR manuals, security protocols, or compliance guidelines — follow a predefined set of rules.

The system retrieves relevant policy sections and checks them against compliance rules, providing:

- ✅ Evidence from the document  
- ✅ Compliance verdict (Compliant / Non-Compliant)  
- ✅ Explanation  
- ✅ Recommended corrections  

---

## 🚀 Key Features

- 🔍 PDF ingestion pipeline (extract → chunk → embed → vector DB)  
- 🎯 Rule-based compliance evaluation (15+ customizable rules)  
- 🤖 LangChain RAG integrated with Gemini  
- 🧠 Multi-step agent for sequential compliance checking  
- 📊 Comparison table for compliant vs non-compliant sections  
- 🧩 Modular codebase with reusable components  

---

## 📂 Project Structure

```

├── data/
│   └── policies/                # PDF files
├── rules/
│   └── compliance_rules.json    # 15+ compliance rules
├── vectorstore/
│   └── chroma/                  # Chroma DB embeddings
├── src/
│   ├── ingest.py                # PDF → Embeddings pipeline
│   ├── rag_pipeline.py          # Retriever + LLM logic
│   ├── compliance_checker.py    # Main compliance evaluation tool
│   ├── agent.py                 # Multi-step compliance agent
│   └── utils.py
├── outputs/
│   ├── compliance_report.json
│   └── comparison_table.csv
└── README.md

````

---

## 📘 1. Compliance Rules File (JSON)

Example: `rules/compliance_rules.json`

```json
[
  {
    "id": "R1",
    "rule": "The document must clearly define data retention duration.",
    "category": "Data Security"
  },
  {
    "id": "R2",
    "rule": "The policy must specify employee grievance reporting procedures.",
    "category": "HR"
  }
]
````

Minimum required: **15 rules**

---

## 📥 2. PDF Ingestion & Vector Store Pipeline

Run the ingestion script:

```bash
python src/ingest.py
```

The script:

* Extracts text from PDFs
* Cleans + splits text using RecursiveCharacterTextSplitter
* Embeds chunks using Gemini Embeddings
* Stores vectors into **Chroma DB**

---

## 🎯 3. RAG Pipeline

Retriever:

```python
retriever = vectorstore.as_retriever(
    search_type="similarity",
    k=5
)
```

LLM evaluation:

```python
response = llm.invoke({
    "rule": rule_text,
    "context": retrieved_chunks
})
```

---

## 🧠 4. Compliance Checker Tool

Returns:

* **Compliance Status:** Compliant / Non-Compliant
* **Evidence:** Retrieved text snippet
* **Explanation:** Why the rule passed/failed
* **Fix Suggestions:** What to add/edit

Run:

```bash
python src/compliance_checker.py
```

---

## 🤖 5. Multi-Step Compliance Agent

The agent sequentially:

1. Loads all rules
2. Retrieves context for each rule
3. Sends to Gemini for evaluation
4. Generates a detailed report

Run:

```bash
python src/agent.py
```

---

## 📊 6. Comparison Table (CSV)

Sample output:

| Rule ID | Description                    | Status          | Evidence              |
| ------- | ------------------------------ | --------------- | --------------------- |
| R1      | Define data retention duration | ❌ Non-Compliant | —                     |
| R2      | Grievance procedure            | ✅ Compliant     | “Employees may file…” |

Stored in:

```
outputs/comparison_table.csv
```
---

## 🛠️ Installation

### **1. Clone repository**

```bash
git clone https://github.com/yourusername/policy-rag-compliance.git
cd policy-rag-compliance
```

### **2. Install dependencies**

```bash
pip install -r requirements.txt
```

### **3. Add API key**

Create `.env`:

```
GEMINI_API_KEY=your_api_key
```

---

## ▶️ How to Run

### **Step 1 — Ingest PDFs**

```bash
python src/ingest.py
```

### **Step 2 — Run Compliance Checker**

```bash
python src/compliance_checker.py
```

### **Step 3 — Run Full Agent Workflow**

```bash
python src/agent.py
```

---

## 📄 Output Files

* `compliance_report.json` — Rule-by-rule compliance results
* `comparison_table.csv` — Compliant vs non-compliant overview
* `retriever_logs/` — Evidence and retrieved chunk history

---

## 🧩 Built With

* Python
* LangChain
* Gemini API
* Chroma DB
* CUAD Dataset
* PDFPlumber / PyPDF2

---

## 🧠 Future Improvements

* Fine-tune embeddings on legal corpora
* Add PDF annotation (mapping evidence back to pages)
* Build Streamlit/FastAPI dashboard
* Add automated scoring metrics


Just tell me!
```
