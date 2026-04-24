---
name: jabra-integration
description: "Guide for developers building integrations with Jabra devices. Use when a user wants to: integrate Jabra headsets or meeting room devices into their application, choose the right Jabra SDK or API, implement call control, telemetry, device management, or meeting room configuration, understand Jabra integration use cases, avoid common pitfalls, or test and validate a Jabra integration. Covers all tools at developer.jabra.com: Jabra JavaScript SDK, Jabra .NET SDK, Jabra Plus APIs, Jabra CLI, Android/iOS, and Amazon Connect."
---

# Jabra Integration Guide

This skill is a **guide layer** — it helps developers choose the right tool and understand the right use case, then fetches the authoritative documentation from [developer.jabra.com](https://developer.jabra.com) on demand. Do not reproduce SDK docs from memory; always fetch the relevant page.

## Step 1: Choose the Right Integration Tool

| Tool | Platform | Best for |
|------|----------|----------|
| **Jabra JavaScript SDK** (`@gnaudio/jabra-js`) | Browser (Chrome/Edge), Node.js | Web-based softphones, browser apps, Electron and other nodejs based desktop apps |
| **Jabra .NET SDK** (`Jabra.NET.Sdk`) | Windows, macOS, Linux (.NET) | Desktop apps, Windows softphones, enterprise apps |
| **Jabra Plus APIs** (REST, beta) | Any (cloud) | Remote fleet management, device inventory, meeting room management |
| **Jabra CLI** | Windows, macOS | IT automation, firmware updates, device config without code |
| **Android / iOS** | Mobile | Call control on mobile (native platform APIs); Jabra Perform/BlueParrott button/telemetry |

**Quick decision guide:**
- Building a softphone or UC client? → **JavaScript SDK** (web) or **.NET SDK** (desktop)
- Managing a fleet of devices remotely from the cloud? → **Jabra Plus APIs**
- IT admin scripting / firmware updates without code? → **Jabra CLI**
- Building a mobile app? → Android Telecom Framework / iOS CallKit for general Jabra devices; Jabra Perform/BlueParrott SDK for those specific device families

## Step 2: Fetch the Relevant Documentation

For use case details, SDK specifics, code samples, and API methods — **fetch the relevant page** from developer.jabra.com. Do not reproduce docs from memory.

| Tool / Topic | URL to fetch |
|---|---|
| Use cases overview | `https://developer.jabra.com/use-cases.md` |
| JavaScript SDK | `https://developer.jabra.com/sdks-and-tools/javascript.md` |
| .NET SDK | `https://developer.jabra.com/sdks-and-tools/dotnet.md` |
| Jabra Plus APIs | `https://developer.jabra.com/sdks-and-tools/jabraplusapis.md` |
| Jabra CLI | `https://developer.jabra.com/sdks-and-tools/jabracli.md` |
| Android / iOS | `https://developer.jabra.com/sdks-and-tools/android-ios.md` |
| Amazon Connect SDK | `https://developer.jabra.com/sdks-and-tools/amazonconnect.md` |

When reading the fetched documentation:
- Follow the guidance provided but look for links to "API Reference" for the most up-to-date method signatures and details.
- Look for links to code samples and usage examples and fetch those as well when needing practical implementation guidance.

## Key Requirements for All Integrations

- A **Partner Key** is recommended to use any Jabra SDK (JavaScript or .NET) in production. For development purposes the key is not required. The same key can be used accross environments for the same application. The key is issues to a named company. Obtained via the [Jabra developer support form](https://developer.jabra.com/support/).
- Always provide a meaningful `appId` and `appName` — these identify your integration in log files.
- Always handle device added/removed events — devices can be connected/disconnected at any time.
- Use **Easy Call Control (multi-call option)** for all new call control integrations. Do not use legacy CallControl.
