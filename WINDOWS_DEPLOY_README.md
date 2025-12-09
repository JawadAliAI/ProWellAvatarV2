# Digital Human Avatar - Windows Deployment Guide

This guide details how to deploy the Digital Human Avatar application on a Windows Server or Local Machine.

## 📋 1. Prerequisites (One-Time Setup)

Before running the application, ensure the following software is installed on your Windows Server:

1.  **Node.js (LTS Version)**
    *   Download: [https://nodejs.org/](https://nodejs.org/)
    *   *Verify*: Open Command Prompt (`cmd`) and type `node -v`.

2.  **Python (Version 3.10 or newer)**
    *   Download: [https://www.python.org/downloads/](https://www.python.org/downloads/)
    *   **IMPORTANT**: During installation, assume check **"Add Python to PATH"**.
    *   *Verify*: Type `python --version` in `cmd`.

3.  **FFmpeg (Required for Audio Processing)**
    *   Download: [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html) (Get a Windows build, e.g., from Gyan.dev).
    *   Action: Extract the downloaded zip. Copy the path to the `bin` folder (e.g., `C:\ffmpeg\bin`) and add it to your System Environment Variables -> Path.
    *   *Verify*: Type `ffmpeg -version` in `cmd`.

---

## ⚙️ 2. Configuration (Credentials)

The application uses sensitive credentials (like Firebase keys) which are stored in `.env` files. **You must set these up before running.**

### Backend Configuration
1.  Navigate to `apps\backend`.
2.  Open the `.env` file (create it if it doesn't exist).
3.  Add/Verify the following content:

```ini
# Port for the server
PORT=3000

# URL for the AI Doctor Brain (External API)
CUSTOM_API_URL=https://prowellchatdoc.onrender.com
```

### Frontend Configuration
1.  Navigate to `apps\frontend`.
2.  Open the `.env` file (create it if it doesn't exist).
3.  Add your Firebase Credentials:

```ini
# Backend Connection
VITE_BACKEND_URL=http://localhost:3000

# Firebase Config (Replace with your actual keys if they change)
VITE_FIREBASE_API_KEY=AIzaSyDJFU-lqh-WBZAd6HvOqNTnz_3hF_AEBNQ
VITE_FIREBASE_AUTH_DOMAIN=prowell-21a58.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=prowell-21a58
VITE_FIREBASE_STORAGE_BUCKET=prowell-21a58.firebasestorage.app
VITE_FIREBASE_MESSAGING_SENDER_ID=522998581596
VITE_FIREBASE_APP_ID=1:522998581596:web:1f65cd22d1f27314b65999
VITE_FIREBASE_MEASUREMENT_ID=G-2B5FZHGMX0
```

---

## 🚀 3. How to Run (Deployment)

We have provided a "One-Click" script to handle installation, building, and running.

1.  Open the root folder `DocAva`.
2.  Double-click **`run_windows_server.bat`**.
3.  The script will automatically:
    *   Install Node.js dependencies for Backend & Frontend.
    *   Install Python dependencies (`requirements.txt`).
    *   Build the Frontend website (compiling it to static `dist` files).
    *   Start the Main Server.

**Access the App**: Open your browser (Chrome/Edge recommended) and go to:
👉 **http://localhost:3000**

---

## 🧹 4. Maintenance & Reset

If you need to reinstall everything from scratch (e.g., if you changed a library or things are acting up):

1.  Right-click `clean_project.ps1` and select "Run with PowerShell".
    *   *This deletes all `node_modules`, temporary files, and builds.*
2.  Run `run_windows_server.bat` again to get a fresh start.

---

## 🛠️ 5. Troubleshooting

### "TTS Error" or Audio Issues
*   The system uses **Microsoft Edge TTS** for high-quality voice.
*   If your server blocks the connection to Microsoft, it automatically falls back to **Google TTS** (gTTS).
*   If *that* fails (no internet), it falls back to **Windows System Voice** (pyttsx3).
*   *Fix*: Ensure the server has internet access.

### "Internal Server Error" (500)
*   Check the console window created by the script. It will show the exact error.
*   Common causes: Missing Python packages or Bad API URL.

### "Firebase Error"
*   Check `apps\frontend\.env` and ensure the API Key is correct.
*   Check the browser console (F12) for specific Firebase permission errors.
