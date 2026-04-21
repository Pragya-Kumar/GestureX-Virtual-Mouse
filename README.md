<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,30&height=200&section=header&text=GestureX%20🖐️&fontSize=55&fontColor=fff&animation=twinkling&fontAlignY=38&desc=Hand-Gesture%20Controlled%20Virtual%20Mouse&descAlignY=58&descSize=18&descColor=A5D6A7"/>

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=18&pause=1000&color=66BB6A&center=true&vCenter=true&width=700&lines=Control+Your+PC+Without+Touching+the+Mouse+%F0%9F%96%B1%EF%B8%8F;21+Hand+Landmarks+via+MediaPipe+%F0%9F%A4%9A;Click+%7C+Scroll+%7C+Move+%E2%80%94+All+with+Gestures+%E2%9C%8B;Voice+Commands+Built-In+%F0%9F%8E%99%EF%B8%8F;Real-Time+OpenCV+%2B+PyAutoGUI+%F0%9F%8E%AF)](https://git.io/typing-svg)

<br/>

[![Python](https://img.shields.io/badge/Python-3.8-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Google-FF6F00?style=for-the-badge&logo=google&logoColor=white)](https://mediapipe.dev)
[![OpenCV](https://img.shields.io/badge/OpenCV-Real--Time-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org)
[![PyAutoGUI](https://img.shields.io/badge/PyAutoGUI-Mouse%20Control-4CAF50?style=for-the-badge)](https://pyautogui.readthedocs.io)
[![SpeechRecognition](https://img.shields.io/badge/SpeechRecognition-Voice%20Commands-F44336?style=for-the-badge)](https://pypi.org/project/SpeechRecognition)

> *Control your computer with just your hand — no mouse required* 🖐️

</div>

---

## 📋 Table of Contents

<div align="center">

| | | |
|:---:|:---:|:---:|
| [✨ Features](#-features) | [🔄 System Flow](#-system-flow) | [🤚 Gesture Map](#-gesture-map) |
| [🦾 How It Works](#-how-it-works) | [📐 MediaPipe Landmarks](#-mediapipe-hand-landmarks) | [🛠️ Tech Stack](#%EF%B8%8F-tech-stack) |
| [📁 Project Structure](#-project-structure) | [🚀 Installation](#-installation) | [⚠️ Important Note](#%EF%B8%8F-important-note) |
| [👥 Collaborators](#-collaborators) | | |

</div>

---

## ✨ Features

<div align="center">

| Category | Gesture | Action |
|:---:|:---:|:---|
| 🖱️ **Cursor** | Index + Middle up | Move cursor smoothly |
| 🧊 **Freeze** | Thumb out | Stop cursor movement |
| 👆 **Left Click** | Index finger folded | Left mouse click |
| 👉 **Right Click** | Middle finger folded | Right mouse click |
| 👆👆 **Double Click** | No gap between Index & Middle | Double click |
| 📜 **Scroll** | Only thumb out + move hand | Scroll up / down |
| 🎙️ **Voice** | Say "Keyboard" or "Calculator" | Open system apps |

</div>

---

## 🔄 System Flow

```mermaid
flowchart TD
    A([📷 Webcam Feed]):::input
    B[🖐️ MediaPipe\nHand Detection]:::mediapipe
    C[📍 21 Landmark\nExtraction]:::mediapipe

    C --> D{🧠 Gesture\nClassifier}:::decision

    D --> E[☝️ Index + Middle Up\nCursor Move]:::gesture
    D --> F[👍 Thumb Out\nFreeze / Scroll]:::gesture
    D --> G[☝️ Index Folded\nLeft Click]:::gesture
    D --> H[🖕 Middle Folded\nRight Click]:::gesture
    D --> I[✌️ No Gap\nDouble Click]:::gesture
    D --> J[🎙️ Voice\nCommand]:::voice

    E & F & G & H & I --> K[🤖 PyAutoGUI\nSystem Action]:::pyautogui
    J --> L[🗣️ SpeechRecognition\nCommand Parser]:::voice
    L --> M[⌨️ Open Keyboard\n🧮 Open Calculator]:::apps

    K --> N[🖥️ Screen / OS Response]:::output
    M --> N

    classDef input      fill:#1B5E20,color:#fff,stroke:none
    classDef mediapipe  fill:#E65100,color:#fff,stroke:none
    classDef decision   fill:#37474F,color:#fff,stroke:none
    classDef gesture    fill:#1A237E,color:#fff,stroke:#5C6BC0
    classDef voice      fill:#4A148C,color:#fff,stroke:none
    classDef pyautogui  fill:#006064,color:#fff,stroke:none
    classDef apps       fill:#880E4F,color:#fff,stroke:none
    classDef output     fill:#33691E,color:#fff,stroke:none
```

---

## 🤚 Gesture Map

```mermaid
flowchart LR
    H([🖐️ Hand Input]):::input

    H --> G1[☝️🖕 Index + Middle Up]:::gesture
    H --> G2[👍 Thumb Out Only]:::gesture
    H --> G3[☝️ Index Folded]:::gesture
    H --> G4[🖕 Middle Folded]:::gesture
    H --> G5[✌️ Fingers Touching]:::gesture
    H --> G6[🎙️ Voice Command]:::voice

    G1 --> A1([🖱️ Move Cursor]):::action
    G2 --> A2([🧊 Freeze / Scroll]):::action
    G3 --> A3([👆 Left Click]):::action
    G4 --> A4([👉 Right Click]):::action
    G5 --> A5([👆👆 Double Click]):::action
    G6 --> A6([⌨️ Keyboard\n🧮 Calculator]):::action

    classDef input   fill:#1B5E20,color:#fff,stroke:none
    classDef gesture fill:#1A237E,color:#fff,stroke:#5C6BC0
    classDef voice   fill:#4A148C,color:#fff,stroke:none
    classDef action  fill:#006064,color:#fff,stroke:none
```

---

## 🦾 How It Works

MediaPipe detects **21 hand landmarks** in real time from the webcam feed. GestureX analyzes these points to determine:

<div align="center">

| Signal | What GestureX Detects |
|:---:|:---|
| 👆 Finger State | Which fingers are **up or folded** |
| 📏 Finger Gap | **Distance** between index and middle finger |
| 👍 Thumb Orientation | Thumb **direction and extension** |
| 🏃 Hand Motion | Overall **movement direction** for scrolling |

</div>

These signals are mapped to system actions using **PyAutoGUI**, and voice commands are handled by **SpeechRecognition** running on a background thread.

---

## 📐 MediaPipe Hand Landmarks

```mermaid
flowchart TD
    W([🔵 Wrist — 0]):::wrist

    subgraph THUMB[👍 Thumb]
        T1[CMC — 1] --> T2[MCP — 2] --> T3[IP — 3] --> T4[Tip — 4]
    end

    subgraph INDEX[☝️ Index Finger]
        I1[MCP — 5] --> I2[PIP — 6] --> I3[DIP — 7] --> I4[Tip — 8]
    end

    subgraph MIDDLE[🖕 Middle Finger]
        M1[MCP — 9] --> M2[PIP — 10] --> M3[DIP — 11] --> M4[Tip — 12]
    end

    subgraph RING[💍 Ring Finger]
        R1[MCP — 13] --> R2[PIP — 14] --> R3[DIP — 15] --> R4[Tip — 16]
    end

    subgraph PINKY[🤙 Pinky]
        P1[MCP — 17] --> P2[PIP — 18] --> P3[DIP — 19] --> P4[Tip — 20]
    end

    W --> T1 & I1 & M1 & R1 & P1

    classDef wrist  fill:#1B5E20,color:#fff,stroke:none
    classDef tip    fill:#BF360C,color:#fff,stroke:none
```

> 💡 GestureX primarily uses landmarks **4 (Thumb Tip)**, **8 (Index Tip)**, **12 (Middle Tip)** and their MCP joints to detect all gestures.

---

## 🛠️ Tech Stack

<div align="center">

| Layer | Technology | Purpose |
|:---:|:---:|:---|
| 🐍 Language | ![Python](https://img.shields.io/badge/Python_3.8-3776AB?style=flat&logo=python&logoColor=white) | Core runtime |
| 🤚 Hand Tracking | ![MediaPipe](https://img.shields.io/badge/MediaPipe-FF6F00?style=flat&logo=google&logoColor=white) | 21-landmark real-time detection |
| 👁️ Vision | ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat&logo=opencv&logoColor=white) | Webcam feed + frame processing |
| 🖱️ Mouse Control | `PyAutoGUI` | Cursor move, click, scroll |
| 🎙️ Voice | `SpeechRecognition` + `PyAudio` | Voice command parsing |
| 🧩 Custom Module | `HandTrackingModule.py` | Landmark abstraction layer |

</div>

---

## 📁 Project Structure

<details>
<summary><b>📂 Click to expand</b></summary>

```
GestureX/
│
├── 🧩 HandTrackingModule.py        # Custom MediaPipe landmark utility
├── 🖱️ gesturex_virtual_mouse.py   # Main gesture recognition + control logic
├── 📄 requirements.txt             # Python dependencies
├── 📖 README.md
└── 🖼️ assets/                     # Screenshots and landmark diagram
```

</details>

---

## 🚀 Installation

**1️⃣ Clone the repository**
```bash
git clone https://github.com/Pragya-Kumar/GestureX-Virtual-Mouse-.git
cd GestureX-Virtual-Mouse-
```

**2️⃣ (Recommended) Create a Python 3.8 virtual environment**
```bash
python3.8 -m venv venv
source venv/bin/activate        # Linux / Mac
venv\Scripts\activate           # Windows
```

**3️⃣ Install dependencies**
```bash
pip install -r requirements.txt
```

**4️⃣ Run GestureX**
```bash
python gesturex_virtual_mouse.py
```

---

## ⚠️ Important Note

> This project works best with **Python 3.8**.
> MediaPipe and PyAudio may **not function properly on Python 3.10+**.
> If you face installation errors, always use a **Python 3.8 virtual environment**.

---

## 👥 Collaborators

<div align="center">

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/Pragya-Kumar">
        <img src="https://github.com/Pragya-Kumar.png" width="80" style="border-radius:50%"/><br/>
        <b>Pragya Kumar</b>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/GeetishM">
        <img src="https://github.com/GeetishM.png" width="80" style="border-radius:50%"/><br/>
        <b>Geetish Mahato</b>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/anamikadey099">
        <img src="https://github.com/anamikadey099.png" width="80" style="border-radius:50%"/><br/>
        <b>Anamika Dey</b>
      </a>
    </td>
  </tr>
</table>

</div>

---

<div align="center">

*Built with 🖐️ + ❤️ by the GestureX team*

⭐ If GestureX impressed you, consider giving it a star!

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,30&height=100&section=footer"/>

</div>
