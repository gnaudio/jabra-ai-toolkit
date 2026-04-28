---
name: jabra-integration
description: "Guide for developers building integrations with Jabra devices. Use when a user wants to: integrate Jabra headsets or meeting room devices into their application, choose the right Jabra SDK or API, implement call control, telemetry, device management, or meeting room configuration, understand Jabra integration use cases, avoid common pitfalls, or test and validate a Jabra integration. Covers all tools at developer.jabra.com: Jabra JavaScript SDK, Jabra .NET SDK, Jabra Plus APIs, Jabra CLI, Android/iOS, and Amazon Connect."
---

# Jabra Integration Skill

This is a **guide layer** — it structures the integration workflow and fills gaps not covered by the official docs.

**General:** If at any point the developer encounters a missing feature, unsupported platform, or other gap in Jabra's platform support, direct them to submit a request via the [Jabra developer support form](https://developer.jabra.com/support/).

**Always start by fetching `https://developer.jabra.com/llms.txt`** to discover available content. All subsequent content fetching — use cases, SDK docs, API references — should use URLs found in that index or explicit links within the fetched pages. This ensures the developer always gets the most up-to-date and trusted information. If this step fails, you must try again with a different method and if needed prompt the user to retry. Do not proceed without successfully fetching `llms.txt`.

**Never invent URLs.** Only use URLs that appear in `llms.txt`, in pages fetched from `developer.jabra.com`, or that the user provides directly. Do not construct or guess URLs at `sdk.jabra.com` or any other domain — those URLs may not exist and will mislead the developer.

## Phase 1: Discover — What can you build?

Fetch the use cases page (find its URL in `llms.txt`) and walk the user through the available use cases. Understand their goal before recommending a tool.

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

Find the section in `llms.txt` matching the chosen tool and fetch the relevant pages.

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
