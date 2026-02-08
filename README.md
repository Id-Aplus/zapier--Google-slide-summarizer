# zapier--Google-slide-summarizer
Automated Google Slides summarizer using Zapier and OpenAI (GPT-4). Features a custom extraction algorithm to handle slide text visibility issues and hallucinations, while on the Free Tier.
Zapier AI Slide Summarizer 

An automated pipeline that reads Google Slides and emails summaries using GPT-4, engineered to run entirely on the Zapier Free Tier.
![Zapier Workflow](https://github.com/user-attachments/assets/b387d26a-0d93-4f6e-a8da-1425bf8ceff1)

Overview

Standard AI automations often hallucinate when reading Google Slides because they process file metadata rather than the actual text. This workflow solves that by combining:

Custom text extraction that scrapes slide elements directly, including text-on-image layers

Strict prompt engineering that forces AI to report insufficient data rather than guessing

The system ensures AI summaries are accurate, reliable, and honest.

Key Features

Dynamic trigger on any new file added to the target Google Drive folder

Custom extraction of slide text elements, bypassing PDF export limitations

Hallucination guardrails: AI outputs “TEXT DOES NOT CONTAIN ENOUGH INFORMATION” if data is missing

Runs entirely on Zapier Free Tier, no paid OCR or external tools required

Tech Stack

Workflow Engine: Zapier (Free Tier)

Intelligence: OpenAI GPT-4 via Zapier integration

Storage: Google Drive

Notification: Gmail

Architecture

Trigger: A new file is dropped into the ZAPIER folder in Google Drive

Extract: Custom Action scrapes raw text elements from slides (handles text-on-image layers)

Analyze: GPT-4 processes the text with a safety-first prompt

Decide:

If text is valid: GPT-4 generates a bullet-point summary

If text is missing: GPT-4 outputs the error message “TEXT DOES NOT CONTAIN ENOUGH INFORMATION”

Notify: Gmail emails the final result (summary or error report)

Problem: Sending PDF/Slide files directly to AI resulted in hallucinations because AI only received file metadata.

Fix: Feed AI raw text strings via a Custom Action instead of binary files.

Safety Valve: The system prompt includes a “kill switch” to prevent hallucination:

"IF YOU VIEW A TEXT FROM A SLIDE AND IT DOESNT CONTAIN USEFUL INFORMATION, SAY 'TEXT DOES NOT CONTAIN ENOUGH INFORMATION'... SAY THIS INSTEAD OF HALLUCINATING."

Setup Instructions

Connect Google Drive, OpenAI, and Gmail to Zapier

Create a folder named ZAPIER in Google Drive

Replicate the 4-step workflow as shown in the architecture

Configure the Custom Action to extract all text elements, including text-on-image layers

Test with both text-containing slides and image-only slides to verify guardrails

Lessons Learned

AI hallucinations occur when it only receives metadata; feeding raw text prevents this

Custom extraction ensures all visible text elements are captured

Strict prompts and safety rules convert potential hallucinations into diagnostic messages

Automation reliability requires acknowledging platform limitations; honest failures are preferable to false summaries
