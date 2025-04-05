# 🏏 Cricket Score Firebase Cloud Functions

This project contains Firebase Cloud Functions to support a real-time cricket scoring web application using Firestore. It processes ball-by-ball data and updates match state documents such as live scores, batting and bowling summaries, and innings info.


## 📁 Project Structure

```
cricket-score-functions/
├── firebase.json        # Firebase configuration (emulators, deploy targets, etc.)
├── .firebaserc          # Project alias and default Firebase project
└── functions/           
    ├── package.json     # NPM dependencies and scripts
    ├── tsconfig.json    # TypeScript compiler settings
    ├── src/
    │   └── index.ts     # Main entry for cloud functions
    └── lib/             # Compiled JS output (auto-generated)
```


## 🚀 Setup Instructions

### 1. Prerequisites

- [Node.js](https://nodejs.org/) (v18+ recommended)
- [Firebase CLI](https://firebase.google.com/docs/cli)
- [Yarn](https://yarnpkg.com/) or `npm`


### 2. Clone and Install

```bash
git clone https://github.com/your-username/cricket-score-functions.git
cd cricket-score-functions/functions
yarn install   # or npm install
```


### 3. Development

Run Firebase emulators locally:

```bash
firebase emulators:start
```

Compile TypeScript in watch mode:

```bash
yarn run build:watch   # or npm run build:watch
```

> You can edit `src/index.ts` — compiled code appears in `lib/`.

---

### 4. Deploy

To deploy functions to your Firebase project:

```bash
firebase deploy --only functions
```

---

## 🔥 Function Overview

Your Cloud Functions listen to writes/updates/deletes on:

- `/feed/{id}` — each ball in the match
  - On create: processes the ball and updates game state
  - On update/delete: recalculates totals and cleans up affected documents

And update:

- `/main/live` — live match summary
- `/batting` — current batting lineup with stats
- `/bowling/{id}` — current bowling stats
- `/inning` — track innings progression and scores

---

## 🛠️ Scripts

| Script         | Description                     |
|----------------|---------------------------------|
| `build`        | Compiles TypeScript → JS        |
| `build:watch`  | Watch mode for development      |
| `deploy`       | Deploys functions to Firebase   |
| `emulators`    | Starts local emulator suite     |

You can add these to `package.json`:

```json
"scripts": {
  "build": "tsc",
  "build:watch": "tsc --watch",
  "deploy": "firebase deploy --only functions",
  "emulators": "firebase emulators:start"
}
```