---
name: jabra-integration
description: "Guide for developers building integrations with Jabra devices. Use when a user wants to: integrate Jabra headsets or meeting room devices into their application, choose the right Jabra SDK or API, implement call control, telemetry, device management, or meeting room configuration, understand Jabra integration use cases, avoid common pitfalls, or test and validate a Jabra integration. Covers all tools at developer.jabra.com: Jabra JavaScript SDK, Jabra .NET SDK, Jabra Plus APIs, Jabra CLI, Android/iOS, and Amazon Connect."
---

# Jabra Integration Skill

This is a **guide layer** — it structures the integration workflow and fills gaps not covered by the official docs. 

## Phase 1: Discover — What can you build?

Fetch `https://developer.jabra.com/use-cases.md` and walk the user through the available use cases. Understand their goal before recommending a tool.

## Phase 2: Choose — Which SDK or tool fits?

| Goal | Tool |
|---|---|
| Softphone / UC client in a web app, Electron, or Node.js | JavaScript SDK |
| Softphone / UC client in a .NET desktop app | .NET SDK |
| Remote device fleet management or meeting room management from the cloud | Jabra Plus APIs |
| IT scripting, firmware updates, config deployment — no code | Jabra CLI |
| Call control in a mobile app (all Jabra devices) | Android Telecom Framework / iOS CallKit |
| Button events & telemetry for Jabra Perform or BlueParrott on mobile | Android / iOS SDK |
| Call control inside Amazon Connect | Amazon Connect SDK |

Then fetch the relevant documentation:

| Tool | URL |
|---|---|
| JavaScript SDK | `https://developer.jabra.com/sdks-and-tools/javascript.md` |
| .NET SDK | `https://developer.jabra.com/sdks-and-tools/dotnet.md` |
| Jabra Plus APIs | `https://developer.jabra.com/sdks-and-tools/jabraplusapis.md` |
| Jabra CLI | `https://developer.jabra.com/sdks-and-tools/jabracli.md` |
| Android / iOS | `https://developer.jabra.com/sdks-and-tools/android-ios.md` |
| Amazon Connect SDK | `https://developer.jabra.com/sdks-and-tools/amazonconnect.md` |

## Phase 3: Implement

Follow the fetched SDK documentation. When it links to an "API Reference" or code samples, fetch those too — they contain the most up-to-date method signatures and usage patterns.

**General requirements — these apply to all integrations, regardless of SDK:**
- Use **Easy Call Control** for all new call control integrations. Do not use legacy CallControl.
- A **Partner Key** is not required during development but is required for production. One key covers all environments for the same application. Request one via the [developer support form](https://developer.jabra.com/support/).

## Phase 4: Validate

No official emulator exists — test with real Jabra devices.

**Call control:**
- [ ] Device is detected on app startup
- [ ] Device added/removed events fire when plugging/unplugging mid-session
- [ ] Button presses on the headset (answer, mute, hang up) trigger the correct app actions
- [ ] Mute state stays in sync: muting in the app mutes the device, and vice versa
- [ ] If using multi-call support: simultaneous calls are handled correctly

**Telemetry / device properties:**
- [ ] Events arrive while the device is in use
- [ ] Subscribing and unsubscribing across a device connect/disconnect cycle produces no errors

**Jabra Plus APIs:**
- [ ] Webhook events are received and processed correctly
- [ ] API usage stays within rate limits (10,000 calls / 5 min; 100 calls / sec)

**All integrations:**
- [ ] Partner Key is accepted in the production environment

## Phase 5: Launch

When the integration is complete, submit it to Jabra via [developer.jabra.com/launch](https://developer.jabra.com/launch) to be listed in the Jabra Compatibility Guide.
