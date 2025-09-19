## 🧪 Micro Frontend POC Using Vite Federation

In this proof of concept, I explored building a **micro frontend architecture** using multiple frameworks, all integrated via **Vite Federation**. The goal was to demonstrate how different technologies can coexist and communicate within a single host application.

---

### 🧱 Architecture Overview

- **Host Application**: Built with **React**, serving as the shell and orchestrator.
- **Cart Micro Frontend**: Developed using **Angular**.
- **Product Listing Component**: Built with **Vue.js**.
- **Payment Micro Frontend**: Another **React** application.

Each micro frontend is independently developed, built, and deployed, yet seamlessly integrated into the host using Vite Federation.

---

### 🔗 Communication Between Micro Frontends

To enable **data sharing and event handling** across micro frontends, I implemented a **custom event bus**. This allowed components from different frameworks to:
- Emit and listen to events (e.g., cart updates, product selections).
- Share state like selected products or payment status.

This decoupled communication model ensures that each micro frontend remains autonomous while still collaborating effectively.

---

### ⚙️ Vite Federation Setup

The most crucial part of this setup is the **`vite.config.js`** file. It defines:
- Remote entries for each micro frontend.
- Shared dependencies.
- Federation configuration for exposing and consuming modules.

> **Note**: In Vite Federation, you must **build each micro frontend** before it can be accessed by the host. This is because the `remoteEntry.js` file is only generated during the build process.

To preview each micro frontend independently, use:

```bash
npm run build
npm run preview
```

This limitation is important to keep in mind during development and testing.

---

### 🚀 Key Takeaways

- Micro frontends can be built using **different frameworks** and still work together smoothly.
- **Vite Federation** simplifies module sharing and integration.
- **Event-driven communication** is a powerful pattern for decoupling micro frontends.
- Proper configuration in `vite.config.js` is essential for federation to work.
- **Build-before-use** is a current limitation of Vite Federation.

## 📁 Project Structure

```
Mirco_FrontEnd/
├── host/                 # React Host Application (Port 3000)
│   ├── src/
│   │   ├── App.jsx      # Main host component with shared state
│   │   ├── App.css      # Host styling
│   │   └── main.jsx     # React entry point
│   ├── package.json
│   ├── vite.config.js   # Module Federation configuration
│   └── index.html
├── product-app/          # Vue.js Product Application (Port 3001)
│   ├── src/
│   │   ├── App.vue      # Vue product component
│   │   └── main.js      # Vue entry point
│   ├── package.json
│   ├── vite.config.js   # Exposes ./App component
│   └── index.html
├── cart/                 # Angular Cart Application (Port 3002)
│   ├── src/
│   │   ├── app.component.ts    # Angular cart component
│   │   ├── app.component.css   # Angular styling
│   │   └── main.ts      # Angular entry point
│   ├── package.json
│   ├── vite.config.js   # Exposes ./App component
│   ├── tsconfig.json    # TypeScript configuration
│   └── index.html
├── payment/              # React Payment Application (Port 3003)
│   ├── src/
│   │   ├── App.jsx      # Payment processing component
│   │   ├── App.css      # Payment styling
│   │   └── main.jsx     # React entry point
│   ├── package.json
│   ├── vite.config.js   # Exposes ./App component
│   └── index.html
├── setup.sh              # Automated setup script
└── Readme.md            # This file
```

Core repo:- https://github.com/Ashutoshsarangi/micro-front-end (POC video added in the readme file)

Note:- In my final application draft, I changed all the components to React, So I can play around more.
