# Web-Based Speech Training Recorder

A zero-installation, browser-based application for recording speech data for ASR (Automatic Speech Recognition) and TTS (Text-to-Speech) projects. This tool is inspired by the original Python-based recorder from LU Lab, Myanmar, and re-imagines it as a modern, accessible web application.

This application allows users to upload a script, record themselves reading the prompts, and export the collected audio and metadata in a structured format, ready for model training. All processing and storage happens directly in your browser, ensuring privacy and simplicity.

## Features

- **Zero Installation:** Runs entirely in any modern web browser. No need to install Python, libraries, or any other dependencies.
- **Prompt File Upload:** Start a session by simply uploading a `.txt` file containing your recording prompts (one per line).
- **Flexible Prompting Modes:**
  - **Random:** Presents prompts in a random order.
  - **Ordered:** Presents prompts sequentially from the file and stops at the end.
  - **Sequential:** Presents prompts in order and loops back to the beginning.
- **In-Browser Recording:** Uses the browser's `MediaRecorder` API to capture high-quality audio from your microphone.
- **Persistent Sessions:** Automatically saves your progress (recorded files and prompts) in the browser's local storage (`IndexedDB`).
- **Resume Sessions:** If you close the browser and return, you will be prompted to resume your previous session, picking up where you left off.
- **One-Click Export:** Package your entire recording session—all `.wav` audio files and a `recordings.tsv` metadata file—into a single `.zip` archive for easy download.
- **Fully Responsive:** The user interface is designed with Tailwind CSS to be fully functional and easy to use on both desktop and mobile devices.

## How to Use

1.  **Get the File:** Save the application code as a single `recorder.html` file on your computer.
2.  **Open in Browser:** Open the `recorder.html` file in a modern web browser (like Google Chrome, Firefox, or Microsoft Edge).
3.  **Configure Your Session:**
    - In the "1. Configuration" section, click **"Upload Prompt File"** to select your `.txt` script.
    - Choose your preferred **"Prompt Selection Mode"**.
    - Click **"Start Session"**.
4.  **Record Audio:**
    - The first prompt will be displayed.
    - Click **"Start Recording"**. Your browser will ask for microphone permission the first time. **You must click "Allow"**.
    - Read the prompt aloud, then click **"Stop Recording"**.
5.  **Review and Save:**
    - You can click **"Play Last"** to listen to your recording.
    - If you are happy with it, click **"Save"**. The recording will be added to the "Session Files" list, and the application will automatically advance to the next prompt.
6.  **Export Your Dataset:**
    - When you have completed your session, click the **"Export Session (.zip)"** button.
    - A `.zip` file will be generated and downloaded, containing your complete dataset.

## Exported File Structure

The exported `.zip` file is named `tts_session_YYYY-MM-DD.zip` and contains the following structure, which is ideal for feeding into model training pipelines:

tts_session_2025-06-24.zip
│
├── wavs/
│ ├── recording_20250624T093000Z.wav
│ ├── recording_20250624T093015Z.wav
│ └── ... (all other audio files)
│
└── recordings.tsv

The `recordings.tsv` is a tab-separated file that maps each audio file to its corresponding text:

| filename                       | prompt                       | timestamp                | sample_rate | bit_depth |
| ------------------------------ | ---------------------------- | ------------------------ | ----------- | --------- |
| recording_20250624T093000Z.wav | This is the first sentence.  | 2025-06-24T09:30:00.123Z | 48000       | 16        |
| recording_20250624T093015Z.wav | This is the second sentence. | 2025-06-24T09:30:15.456Z | 48000       | 16        |

## Technical Details

- **Frontend:** Built with plain HTML, styled with **Tailwind CSS**, and powered by modern **JavaScript (ESM)**.
- **Audio API:** Uses the standard `MediaRecorder` Web API for recording.
- **Storage:** Leverages `IndexedDB` for robust, persistent client-side storage.
- **Archiving:** Uses the **JSZip** library to create the `.zip` file dynamically in the browser.

---

Created by Htut Ko Ko.
