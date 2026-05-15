# Neural-Animation-Pipeline

Real-time speech-driven facial animation using neural TTS and modular processing.

## Overview

Neural Animation Pipeline is a browser-based system for building interactive 3D talking-head avatars. It converts textual or spoken input into synchronized avatar output by combining text-to-speech, phoneme and viseme generation, facial animation, body motion, and real-time rendering in one modular pipeline.

The project exists to solve a core limitation of conventional speech systems: speech synthesis can generate audio, but it does not by itself create believable visual speech. For an animated avatar to appear natural, the system must coordinate voice output with mouth shapes, facial expressions, eye movement, gestures, and scene rendering at runtime.

This project unifies those normally separate layers into a single extensible architecture, making it suitable for virtual assistants, educational agents, conversational interfaces, and real-time digital human applications.

## Key Features

- Real-time text-to-speech and speech-driven animation
- Modular architecture for animation pipelines
- Multi-language dictionary and lip-sync support
- Viseme-based facial synchronization with speech output
- Low-latency audio streaming for interactive systems
- 3D avatar rendering with pose, gesture, and mood control
- Physics-based secondary motion through dynamic bones
- Support for multiple AI and TTS providers
- Scalable and extensible module design
- Optional local neural TTS subsystem using browser or Node.js execution

## System Architecture

The pipeline consists of the following components:

1. **Input Processing** – Accepts typed text, microphone input, uploaded audio, or scripted dialogue.
2. **AI / Dialogue Layer** – Optionally generates conversational responses through supported AI providers.
3. **TTS Engine** – Converts text into speech using browser-native, cloud-based, or local neural TTS engines.
4. **Phoneme / Viseme Mapping** – Aligns speech with visemes for lip-sync animation.
5. **Animation Module** – Generates facial animation, eye movement, gestures, poses, and secondary motion.
6. **Output Renderer** – Displays the final synchronized 3D avatar animation in real time.

```text
User Input
   ↓
Input Processing
   ↓
AI / Dialogue Layer (optional)
   ↓
TTS Engine
   ↓
Phoneme / Viseme Mapping
   ↓
Animation Module
   ↓
Output Renderer
```

## Tech Stack

- JavaScript with ES Modules
- Node.js for the optional local neural TTS server
- HTML5, CSS3, and browser Web APIs
- Three.js and WebGL for real-time 3D rendering
- Web Audio API and AudioWorklet for playback, mixing, and streaming
- Browser-native speech synthesis plus external TTS providers
- Kokoro ONNX and `transformers.js` for optional local neural TTS
- JSON-based configuration for avatars, voices, presets, and server settings
- GLB and FBX assets for avatar models, poses, and animations
- Blender Python scripts for avatar preprocessing and blendshape normalization
