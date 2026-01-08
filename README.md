
# 🎙️ OpenWhisper

> **The delightful, always-on-top AI dictation widget for Windows.** > Powered by Groq & Whisper-v3-Turbo for lightning-fast, privacy-focused voice typing.

![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Stack](https://img.shields.io/badge/built%20with-Neutralinojs-orange?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Windows-0078D6?style=flat-square&logo=windows&logoColor=white)

---

## 🧐 What is OpenWhisper?

**OpenWhisper** is a minimalist, open-source alternative to commercial dictation apps like Wispr Flow. It sits quietly on your screen as a tiny (140px) floating pill and allows you to type with your voice into **any application** using the state-of-the-art **Whisper-Large-V3-Turbo** model.

It is built for power users who want:
* **Speed:** Sub-second transcription via Groq Cloud.
* **Privacy:** You bring your own API key. No audio is stored on our servers.
* **Minimalism:** No bulky windows. Just a tiny, delightful UI that stays out of your way.

---

## ✨ Features

* **🎈 Ultra-Compact UI:** A tiny `140x35px` borderless widget that floats always-on-top.
* **⚡ Groq Integration:** Uses `whisper-large-v3-turbo` for near-instant speech-to-text.
* **🧠 Smart Insertion:** Record, click into *any* input field (Notepad, Slack, Chrome), and hit **Insert** to auto-type your text.
* **🎨 Delightful UX:**
    * Reactive "Neon Red" glow when recording.
    * Live timer with millisecond precision.
    * Dark mode design inspired by Windows 11 aesthetics.
* **🔐 Private & Secure:** Your API Key is stored locally. The app is fully open-source.

---

## 🚀 Getting Started

### 1. Prerequisites
You need a **Groq API Key**.
* Go to [Groq Console](https://console.groq.com/keys).
* Create a free API key.

### 2. Installation (For Users)
* Download the latest `.zip` from the [Releases](https://github.com/weroperking/OpenWhisper/releases) page.
* Extract and run `OpenWhisper.exe`.
* Click the small **Key Icon (🔑)** on the widget and paste your Groq API Key.

---

## 🛠️ Development & Build

OpenWhisper is built on **Neutralinojs**, a lightweight alternative to Electron.

### Stack
* **Framework:** [Neutralinojs](https://neutralino.js.org/) (Native HTML/JS/CSS)
* **Logic:** Vanilla JavaScript (ES6+)
* **Styling:** CSS3 (Flexbox, Glassmorphism)
* **Automation:** Windows PowerShell (for clipboard injection)

### Setup
```bash
# 1. Install Neutralino CLI globally
npm install -g @neutralinojs/neu

# 2. Clone the repository
git clone [https://github.com/weroperking/OpenWhisper.git](https://github.com/weroperking/OpenWhisper.git)
cd OpenWhisper

# 3. Install dependencies
neu update

# 4. Run in dev mode
neu run

```

### Build for Release

To create a standalone `.exe`:

```bash
neu build --release

```

The output will be in the `/dist` folder.

---

## 🧩 How "Smart Insert" Works

Since web-based desktop apps cannot easily type into other applications for security reasons, OpenWhisper uses a clever native bridge:

1. User clicks **Insert**.
2. OpenWhisper briefly **hides itself** to return focus to your previous window.
3. It executes a background PowerShell command to set the **System Clipboard**.
4. It simulates a `Ctrl + V` keystroke to paste the text instantly.
5. OpenWhisper reappears.

---

## 🗺️ Roadmap

* [ ] **Global Hotkey:** Start recording with `Alt + Space`.
* [ ] **System Tray Support:** Hide completely when not in use.
* [ ] **Local Model Support:** Option to use local Whisper for offline use.

---

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

<p align="center">
Made with ❤️ and ☕ by <a href="https://github.com/weroperking">Weroperking</a>
</p>

```

```