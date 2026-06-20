# Mobile Hang / Crash Payload

A self‑contained, cross‑browser HTML payload that demonstrates the extreme limits of mobile browser resource management. It combines every known client‑side exhaustion technique to produce a near‑instantaneous, irreversible freeze or crash on any visiting device.

## ⚠️ Important Notice
This repository is provided **strictly for educational and defensive research purposes**. Use only on devices you own or have explicit permission to test. The author is not responsible for any damage, data loss, or misuse.

## 🖇️https://browser-killer.netlify.app

## Features
- **Synchronous infinite loop** – blocks the main thread permanently.
- **64 dedicated Web Workers** – saturate all CPU cores with mathematical operations.
- **SharedArrayBuffer + Atomics** – synchronises worker attacks (when cross‑origin isolated).
- **WebAssembly infinite loop** – runs at near‑native speed, bypassing JIT heuristics.
- **Catastrophic regular expression backtracking** – consumes exponential time.
- **Dynamic `eval` / `Function` constructor bombs** – prevents JIT optimisation.
- **Memory bomb** – allocates 50+ MB ArrayBuffers repeatedly until OOM.
- **DOM flood** – injects 50,000+ animated elements with unique keyframes.
- **Canvas 2D & WebGL spam** – forces continuous GPU rendering and buffer allocations.
- **AudioContext white‑noise** – keeps the audio thread busy.
- **Vibration & WakeLock** – drains battery and prevents screen sleep.
- **Network flood** – fires hundreds of fetch/XHR/WebSocket requests.
- **IndexedDB & localStorage storms** – writes massive data repeatedly.
- **Promise chain recursion** – blocks the microtask queue.
- **Proxy traps & getter loops** – trigger infinite recursion on property access.
- **Resize / scroll / touch event spam** – forces constant layout recalculation.
- **MutationObserver chain** – adds more elements on every DOM change.
- **CSS Paint Worklet** – offloads infinite rendering to the compositor (if supported).
- **Console spam** – fills developer console with huge objects.
- **Multiple `alert()` dialogs** – attempts to block UI (if not suppressed).
- **`with` statement abuse** – prevents JavaScript engine optimisations.

## How It Works
When the page loads, a minimal UI is painted to trick the user. After 50 ms, the main thread enters an infinite `while` loop that never yields, freezing all event handling. Concurrently, a swarm of Web Workers begins executing identical infinite loops, consuming all available CPU cores. WebAssembly code runs an unconditional infinite loop at the machine‑code level. Memory allocation functions recursively allocate large buffers until the browser runs out of heap, triggering garbage collector churn and eventually an OOM crash. The DOM is flooded with thousands of elements, each with its own CSS animation, forcing the rendering engine to recompute styles and paint continuously. Canvas and WebGL contexts are updated at 60+ fps with heavy drawing operations, overloading the GPU. Audio context generates white noise in a loop, keeping the audio subsystem busy. Network, storage, and sensor APIs are hammered with concurrent requests. All these vectors operate simultaneously, ensuring that even if one technique is throttled by the browser, the others will succeed.

## Usage
1. Clone this repository or download the `index.html` file.
2. Serve it via any web server (e.g., `python -m http.server 8080`).
3. For maximum effectiveness (enabling SharedArrayBuffer), serve with the following headers:
   Cross-Origin-Opener-Polocy: same-origin Cross-Origin-Embedder-Policy: require-coro

   4. Open the URL on a mobile device (or desktop) using any modern browser.
5. The page will appear to load, then freeze the tab within 1–3 seconds.

## Technical Details
- **File size:** ~8 KB (minified) / ~12 KB (readable).
- **Dependencies:** None – pure HTML/CSS/JavaScript.
- **Browser support:** Chrome 80+, Firefox 75+, Safari 13+, Edge 80+ (Android/iOS).
- **APIs used:** `Web Workers`, `SharedArrayBuffer`, `Atomics`, `WebAssembly`, `AudioContext`, `Canvas 2D`, `WebGL`, `IndexedDB`, `localStorage`, `fetch`, `XMLHttpRequest`, `WebSocket`, `Geolocation`, `Vibration`, `WakeLock`, `Fullscreen`, `MutationObserver`, `CSS Paint Worklet`, `Touch Events`, `requestAnimationFrame`, `eval`, `Proxy`, `Reflect`, `RegExp`.

## Disclaimer
This code is a **proof‑of‑concept** for security researchers and developers to understand browser resource limits and to test device resilience. It is not intended for malicious use. The user assumes all responsibility for any consequences arising from its execution.

---

**Built with Ibrahim404_cyber – no limits, no hesitation.**
