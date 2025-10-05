# 🎥 Screen Recorder (Web)

A simple, client-side web application for recording your screen, optionally including your microphone and webcam, with features like cursor highlighting and quality selection.

This project is implemented as a single `index.html` file using **vanilla JavaScript** and **Bootstrap 5** for styling, making it highly portable and easy to deploy.

## ✨ Features

* **Screen & Audio Capture:** Records screen activity and system audio (where supported by the browser and user selection via `getDisplayMedia`).
* **Microphone Inclusion:** Optional toggle to include audio from the user's microphone.
* **Webcam Overlay:** Optional webcam feed overlay with:
    * **Draggable Preview:** Reposition the webcam overlay on the screen during recording by dragging the preview window.
    * **Position Presets:** Select from **Bottom Right**, **Bottom Left**, **Top Right**, or **Top Left** positions.
    * **Optional Border:** Toggle a subtle border around the webcam feed.
* **Cursor Highlighting:** Visually highlights mouse clicks and cursor position, which is useful for tutorials or demonstrations.
* **Quality Selection:** Choose between **High (1080p)**, **Medium (720p)**, and **Low (480p)** recording quality.
* **Dark Mode:** Built-in switch for a dark color scheme.
* **Preview & Download:** After stopping, preview the recorded video and download it as a **WebM** file.

## 🚀 How It Works

The application uses modern browser APIs to achieve the recording functionality:

1.  **Screen & Webcam Streams:** It uses `navigator.mediaDevices.getDisplayMedia` to capture the screen and `navigator.mediaDevices.getUserMedia` for the microphone and webcam.
2.  **Composite Canvas:** All visual elements (screen, cursor highlight, and webcam overlay) are drawn onto an HTML `<canvas>` element on a frame-by-frame basis using a drawing loop. This is essential for combining the screen capture with the webcam and effects.
3.  **Recording:** The stream from the composite canvas is captured using `compositeCanvas.captureStream()`. This canvas video stream is then merged with the microphone and system audio tracks to create a final `mixedStream`.
4.  **MediaRecorder:** A `MediaRecorder` is used to encode the `mixedStream` into a **WebM** file format, collecting the data chunks until the user stops the recording.

**Note:** This application is entirely client-side. No data is sent to any external server.

## ⚙️ Setup and Usage

Since the project is a single HTML file, setup is very straightforward:

1.  **Clone the Repository:**
    ```bash
    git clone <your-repo-url>
    cd screen-recorder
    ```
2.  **Open the File:** Simply open the `index.html` file in any modern web browser (Chrome, Firefox, Edge, etc.).

    ```bash
    open index.html # on macOS/Linux
    # or navigate to the file path directly in your browser
    ```
3.  **Start Recording:**
    * Select your desired **Recording Settings** (Mic, Webcam, Cursor Highlight, Quality).
    * Click **"Start Recording"**.
    * You will be prompted by your browser to choose which screen, window, or tab to share. **For best results, choose "This window" or "Application window" when prompted.**
    * The browser will handle permissions for the screen, microphone, and webcam.
4.  **Stop & Save:**
    * Use the **Pause** or **Stop** buttons at the bottom of the screen.
    * After stopping, a **Preview & Save** card will appear, allowing you to view the recording and click **Download** to save the `.webm` file.

## ⚠️ Known Limitations

* **Cursor Tracking:** The cursor highlight and click effect rely on mouse events within the browser page. If you choose to record an external application, the cursor highlight will only track the mouse when it's over the browser window where the recorder is running.
* **System Audio:** Capturing system/tab audio is highly dependent on the browser and the user's selection in the `getDisplayMedia` prompt. Not all combinations of browser and operating system support system audio capture.