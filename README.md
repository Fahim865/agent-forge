# Agent Forge

# FJ Vibe Agent — Core Functionality Test & Fix Prompt

## ROLE

Act as a senior debugging engineer. Do NOT add new features. 

ONLY test and fix the core agent loop.

## STEP 1 — RUN THIS EXACT TEST

1. Launch the application.

2. Add an API provider with a real API key and model.

3. Test the connection — confirm it actually succeeds.

4. Open/create a simple project (HTML/CSS/JS).

5. Prompt: "Build a simple landing page with a hero section and a button."

6. Verify:

   - Did the AI actually respond?

   - Were real files actually created in the folder? (check disk, 

     not just chat message)

   - Does the live preview show the actual website?

7. Prompt: "Change the button color to blue."

   - Verify the file actually changed and preview updated.

## STEP 2 — REPORT EXACT RESULTS

For each step above, report clearly:

- What worked

- What failed

- The EXACT error message (if any), not a summary

- Whether it's a UI bug, API connection bug, tool-calling bug, or 

  file-system bug

## STEP 3 — FIX ONLY WHAT'S BROKEN

- Do not rewrite working parts.

- Fix the root cause of each failure found in Step 1.

- Re-run the same test after each fix.

## STEP 4 — CONFIRM

Only report "working" after the full test (Step 1) passes completely, 

end to end, with real file changes and real preview updates verified.

## RULE

Do not claim success without actual verification. If something is 

broken, say exactly what and why.
# FJ Vibe Agent — Build Core Agent (Chat + Tools) On Top of Existing Scaffold

## ROLE

Act as a senior AI-agent engineer. The project already has: API key 

secure storage (Rust keyring), desktop auto-updater, and Android 

version-gate logic. Do NOT modify or rebuild these — they are done.

## WHAT'S MISSING (BUILD THIS NOW)

1. Chat UI — a real chat interface in the app (not just the settings screen)

2. AI provider call — actually send messages to the user's configured 

   API (OpenAI-compatible / Anthropic) using their stored key + selected 

   model, and stream/display the real response

3. Tool system — implement: read_file, write_file, edit_file, list_files, 

   run_command — as real Tauri commands (Rust backend) that the AI can call

4. Agent loop — connect chat → AI decides to use tools → tools execute 

   on the real filesystem/terminal → results go back to AI → AI continues 

   → final response shown to user

5. Workspace selection — let user pick a real folder as the active project

6. Basic live preview — at least for simple HTML/CSS/JS projects

## VALIDATION (MUST PASS BEFORE REPORTING DONE)

1. Launch app, enter real API key + model.

2. Select/open a folder as workspace.

3. Type: "Create a simple HTML page with a heading that says Hello."

4. CONFIRM: a real .html file appears in that folder on disk.

5. Type: "Change the heading to say Welcome."

6. CONFIRM: the file actually changed.

Do not report success without this test passing for real.

## RULE

Do not fake AI responses, tool execution, or file changes. If a step 

fails, report the exact error.
Gemini চ্যাটে code লিখে দেয় (টেক্সট)

        ↓

তুমি সেই code গুলো ফাইলে সেভ করো (ঠিক ফোল্ডার স্ট্রাকচারে)

        ↓

কেউ একজন (যার Rust/Tauri setup আছে) build command চালায়

        ↓

Build শেষে .exe ফাইল তৈরি হয় ওই computer-এই

        ↓

সেই .exe ফাইল তুমি তোমার laptop-এ নিয়ে install করো
name: Build FJ Vibe Agent

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: windows-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Install Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install Rust
        uses: dtolnay/rust-action@v1
        with:
          toolchain: stable

      - name: Install frontend dependencies
        run: npm install

      - name: Build Tauri App
        uses: tauri-apps/tauri-action@v0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Upload Windows Installer
        uses: actions/upload-artifact@v4
        with:
          name: fj-vibe-agent-windows
          path: src-tauri/target/release/bundle/nsis/*.exe
I am building a Tauri (Rust + React/TypeScript) desktop application 

called "FJ Vibe Agent." We have already written code for this project 

across our previous conversation, including:

- Cargo.toml

- tauri.conf.json

- src-tauri/src/lib.rs

- src-tauri/src/main.rs

- src-tauri/src/agent_tools.rs

- src/lib/secureStore.ts

- src/lib/updater.ts

- src/lib/androidUpdateGate.ts

- src/lib/toolsBridge.ts

- src/lib/agentLoop.ts

- src/components/AgentWorkspace.tsx

- src/App.tsx

I need to upload this ENTIRE project to a GitHub repository so it can 

be built automatically via GitHub Actions. To do this correctly, I 

need you to give me EVERY file needed for the complete project, 

clearly organized.

Please provide:

1. A COMPLETE FILE TREE first, showing every file and folder path 

   needed for this project to build successfully, for example:


2. Then, for EACH file in that tree, give me the FULL, complete, final 

   content — including any files not yet written that are REQUIRED for 

   the project to actually build (such as package.json with correct 

   dependencies and scripts, index.html, vite.config.ts, tsconfig.json, 

   src/main.tsx entry point, src-tauri/build.rs, and a basic .gitignore).

3. Clearly label each file with its exact path as a heading before its 

   code block, like:

   ### File: src-tauri/Cargo.toml

```toml

   ...content...

```

4. Do NOT skip or summarize any file with "// rest stays the same" — 

   give the full, real, complete content of every single file needed, 

   since I will be copying each one directly into a new GitHub repository.

5. Also tell me if I need placeholder icon files (icons/32x32.png, 

   icons/128x128.png, icon.ico, icon.icns) for the build to succeed, 

   and if so, the simplest way to generate them.

6. Double check: make sure package.json includes all required 

   dependencies (React, Tauri APIs, tauri-plugin-updater, 

   tauri-plugin-process, etc.) so `npm install` won't fail.

Give me everything needed so that if I copy these files exactly as-is 

into a new GitHub repository and run a GitHub Actions Tauri build, it 

will compile successfully with zero missing files or errors.

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/cc1b004c-6a3b-4ec0-b49d-7d93b1ea6dd1).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
