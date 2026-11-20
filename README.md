# Telepety — Telepresence Robot Interface

Telepety is a low-cost telepresence robotics concept that combines a browser-based video/audio calling interface with remote movement controls.

This repository currently contains a single-page web prototype (`index.html`). It demonstrates the communication and user-interface layer; **it does not contain firmware or a confirmed motor-controller integration**.

## Current prototype

The web interface uses:

- **HTML, CSS, and JavaScript** for the interface
- **PeerJS** (loaded from a CDN) for peer-to-peer connection setup and media/data communication
- Browser camera and microphone APIs for audio/video
- A small command set sent through a PeerJS data connection: `forward`, `backward`, `left`, `right`, and `stop`

## Roles

- **Robot** — selects the robot role, requests camera/microphone access, and waits for a caller.
- **Caller** — selects the caller role and initiates a connection to the configured robot peer ID.

The prototype uses a fixed demo peer ID in the source. This is suitable only for experimentation and should not be considered a secure production identity or access-control mechanism.

## Run

1. Serve `index.html` from a local web server or host it on a compatible HTTPS site.
2. Open it on the robot-side device and select **Telepety (stays home)**.
3. Open it on the remote device and select **Caller**.
4. Grant camera and microphone permissions when prompted.
5. Initiate the call and test the interface.

Browser media APIs generally require a secure context (HTTPS or localhost). A network connection and PeerJS's configured signaling infrastructure are also required.

## Important limitations

- This is a web-interface prototype, not a complete robot system.
- The current repository does not include ESP32/Arduino firmware, motor-driver code, or a hardware command receiver.
- The robot side currently logs received command data; movement commands are not shown as connected to motors in this implementation.
- The prototype has no authentication or authorization layer for the fixed peer ID.
- Camera/microphone access and peer connectivity depend on browser permissions and network conditions.
- No automated tests or hardware validation are included.

## Planned engineering work

1. Define the robot-side hardware architecture and command protocol.
2. Connect the data channel to a firmware receiver.
3. Add explicit connection-state handling and robust call teardown.
4. Add authentication or a safer pairing mechanism before remote operation.
5. Add command timeouts and a fail-safe stop behavior in firmware.
6. Test on target devices and document observed latency and reliability.

## Safety

Do not connect this prototype to a powered robot capable of causing injury until command validation, communication-loss behavior, emergency stop, and hardware-level safeguards have been implemented and tested.

---

*Status: communication/UI prototype; hardware integration and validation remain future work.*
