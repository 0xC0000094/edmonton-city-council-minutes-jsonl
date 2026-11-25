# Edmonton City Council Meeting Minutes (JSONL)

This repository contains a machine-readable dataset of **public meeting minutes** collected from **2021–2025** across approximately **72 committees**.  
The minutes have been parsed, cleaned, and converted into a **structured JSONL format** for use in:

- **Machine Learning (ML) & NLP research**
- **Civic analytics & transparency projects**
- **Fine-tuning or prompting LLMs for summarization and question answering**

---

## 📊 Dataset Overview

- **Years Covered:** 2021–2025  
- **Committees Covered:** ~72 (various committees, advisory boards, and council sessions)  
- **Source:** [City of Edmonton Public Meetings Portal](https://pub-edmonton.escribemeetings.com/)  
- **Format:** JSONL (one JSON object per line)  
- **Fields:** Meeting metadata, agenda items, attendance, and extracted content  

Example record:

```jsonc
{
  "document_id": "aca214f6ea903b5...",
  "filename": "2021_01_07_Emergency_Advisory_Committee.pdf",
  "meeting_metadata": {
    "date": "2021-01-07",
    "committee_name": "Emergency Advisory Committee"
  },
  "members": ["D. Iveson", "M. Banga", "T. Cartmell"],
  "agenda_items": [
    {"section": "1.4", "title": "Adoption of Agenda"},
    {"section": "2.0", "title": "Public Updates"}
  ],
  "attendance": {
    "present": ["D. Iveson", "M. Banga"],
    "absent_with_notice": ["T. Caterina"]
  },
  "extraction_metadata": {
    "processed_date": "2025-08-15T12:00:00",
    "human_reviewed": false
  }
}
````

---

## 📥 Getting the Dataset

You have two ways to get the data:

### **Option 1: Clone the Full Repository**

Includes the dataset, LICENSE, schema, and documentation.

```bash
git clone https://github.com/0xC0000094/edmonton-city-council-minutes-jsonl
cd edmonton-city-council-minutes-jsonl
```

### **Option 2: Download the File Directly**

If you only need the data:

* [Download JSONL File](https://github.com/0xC0000094/edmonton-city-council-minutes-jsonl/tree/main/data)

Save it somewhere on your computer and attach it to a GPT project or load it manually.

---

## 🧠 How to Use with GPT Projects

This dataset is designed to work **directly with GPT projects** so you can ask questions and generate summaries interactively.

### Why Attach the File

GPT projects run in a **secure sandbox** where they can:

1. Load your JSONL file
2. Run Python scripts to filter, summarize, and analyze meetings
3. Return tables, charts, or text summaries back to you

If you don’t attach the file, GPT cannot access your data it cannot browse your computer or the web by default.

### Step-by-Step Guide

1. **Choose your setup:**

   * Clone the repo (Option 1) OR download just the file (Option 2)
2. **Create a GPT Project**:

   * Open [ChatGPT Projects](https://chat.openai.com/)
   * Create a new project (or use an existing one)
3. **Attach the JSONL file**:

   * Upload `2025 - 08 extracted_data_for_review.jsonl`
   * The file will now be available in the sandbox for GPT to process
4. **Ask questions like**:

   * “Summarize all meetings from 2022.”
   * “List committees with the most meetings in 2024.”
   * “Count how many agenda items mention ‘budget’ between 2023-2025.”
   * “Generate a CSV of attendance for Audit Committee meetings.”

GPT will automatically write and execute Python code inside the sandbox to answer your question.

---

## 🚀 Quick Example in Python

You can also load the data manually:

```python
import json

with open("2025 - 08 extracted_data_for_review.jsonl", "r", encoding="utf-8") as f:
    for line in f:
        record = json.loads(line)
        if record["meeting_metadata"]["committee_name"] == "Audit Committee":
            print(record["meeting_metadata"]["date"], record["agenda_items"])
```

---

## 🛠 GPT Project Instructions

To ensure consistent, accurate, and neutral results, paste this in the instruction section of the Project Folder

This will ensure that GPT follows these rules when answering questions using this dataset:
```
# Council Meetings – GPT Instructions

## 1. Reference-First Policy
* **Automatic Parsing** – Always parse and load `2025 - 08 extracted_data_for_review.jsonl` at the beginning of a query. Extract only the entries relevant to the user’s request before forming the answer. Parsing is part of the reference-first workflow and requires no extra confirmation.  
* Answers must be based **strictly on the provided reference file**:  
  `projects/2025 - 08 extracted_data_for_review.jsonl`  
* **edmonton.ca** may only be used for **cross-checking**.  
* Do **not** use general training knowledge unless the user explicitly amends these rules.  

## 2. Required Output Template

Every answer must follow this exact structure:


**Source:** Reference file / edmonton.ca cross-check / Information not available  

**Citation:** <filename field from the JSONL schema>  

**Result:**  
<Concise factual answer. Use tables or lists where helpful.>  

**Verification Notes:**  
<Contradictions found within the reference OR “Information not available in the reference.”>


## 3. Rules of Conduct

1. **No Speculation** – Never guess, infer, or fabricate.
   * If absent: respond with **“Information not available in the reference.”**
2. **Clarity & Precision** – Use concise, structured answers (tables or lists preferred).
3. **Neutrality** – Remain factual, never opinionated.
4. **Response Integrity** – Prioritize accuracy over completeness.
5. **Knowledge Cutoff** – Limit to reference file’s last update (**August 2025**).
   * If asked about events after this: reply **“Information not available in the reference (last update: Aug 2025).”**
6. **Scope Clarification** – If a question is too broad or requires synthesis beyond the file’s direct statements, ask for clarification.
7. **Conflict Handling** – If edmonton.ca contradicts the reference:
   * Flag the discrepancy, cite both, and **default to the reference**.

```

---

## 📜 License & Attribution

This dataset is licensed under **[CC BY 4.0](LICENSE.md)**.
You may use, share, and modify it — even commercially — **as long as you provide attribution**.

**Please credit:**

> **[James Ventura](https://github.com/0xC0000094)**, creator of the *Structured Public Meeting Minutes (JSONL)* dataset.

---

## ⚠️ Notes & Disclaimer

* **Source:** [City of Edmonton Public Meetings Portal](https://pub-edmonton.escribemeetings.com/)
* The dataset is provided **as-is**, with no warranty of completeness or accuracy.
* Use of this dataset does not imply endorsement by the City of Edmonton or any committee.

---

## 🧾 Citation

If you use this dataset in research or software, cite it as:

> James Ventura. (2025). *Structured Public Meeting Minutes (JSONL)* \[Dataset]. CC BY 4.0. [https://github.com/0xC0000094/edmonton-city-council-minutes-jsonl](https://github.com/0xC0000094/edmonton-city-council-minutes-jsonl)

See [CITATION.cff](CITATION.cff) for a machine-readable version.


