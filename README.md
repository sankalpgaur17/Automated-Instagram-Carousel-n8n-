# 🚀 Self-Built Instagram Carousel Automation – No Third-Party Tools!

Welcome to my fully **custom-built, cost-efficient, and highly accurate** Instagram automation system — designed using [n8n](https://n8n.io/) and OpenAI APIs.

This repository contains the exported `.json` of the automation workflow that:
- Extracts content topics from Google Sheets
- Generates slide-wise headings and subheadings
- Creates stunning AI-generated images (portrait format)
- Adds text overlays on those images (with correct alignment and formatting)
- Crafts engaging, platform-aware captions using OpenAI
- Publishes them to **Instagram** and optionally to **Facebook**
- Automatically marks the content as "done" to avoid duplication

---

## 📂 Files Included

- `carousal posting.json` – Main automation workflow
- `README.md` – You're here :)

---

## 🔁 Workflow Flow Overview

This is the step-by-step breakdown of what happens inside the automation:

### 1. 🧾 **Topic Input from Google Sheets**
- Connects to your Google Sheet
- Filters for rows where `status != ✅`
- Picks the next available topic for that day

### 2. 🧠 **Slide Breakdown & Text Structuring**
- Uses subheadings array
- Dynamically assigns `subheading1`, `subheading2`, etc.
- Applies fallback values (`''`) if fewer subheadings exist
- Handles errors when fields are missing

### 3. 🎨 **Image Generation via OpenAI**
- Uses DALL·E 3 API to create **portrait** images (`1024x1280`)
- Image style, camera angle, lighting, and props are **prompt-driven**
- Avoids abstract/cartoon images by system prompt

### 4. 🖋️ **Text Overlay on Images**
- n8n Edit Image node adds `heading` and `subheadings` on images
- Dynamic font sizing and positioning
- Centers or aligns text based on availability

### 5. ☁️ **Cloud Upload (e.g., Cloudinary)**
- Uploads processed images and returns `secure_url`
- Clean and consistent URL format used for publishing

### 6. 📝 **Caption Generation (OpenAI HTTP Node)**
- Custom system prompt to generate captions using:
  - Ayurveda themes
  - Health context
  - Related hashtags and emojis
- JSON output extracted and formatted into array

### 7. 📤 **Publishing to Instagram**
- Uses Instagram Graph API (via Facebook)
- Posts images as a carousel
- Automatically publishes container with all media items

### 8. 📣 **Optional: Post to Facebook**
- Uses `page_id` and access token for Facebook Graph API
- Posts same carousel or summary post (via subworkflow)

### 9. ✅ **Update Google Sheet**
- Marks the topic row as `✅`
- Ensures the same content isn’t used again

### 10. 🔁 **Scheduled Execution**
- Triggered daily at 4 PM using n8n Cron node
- Skips execution if all rows are marked `✅`

---

## 🛠️ Setup Instructions

1. **Import JSON Workflow:**
   - Open your self-hosted n8n instance.
   - Click “Import Workflow” and upload `carousal posting.json`.

2. **Set Up Google Sheet Integration:**
   - Add your credentials via Google API.
   - Point the node to your content sheet.

3. **Set Your API Keys:**
   - OpenAI API Key (used in HTTP node for captions & DALL·E)
   - Facebook Page Access Token (for publishing)

4. **Update Constants:**
   - Your `page_id`, `Instagram Business ID`, and image host URLs (Cloudinary or similar)

5. **Customize Prompts (Optional):**
   - Update prompt templates for better control on tone, format, or language.

---

## 🧠 No Third-Party Tools Used

- ❌ No Canva  
- ❌ No Zapier / Make  
- ❌ No pre-made templates  
- ✅ Fully self-designed  
- ✅ Self-hosted on AWS (`t3.small` instance)
- ✅ Debugged, optimized, and structured by me from scratch

---

## 📌 Requirements

- n8n `v1.104.2+`
- OpenAI API access (DALL·E 3 + GPT)
- Google Sheets access
- Facebook Developer App (for Instagram Graph API)

---

## 🙌 Credits

Built as part of my internship project — from scratch, solo, and fully custom. Proud to say: **no third-party fluff, just engineering.**

---

## 📬 Feedback / Help?

Feel free to open an [Issue](https://github.com/) or connect with me on [LinkedIn](https://www.linkedin.com/).

---

