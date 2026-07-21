# Matiks-Math-Duels-Solver

# 🧩 Matiks Solver V1.0

> An intelligent Chrome Extension designed as a helper and automated solver tool for the Matiks web application.

An extention which can solve 75+ Arithmetic Questions in Matiks Duel in just 60 seconds without any External API
---

## 🚀 About the Extension
**Matiks Solver V1.0** is a browser extension built to assist users interacting with the Matiks web app. It automates problem-solving workflows, extracts on-screen data seamlessly using advanced OCR (Optical Character Recognition), and provides real-time solutions directly within the web interface.

---

## 🛠️ Tech Stack & Technologies Used
* **JavaScript (ES6+)**: Core extension logic, background scripts, and DOM manipulation.
* **HTML5 / CSS3**: User interface design for the extension popup (`popup.html`, `popup.css`).
* **Chrome Extensions Manifest V3**: Utilizing modern extension APIs (`background.js`, `content.js`).
* **Tesseract.js / OCR Engine**: For extracting text and math symbols from web elements and images (`ocr.js`, `tessdata/eng.traineddata.gz`).
* **Offscreen API**: Handling heavy tasks like OCR processing smoothly in the background (`offscreen.html`).

---

## 🧠 Algorithms & Core Logic
* **DOM Content Scraping (`content.js`)**: Safely injects scripts into the target Matiks web page to read question data, states, and user inputs dynamically without breaking the UI layout.
* **OCR Text Preprocessing Pipeline (`ocr.js`)**: 
  * Captures specific regions of interest (ROI) from the web app.
  * Cleans and normalizes image data (grayscale conversion, thresholding/contrast adjustment) before feeding it into the OCR engine to drastically reduce recognition errors.
* **Problem-Solving Engine (`solver.js`)**: Parses the cleaned textual data, applies deterministic solving algorithms based on the problem type, and computes accurate answers instantly.

---

## 🐛 Bug Fixes & Edge Cases Handled

### 1. Fixing Inaccurate OCR Readings (The OCR Bug)
* **The Issue:** Initially, Tesseract was misinterpreting characters (e.g., confusing numbers like `0` and `O`, `1` and `l`, or misreading mathematical operators due to background noise or anti-aliasing).
* **The Fix:** 
  * Implemented an image-preprocessing step in `ocr.js` that increases contrast and removes visual artifacts before scanning.
  * Added a **Post-Processing Correction Dictionary / Regular Expressions (RegEx)** to automatically correct common OCR typos based on the context of Matiks questions.

### 2. Handling DOM Changes & Asynchronous Loading
* **The Edge Case:** The Matiks web app dynamically loads questions using JavaScript frameworks, meaning elements weren't always present when the extension script first ran.
* **The Fix:** Utilized `MutationObserver` and asynchronous polling in `content.js` to wait for elements to render completely before triggering data extraction.

### 3. Offscreen Canvas Performance
* **The Edge Case:** Running heavy image processing and OCR directly in the popup or content script caused UI freezing and performance lags.
* **The Fix:** Offloaded heavy lifting tasks to Chrome's **Offscreen Documents API (`offscreen.html`)**, ensuring a smooth, non-blocking user experience.
 
