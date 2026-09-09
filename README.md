# 🌍 AR-MULTI++ Web

AI-powered multilingual OCR, translation, text-to-speech, and AR-style image overlay web application.

Upload an image containing text, automatically extract the text using Google Cloud Vision, translate it into your selected language, generate translated speech, and display the translated text directly over the original image.

---

## ✨ Features

- 📷 Upload images containing text
- 🔍 OCR using Google Cloud Vision API
- 🌐 Automatic source-language detection
- 🔤 Extract text from real-world images
- 📦 Word-level text bounding boxes
- 🌍 Translate text into 13+ languages
- 🔊 Generate translated speech using gTTS
- 🎨 AR-style translated text overlay
- 🖼️ Display original and translated images
- 📊 Display OCR confidence information
- 💻 Modern responsive web interface
- ⚡ Full-stack REST API architecture
- 🛡️ Image type and file-size validation

---

## 🌐 Supported Languages

| Language | Code |
|----------|------|
| 🇬🇧 English | `en` |
| 🇪🇸 Spanish | `es` |
| 🇫🇷 French | `fr` |
| 🇩🇪 German | `de` |
| 🇮🇹 Italian | `it` |
| 🇵🇹 Portuguese | `pt` |
| 🇷🇺 Russian | `ru` |
| 🇯🇵 Japanese | `ja` |
| 🇰🇷 Korean | `ko` |
| 🇨🇳 Chinese | `zh` |
| 🇸🇦 Arabic | `ar` |
| 🇮🇳 Hindi | `hi` |
| 🇮🇳 Telugu | `te` |

---

## 🔄 How It Works

```text
📷 Upload Image
       ↓
🔍 OCR Processing
       ↓
📝 Extract Text
       ↓
🌐 Detect Source Language
       ↓
🔤 Translate Text
       ↓
🔊 Generate Speech
       ↓
🎨 Create AR-Style Overlay
       ↓
📊 Display Results
```

---

## 📸 Example

```text
Input Image
     ↓
┌──────────────────────┐
│   Hello World        │
│   Welcome            │
└──────────────────────┘
     ↓
Select Language
     ↓
Spanish
     ↓
┌──────────────────────┐
│   Hola Mundo         │
│   Bienvenido         │
└──────────────────────┘
     ↓
🔊 Spanish Audio
```

---

## 🏗️ Architecture

```text
                ┌─────────────────┐
                │      User       │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Next.js Frontend│
                │ React + TypeScript
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Express Backend │
                │    REST API     │
                └────────┬────────┘
                         │
             ┌───────────┼───────────┐
             │           │           │
             ▼           ▼           ▼
        ┌────────┐ ┌────────────┐ ┌────────┐
        │  OCR   │ │ Translation│ │  TTS   │
        │ Vision │ │   Service   │ │ gTTS   │
        └────┬───┘ └─────┬──────┘ └───┬────┘
             │            │             │
             └────────────┼─────────────┘
                          ▼
                  ┌───────────────┐
                  │ Image Overlay │
                  │     Jimp      │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │    Results    │
                  └───────────────┘
```

---

## 🚀 Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ar-multi-web.git
cd ar-multi-web
```

### 2. Install Dependencies

Install frontend dependencies:

```bash
npm install
```

If the backend has a separate `package.json`:

```bash
cd backend
npm install
cd ..
```

### 3. Configure Google Cloud Vision

AR-MULTI++ Web uses Google Cloud Vision API for OCR.

Create a Google Cloud service account and download the credentials JSON file.

Set the environment variable.

#### Windows PowerShell

```powershell
$env:GOOGLE_APPLICATION_CREDENTIALS="C:\path\to\service-account.json"
```

#### Windows CMD

```cmd
set GOOGLE_APPLICATION_CREDENTIALS=C:\path\to\service-account.json
```

#### Linux / macOS

```bash
export GOOGLE_APPLICATION_CREDENTIALS="/path/to/service-account.json"
```

### 4. Start the Backend

```bash
cd backend
node server.js
```

Backend:

```text
http://localhost:3001
```

### 5. Start the Frontend

Open another terminal:

```bash
npm run dev
```

Frontend:

```text
http://localhost:3000
```

---

## 🔐 Environment Variables

Example configuration:

```env
GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json
```

⚠️ Never upload your Google Cloud credentials, API keys, `.env` files, or service-account JSON files to GitHub.

Add sensitive files to `.gitignore`:

```gitignore
.env
.env.local
*.json
credentials/
service-account.json
node_modules/
.next/
uploads/
```

---

## 📡 API

### Health Check

```http
GET /health
```

Checks whether the backend server is running.

### Translate Image

```http
POST /api/translate
```

Content type:

```text
multipart/form-data
```

Required fields:

```text
image
targetLanguage
```

Example:

```text
image = sample.jpg
targetLanguage = es
```

Example response:

```json
{
  "success": true,
  "extractedText": "Hello World",
  "translatedText": "Hola Mundo",
  "originalImage": "/uploads/original-image.jpg",
  "overlayImage": "/uploads/translated-image.jpg",
  "audioUrl": "/audio/translated-text.mp3",
  "confidence": 0.98,
  "language": "en"
}
```

---

## 🧩 Main Modules

### 🔍 OCR Service

Uses Google Cloud Vision API to:

- Detect text in images
- Extract recognized text
- Detect source language
- Generate word-level bounding boxes
- Provide OCR confidence information

### 🌐 Translation Service

Uses:

```text
google-translate-api-x
```

The service translates extracted OCR text into the language selected by the user.

Example:

```text
English
   ↓
Spanish
   ↓
Hola Mundo
```

### 🔊 Text-to-Speech Service

Uses:

```text
gTTS
```

The translated text is converted into an MP3 audio file.

The generated audio can be played from the frontend.

### 🎨 Overlay Service

Uses:

```text
Jimp
```

The overlay service places translated text over the corresponding regions of the original image.

It supports:

- OCR bounding-box coordinates
- Dynamic font sizing
- Text positioning
- Semi-transparent backgrounds
- Translated text rendering

This creates an AR-style translation effect.

---

## 📂 Project Structure

```text
AR-MULTI++/
│
├── app/
│   ├── api/
│   │   └── translate/
│   │       └── route.ts
│   │
│   ├── page.tsx
│   ├── layout.tsx
│   └── globals.css
│
├── components/
│   ├── ImageUpload.tsx
│   └── LanguageSelector.tsx
│
├── backend/
│   ├── server.js
│   │
│   └── services/
│       ├── ocrService.js
│       ├── translationService.js
│       ├── ttsService.js
│       └── overlayService.js
│
├── public/
│   └── audio/
│
├── uploads/
│
├── package.json
├── package-lock.json
├── tsconfig.json
├── tailwind.config.js
├── next.config.js
├── .gitignore
└── README.md
```

---

## 🛠️ Tech Stack

### Frontend

- Next.js 14
- React 18
- TypeScript 5.2
- Tailwind CSS 3.3
- Framer Motion
- Lucide React
- React Dropzone
- Axios

### Backend

- Node.js 18+
- Express.js 4.18.2
- Multer 1.4.5
- CORS 2.8.5
- Jimp 0.22.10
- Sharp 0.32.6

### AI / Cloud

- Google Cloud Vision API
- Google Translate
- gTTS

---

## 📊 Processing Pipeline

```text
Image Upload
     ↓
Multer
     ↓
Image Validation
     ↓
Google Cloud Vision
     ↓
OCR Text + Bounding Boxes
     ↓
Language Detection
     ↓
Google Translation
     ↓
Translated Text
     ├───────────────┐
     ↓               ↓
    gTTS            Jimp
     ↓               ↓
MP3 Audio       Image Overlay
     │               │
     └───────┬───────┘
             ↓
        JSON Response
             ↓
         Next.js UI
```

---

## 📋 Output

After processing an image, the application provides:

```text
📝 Extracted Text
🌐 Translated Text
🖼️ Original Image
🎨 Translated Overlay Image
🔊 Translated Audio
📊 OCR Confidence
🌍 Detected Language
```

---

## 📏 Upload Limit

Maximum image size:

```text
10 MB
```

Only image MIME types are accepted.

---

## ⚠️ Notes

- Google Cloud Vision credentials are required.
- Internet connectivity is required for cloud-based OCR and translation.
- Webcam or camera access is not required; the application works with uploaded images.
- OCR accuracy depends on image quality and text visibility.
- Complex, distorted, handwritten, or highly stylized text may produce lower OCR accuracy.
- Overlay quality depends on the accuracy of OCR bounding boxes.
- Telugu currently uses Hindi voice fallback/mapping in the TTS configuration.
- Keep all API credentials and service-account files private.

---

## 🎯 Applications

AR-MULTI++ Web can be used for:

- 🌍 Travel and tourism
- 🍽️ Restaurant menu translation
- 🏪 Product label translation
- 🚉 Transportation signs
- 🛣️ Road signs
- 📚 Educational materials
- 📄 Document translation
- 🛍️ Shopping
- 🗺️ Location information
- 🌐 Multilingual communication

---

## 💡 Future Enhancements

- 📱 Android and iOS application
- 📷 Real-time camera translation
- 🥽 Real-time AR translation
- 🎥 Video text translation
- ✍️ Handwritten text recognition
- 🔊 Improved multilingual TTS
- 🇮🇳 Native Telugu TTS support
- 📄 Document and PDF translation
- 📦 Batch image translation
- 💾 Translation history
- 👤 User accounts
- ⬇️ Download translated documents
- 🌐 Additional language support
- ⚡ Offline OCR support

---

## 🏆 Resume Highlights

```text
AR-MULTI++ Web | Next.js, React, Node.js, Express.js,
Google Cloud Vision, Translation, TTS

• Built a full-stack multilingual OCR and translation platform
  that extracts text from images and translates it into 13+
  target languages.

• Integrated Google Cloud Vision API for OCR, language
  detection, confidence scoring, and word-level bounding boxes.

• Implemented multilingual translation and text-to-speech
  generation for translated text and audio output.

• Developed an AR-style image overlay pipeline using Jimp
  to position translated text over detected regions.

• Designed a responsive Next.js/React frontend with a
  Node.js/Express REST API backend.
```

---

## 📚 Skills Demonstrated

```text
JavaScript
TypeScript
React
Next.js
Node.js
Express.js
REST APIs
Google Cloud Vision API
OCR
Machine Translation
Text-to-Speech
Image Processing
Jimp
Sharp
Tailwind CSS
Framer Motion
API Integration
Full-Stack Development
Cloud Services
Git
GitHub
```

---

## 📌 Project Information

| Category | Details |
|----------|---------|
| Project Name | AR-MULTI++ Web |
| Project Type | Full-Stack Web Application |
| Domain | AI / OCR / Translation |
| Frontend | Next.js + React + TypeScript |
| Backend | Node.js + Express.js |
| OCR | Google Cloud Vision API |
| Translation | Google Translate |
| TTS | gTTS |
| Image Processing | Jimp + Sharp |
| Languages | 13+ |
| Maximum Upload | 10 MB |
| Frontend Port | 3000 |
| Backend Port | 3001 |

---

## 🤝 Contributions

Contributions, suggestions, and improvements are welcome.

Feel free to fork the repository, create a new branch, and submit a pull request.

```bash
git checkout -b feature/new-feature
git add .
git commit -m "Add new feature"
git push origin feature/new-feature
```

---

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.

---

## 📜 License

This project is intended for educational, portfolio, and demonstration purposes.
