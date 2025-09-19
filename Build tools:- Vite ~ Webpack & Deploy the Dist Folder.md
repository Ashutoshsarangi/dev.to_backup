When ever we do dynamic imports the bundler plugins, like webpack, Parcel, Rollup, and esbuild can be configured to split JavaScript bundles into smaller chunks whenever they encounter a **dynamic import()** call in your source code.

Vite internally using esbuild for bundling so it also split in to chunks.


Earlier days we are expecting as previous version of webpack bundles to a single file . now a days it is anti pattern . and every one wants to have the minimal chunks rather than a single loaded js /css file.

Now with http2 protocol we can set parally more than 100 (default) network calls. so in chunk data it would be improve performance a lot.

in the Earlier http/1 protocol, we can go for 6 parallel API calls. Other API calls browser put them in queue and when time arries it will start hitting Server for data.

When using HTTP/2, the maximum number of simultaneous HTTP streams is negotiated between the server and the client (defaults to 100).
 

http1, every time validation header overhead...


![Network Queued Api calls](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jb3vipfrc3wvvij9pmmf.png)

Performance benefit of 

**CSS Module**

- counter.module.css
it will have the modular scope rather then global scope.

---

### ⚙️ **Core Differences**

| Feature            | **Vite**                                  | **Webpack**                               |
|--------------------|-------------------------------------------|-------------------------------------------|
| **Build Strategy** | Uses **native ES modules** for dev server | Bundles everything upfront                |
| **Dev Server**     | Instant startup with **on-demand** loading| Slower startup due to full bundling       |
| **Hot Module Reload (HMR)** | Extremely fast and efficient         | Slower and sometimes buggy                |
| **Configuration**  | Minimal config out of the box             | Highly configurable but complex           |
| **Plugin Ecosystem** | Growing, based on Rollup                | Mature and extensive                      |
| **Build Tooling**  | Uses **Rollup** for production builds     | Uses its own bundler                      |

---

### ✅ **Advantages of Vite**

1. **Blazing Fast Dev Server**: Uses native ESM and serves files on demand.
2. **Simpler Configuration**: Easier to set up and use, especially for small to medium projects.
3. **Modern Syntax Support**: Built with modern JS and TS in mind.
4. **Better HMR**: Updates modules almost instantly.
5. **Optimized Production Build**: Uses Rollup for tree-shaking and smaller bundles.

---

### ❌ **Disadvantages of Vite**

1. **Limited Legacy Support**: May not work well with older browsers or complex legacy setups.
2. **Plugin Ecosystem Still Growing**: Not as mature as Webpack’s.
3. **Rollup Limitations**: Some advanced bundling features are harder to achieve.

---

### ✅ **Advantages of Webpack**

1. **Highly Configurable**: Can handle complex setups and custom workflows.
2. **Mature Ecosystem**: Tons of plugins and loaders available.
3. **Wide Adoption**: Lots of community support and documentation.
4. **Works with Legacy Code**: Better suited for older projects or mixed tech stacks.

---

### ❌ **Disadvantages of Webpack**

1. **Slow Dev Server**: Full bundling makes startup and rebuilds slower.
2. **Complex Configuration**: Can be hard to maintain and debug.
3. **HMR Performance**: Not as fast or reliable as Vite.

---

### 🧠 When to Use What?

- **Use Vite** if you're starting a new project with modern frameworks like Vue 3, React, or Svelte, and want fast development experience.
- **Use Webpack** if you're working on a large, legacy codebase or need advanced customization and plugin support.

---

Yes, both **Vite** and **Webpack** support **tree-shaking**, **uglifying**, and **minification**, but they handle these tasks differently due to their underlying architectures.

---

### 🌳 **Tree-Shaking**

- **Webpack**: Supports tree-shaking via its static analysis of ES modules. You need to use `mode: 'production'` and ensure your code uses ES module syntax (`import/export`) for effective tree-shaking.
- **Vite**: Uses **Rollup** for production builds, which has excellent tree-shaking capabilities. Vite automatically tree-shakes unused code during the build process.

---

### 🧹 **Uglifying and Minification**

- **Webpack**:
  - Uses **TerserPlugin** for minification and uglification in production mode.
  - Automatically enabled when `mode: 'production'` is set.
  - You can customize it via `optimization.minimizer`.

- **Vite**:
  - Uses **esbuild** during development (which is fast but not as powerful for minification).
  - For production, Vite uses **Rollup + Terser** for minification and uglification.
  - You can configure this in `vite.config.js` under `build.minify`.

---

### 🔧 Example Config Snippets

**Webpack (webpack.config.js):**
```js
module.exports = {
  mode: 'production',
  optimization: {
    minimize: true,
    minimizer: [new TerserPlugin()],
  },
};
```

**Vite (vite.config.js):**
```js
export default {
  build: {
    minify: 'terser', // or 'esbuild' for faster builds
    terserOptions: {
      compress: true,
      mangle: true,
    },
  },
};
```

---

### 📦 What is Rollup?

**Rollup** is a **JavaScript module bundler**—similar to Webpack—but it's designed with a focus on **ES modules (ESM)** and **tree-shaking**. It takes your application code and its dependencies and bundles them into optimized files for production.

---

### 🔍 Key Features of Rollup

1. **Tree-Shaking**: Rollup is known for its **aggressive and effective tree-shaking**, which removes unused code from your final bundle.
2. **ES Module First**: It was built around the ES module standard (`import/export`), making it ideal for modern JavaScript.
3. **Smaller Bundles**: Because of its optimization strategies, Rollup often produces **smaller and cleaner bundles** than Webpack.
4. **Plugins System**: Rollup has a flexible plugin system that allows you to customize the build process.
5. **Code Splitting**: Supports splitting code into multiple chunks for better performance.

---

### 🛠️ How Rollup Works in Vite

- In **development**, Vite uses **ESBuild** for lightning-fast module resolution and transformation.
- In **production**, Vite switches to **Rollup** to bundle your app efficiently.
- This hybrid approach gives you the best of both worlds: fast dev experience and optimized production builds.

---

### ✅ Here's how it works:

- **Vite internally uses Rollup** for production builds.
- You configure **everything** (development and production) in **`vite.config.js`**.
- If you need to customize Rollup-specific behavior (like plugins, output formats, etc.), you do it **inside `vite.config.js`** under the `build.rollupOptions` field.

---

### 🛠️ Example: Rollup Options in `vite.config.js`

```js
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  build: {
    rollupOptions: {
      input: 'src/main.js',
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom']
        }
      },
      plugins: [
        // Add Rollup plugins here if needed
      ]
    }
  }
});
```

This way, you get full control over Rollup's behavior **without needing a separate `rollup.config.js` file**.

---

### 🧠 Summary

| Task                  | File to Use         |
|-----------------------|---------------------|
| Development config    | `vite.config.js`    |
| Production build      | `vite.config.js` (with `build.rollupOptions`) |
| Rollup customization  | Inside `vite.config.js` |

---

### 🔍 What does this do?

```js
output: {
  manualChunks: {
    vendor: ['react', 'react-dom']
  }
}
```

This tells Rollup (via Vite) to:

- Create a **separate chunk** named `vendor`.
- Put the modules `react` and `react-dom` into that chunk.
- This chunk will be loaded separately from your main application code.

---

### ✅ Why is this useful?

1. **Better caching**: Vendor libraries like React change less frequently than your app code. By separating them, browsers can cache the vendor chunk longer.
2. **Faster initial load**: Smaller initial bundles mean faster page loads.
3. **Improved performance**: Helps with parallel loading and reduces the size of critical path resources.

---

### 📦 Resulting Bundle Structure

After build, you might see something like:

```
dist/
├── assets/
│   ├── vendor.[hash].js     ← contains react & react-dom
│   ├── main.[hash].js       ← your app code
```

---

### 🧠 When to use `manualChunks`

- For large dependencies (like React, Vue, Lodash, etc.)
- For code splitting by route or feature
- For optimizing caching and performance

---

Once Vite generates the **`dist/`** folder during the production build, you're ready to deploy your app. Here's how you can do it depending on your hosting environment:

---

### 🚀 Common Deployment Options

#### 1. **Static Hosting Services**
These are ideal for Vite apps since they generate static files.

- **Netlify**
  - Drag and drop the `dist/` folder in the dashboard, or use CLI:
    ```bash
    netlify deploy --prod --dir=dist
    ```

- **Vercel**
  - Use the Vercel CLI or Git integration.
  - Set the build output directory to `dist`.

- **GitHub Pages**
  - Use a plugin like `vite-plugin-gh-pages` or manually push `dist/` to the `gh-pages` branch.

- **Firebase Hosting**
  ```bash
  firebase init
  firebase deploy
  ```
  Set `dist` as the public directory during setup.

---

#### 2. **Traditional Web Servers (Apache, Nginx, etc.)**
- Upload the contents of the `dist/` folder to your server’s public directory (e.g., `/var/www/html`).
- Make sure your server is configured to serve `index.html` and handle SPA routing (e.g., fallback to `index.html` for unknown routes).

---

#### 3. **Docker**
You can containerize your Vite app:

```Dockerfile
FROM nginx:alpine
COPY dist/ /usr/share/nginx/html
```

Then build and run the container.

---

#### 4. **Cloud Platforms**
- **AWS S3 + CloudFront**: Upload `dist/` to an S3 bucket and serve via CloudFront.
- **Azure Static Web Apps**: Connect your repo and set `dist` as the output folder.
- **Google Cloud Storage**: Upload `dist/` and configure bucket for static hosting.

---

### 🧪 Quick Checklist Before Deploying

- ✅ Run `vite build` to generate the `dist/` folder.
- ✅ Ensure all assets are correctly referenced (relative paths or base config).
- ✅ Test locally with `npx serve dist` or similar.
- ✅ Choose a hosting method and upload the contents of `dist/`.


Reference :-

- https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events
