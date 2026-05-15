# Neural Animation Pipeline — Full Setup Guide

This project is a browser-based talking-head avatar app. The main application runs as a static website from `index.html`, so there is no build step and no package installation required for the core app. A separate optional module, `Talking-module/`, can run a local Talking-module server if you want local neural text-to-speech experiments.

## 1. What you need

### Required for the main app

- A modern web browser with WebGL support
  - Chrome or Edge are the safest choices
- Python 3 **or** Node.js, only to run a local web server
- Internet access for external libraries, avatar assets, and cloud AI providers

### Optional

- A provider API key if you want AI chat responses from Groq, Gemini, OpenAI, Grok, Google TTS, Microsoft TTS, or ElevenLabs
- Node.js + npm if you want to run the optional local Talking-module server in `Talking-module/`
- Ollama if you want to test the local Ollama-backed AI options exposed in the UI

## 2. Get the project onto your machine

If you are cloning from GitHub:

```bash
git clone <your-repository-url>
cd Neural-Animation-Pipeline
```

If you already have the project locally, move into the project folder:

```bash
cd /path/to/Neural-Animation-Pipeline
```

You should see files such as:

```text
index.html
siteconfig.js
modules/
examples/
Talking-module/
```

## 3. Recommended working-directory setup

Open a terminal in the project root—the folder that contains `index.html`.

Example for this local workspace:

```bash
cd /Users/aaryaplakkat/Documents/Internship/Ai-in-animation/Neural-Animation-Pipeline
```

Confirm you are in the right place:

```bash
pwd
ls
```

Expected important files/folders:

```text
index.html
README.md
SETUP_GUIDE.md
modules
avatars
examples
Talking-module
```

## 4. Run the main application

Do **not** open `index.html` by double-clicking it. Browser module imports work more reliably through a local HTTP server.

### Option A — run with Python 3

From the project root:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/index.html
```

### Option B — run with Node.js

If you prefer Node:

```bash
npx http-server -p 8000
```

Then open:

```text
http://localhost:8000/index.html
```

To stop either server later, return to the terminal and press:

```text
Ctrl + C
```

## 5. First-run configuration inside the app

1. Open `http://localhost:8000/index.html`.
2. Wait for the avatar to load.
3. Open the Settings panel.
4. In **Voice**, keep **Native** selected if you want browser speech synthesis with no voice API key.
5. In **AI**, choose the provider/model you want:
   - Groq models are available in the UI
   - Gemini models are available in the UI
   - Other provider paths are also present in the code
6. In **API Keys**, paste the matching key for the provider you selected.

Important: API keys are entered in the browser UI at runtime. Do **not** hardcode them into `index.html`, commit them to Git, or paste them into public screenshots.

## 6. Quick smoke test

After the page loads:

1. Set **Voice Type** to `Native`.
2. Use the native voice test button in Settings to confirm browser speech works.
3. Select an AI model.
4. Add the matching API key if the provider requires one.
5. Send a short message such as:

```text
Tell me a short joke.
```

Expected result:

```text
message sent
   -> AI response returned
   -> response appears in chat
   -> avatar speaks
   -> lipsync animation plays
```

## 7. Optional: run the local Talking-module server

The folder `Talking-module/` is a separate Node.js package for Talking-module. Use this only if you want to experiment with local neural TTS rather than the main app's native browser voice path.

From the project root:

```bash
cd Talking-module
npm install
npm start
```

By default, the Talking-module server is configured from:

```text
Talking-module/talking-module-node.json
```

and listens on port `8882`.

To open the included Talking-module demo while the main static server is running, visit:

```text
http://localhost:8000/Talking-module/index.html
```

To stop the Talking-module server:

```text
Ctrl + C
```

Then return to the main project root if needed:

```bash
cd ..
```

## 8. Optional: run examples

With the local static server still running, you can open:

```text
http://localhost:8000/examples/minimal.html
http://localhost:8000/examples/mp3.html
http://localhost:8000/examples/azure-blendshapes.html
http://localhost:8000/examples/azure-audio-streaming.html
```

Notes:

- `examples/mp3.html` contains an OpenAI placeholder and requires your own runtime API key if you use that workflow.
- The Azure examples require Azure credentials entered in the browser UI.

## 9. Optional: local Ollama path

The main app contains Ollama-backed model options that call:

```text
http://localhost:11434/api/chat
```

If you want to use those options, install and run Ollama separately, then make sure the desired model is available locally before selecting an Ollama option in the app.

## 10. Suggested development workflow

From the project root:

```bash
# 1. Start the static site
python3 -m http.server 8000

# 2. Open the app in your browser
# http://localhost:8000/index.html

# 3. Edit files, save, refresh browser
```

Useful files:

```text
index.html              main app UI and behavior
siteconfig.js           preset avatars, voices, scenes, gestures
modules/                talking-head engine modules
examples/               standalone demos
Talking-module/         optional Talking-module package/server
```

## 11. Troubleshooting

### The page opens but assets do not load

- Make sure you started a local HTTP server from the project root.
- Make sure you opened `http://localhost:8000/index.html`, not a `file://` URL.

### The avatar loads but does not speak

- Use **Native** voice first.
- Confirm your browser allows audio playback.
- Use the native voice test button in Settings.
- Check the browser console for errors.

### AI responses do not appear

- Make sure the selected AI provider matches the API key you entered.
- Re-check the key for typos or expiration.
- Confirm you have internet access.
- Open the browser console and inspect the network/API error.

### Talking-module does not start

From `Talking-module/`, run:

```bash
npm install
npm start
```

If port `8882` is already in use, either stop the conflicting process or change the port in `Talking-module/talking-module-node.json`.

## 12. Security checklist before pushing to Git

Before every push:

```bash
# From the project root
rg -n "(gsk_[A-Za-z0-9]{20,}|AIza[0-9A-Za-z_-]{20,}|sk-[A-Za-z0-9_-]{20,}|xai-[A-Za-z0-9_-]{20,}|AKIA[0-9A-Z]{16}|BEGIN .*PRIVATE KEY)" . -g '!Talking-module/node_modules/**' -g '!SETUP_GUIDE.md'
```

Also verify:

- no real API keys are hardcoded in HTML or JS
- no `.env` files are committed
- no credential JSON, PEM, or private-key files are committed
- `.gitignore` is present and active

A secret entered into a masked textbox is still public if it exists in source code. Runtime entry is safe; committed source secrets are not.

## 13. Minimal command summary

For the main app only:

```bash
cd /path/to/Neural-Animation-Pipeline
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/index.html
```

For the optional Talking-module server:

```bash
cd /path/to/Neural-Animation-Pipeline/Talking-module
npm install
npm start
```
