# 🚫 Zapier AI Slide Summarizer (Hallucination-Proof)

**An automated pipeline that reads Google Slides and emails summaries using GPT-4, engineered to run entirely on the Zapier Free Tier.**

<img src="https://github.com/user-attachments/assets/b387d26a-0d93-4f6e-a8da-1425bf8ceff1" alt="Zapier Workflow" width="800">

## 💡 Overview
Standard AI automations often "hallucinate" when reading Google Slides because they process file metadata instead of actual text. This workflow solves that by combining:

* **Custom text extraction** that scrapes slide elements directly (including text-on-image layers).
* **Strict prompt engineering** that forces AI to report insufficient data rather than guessing.

The result? A system that ensures AI summaries are accurate, reliable, and honest.

## 🚀 Key Features
* **Dynamic Trigger:** Runs automatically on any new file added to the target Google Drive folder.
* **Custom Extraction:** Scrapes text elements directly, bypassing PDF export limitations.
* **Hallucination Guardrails:** AI outputs `TEXT DOES NOT CONTAIN ENOUGH INFORMATION` if data is missing.
* **Cost Engineered:** Runs entirely on the **Zapier Free Tier** (no paid OCR or external tools required).

## 🛠️ Tech Stack
* **Workflow Engine:** Zapier (Free Tier)
* **Intelligence:** OpenAI GPT-4 (via Zapier integration)
* **Storage:** Google Drive
* **Notification:** Gmail

## ⚙️ Architecture & Logic
1.  **Trigger:** A new file is dropped into the `ZAPIER` folder in Google Drive.
2.  **Extract:** A Custom Action scrapes raw text elements from slides (handles text-on-image layers).
3.  **Analyze:** GPT-4 processes the text with a "Safety-First" prompt.
4.  **Decide:**
    * *If text is valid:* GPT-4 generates a bullet-point summary.
    * *If text is missing:* GPT-4 outputs the error message.
5.  **Notify:** Gmail emails the final result (Summary or Error Report).

## 🐛 Debugging Case Study: The "Invisible Text" Bug
**The Problem:** Sending PDF/Slide files directly to the AI resulted in hallucinations because the AI only received file metadata (filename, size), not the content.

**The Fix:** We engineered a Custom Action to feed the AI **raw text strings** instead of binary files.

**The Safety Valve:** The system prompt includes a "Kill Switch" to prevent hallucination:
> "IF YOU VIEW A TEXT FROM A SLIDE AND IT DOESNT CONTAIN USEFUL INFORMATION, SAY 'TEXT DOES NOT CONTAIN ENOUGH INFORMATION'... SAY THIS INSTEAD OF HALLUCINATING."

## 📦 Setup Instructions
1.  Connect Google Drive, OpenAI, and Gmail to Zapier.
2.  Create a folder named `ZAPIER` in Google Drive.
3.  Replicate the 4-step workflow as shown in the architecture diagram.
4.  Configure the Custom Action to extract all text elements.
5.  **Test:** Upload both text-containing slides and image-only slides to verify the guardrails work.

## 🧠 Lessons Learned
* **Metadata vs. Content:** AI hallucinations occur when it only receives metadata; feeding raw text prevents this.
* **Honesty over Confidence:** Strict prompts and safety rules convert potential hallucinations into useful diagnostic messages.
* **Platform Limits:** Automation reliability requires acknowledging platform limitations (like Zapier's file handling); honest failures are preferable to false summaries.
