# ⚡ Electron + React + TypeScript + Vite + Tailwind ⚡

A modern boilerplate for building cross-platform desktop apps with Electron, React, and TypeScript using Vite for super-fast HMR ⚙️

This template is **preconfigured** with:
- ✅ Vite + React + TypeScript
- ✅ Tailwind CSS
- ✅ ESLint + Type-aware rules
- ✅ Electron with full build pipeline (Win/Mac/Linux)
- ✅ Separate TypeScript configs for React and Electron
- ✅ Playwright + Vitest for testing
- ✅ Ready-to-go build & dev scripts

---

## 📦 Scripts

json
"scripts": {
  "dev": "npm-run-all --parallel dev:react dev:electron",
  "dev:react": "vite",
  "dev:electron": "npm run transpile:electron && cross-env NODE_ENV=development electron .",
  "build": "tsc && vite build",
  "preview": "vite preview",
  "transpile:electron": "tsc --project src/electron/tsconfig.json",

  "dist:mac": "npm run transpile:electron && npm run build && electron-builder --mac --arm64",
  "dist:win": "npm run transpile:electron && npm run build && electron-builder --win --x64",
  "dist:linux": "npm run transpile:electron && npm run build && electron-builder --linux --x64",

  "test:e2e": "playwright test",
  "test:unit": "vitest src"
}
🔥 Development
bash
Copy code
npm run dev
This will:

Start Vite dev server for React

Transpile Electron main process TypeScript

Launch Electron app with HMR

📂 Folder Structure
php
Copy code
root/
├── src/
│   ├── electron/             # Electron Main Process (tsconfig isolated)
│   └── renderer/             # React Frontend (Vite + Tailwind + TS)
├── dist/                     # Vite build output
├── public/                   # Static assets
├── tsconfig.json             # Root TS config
├── vite.config.ts            # Vite config for frontend
├── electron-builder.json     # For packaging
🧠 ESLint Setup
Using @typescript-eslint with type-aware linting (separate for React + Electron). You can extend the configuration like this:

ts
Copy code
export default tseslint.config([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      ...tseslint.configs.strictTypeChecked,
      ...tseslint.configs.stylisticTypeChecked,
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
    },
  },
])
You can also use:

eslint-plugin-react-x

eslint-plugin-react-dom

To enable React-specific lint rules:

ts
Copy code
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default tseslint.config([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      reactX.configs['recommended-typescript'],
      reactDom.configs.recommended,
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
    },
  },
])
🛠 Tech Stack Summary
Category	Tools Used
Frontend	React, TypeScript, Tailwind, Vite
Backend/Main	Electron (Main process, bundled separately)
Build Tools	Vite, Electron Builder, TSC
Linting	ESLint with TypeScript + React plugins
Testing	Playwright (E2E), Vitest (unit)
Packaging	electron-builder (supports Windows, MacOS, Linux builds)

🧪 Testing
bash
Copy code
npm run test:unit     # Unit tests with Vitest
npm run test:e2e      # E2E tests with Playwright
🚀 Build Production App
Windows: npm run dist:win

Mac (ARM64): npm run dist:mac

Linux: npm run dist:linux

💡 Why This Template?
Whenever you want to start a new Electron app with full frontend power (React, Tailwind, TS), just clone or pull this template. It’s a solid, clean, production-ready base. You don’t have to deal with separate boilerplate for React and Electron—it’s all combined and ready to scale.

Made with ❤️ by Jeevan
