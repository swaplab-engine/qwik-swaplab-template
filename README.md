# Qwik City App ⚡️

- [Qwik Docs](https://qwik.dev/)
- [Discord](https://qwik.dev/chat)
- [Qwik GitHub](https://github.com/QwikDev/qwik)
- [@QwikDev](https://twitter.com/QwikDev)
- [Vite](https://vitejs.dev/)

---

# Qwik Capacitor Template ⚡️

Official Qwik template optimized for **[SwapLab.net](https://swaplab.net)**.
This template comes pre-configured with `@capacitor/core`, `@capacitor/android`, and `@capacitor/ios`, ready for instant mobile build.

## 🚀 Build Support & Pricing

| Build Type | Availability |
| :--- | :--- |
| **Debug APK** | ✅ **Free Forever** (Unlimited, No Subscription) |
| **Release APK / AAB** | 🎁 **Free PROMO** (Ends Jan 1, 2026) |
| **Export Android Studio/Xcode** | 🎁 **Free PROMO** (Ends Jan 1, 2026) |

---

## 📂 System Bridge (Workflows)

> [!WARNING]
> **⛔️ CRITICAL: DO NOT DELETE THE `.github/workflows` DIRECTORY**
>
> This directory is the **digital bridge** connecting your repository to the SwapLab Service.
> * **How it works:** SwapLab acts as the **Trigger**, but the build runs on **YOUR GitHub Account** using your Action Minutes.
> * **Consequence:** Removing these files will **sever the connection**, and the Service will be **unable to trigger** the build process.

### Available Workflows

Select and copy the workflow that matches your project requirements:

| Filename | Purpose | Recommended For |
| :--- | :--- | :--- |
| `capacitor-workflow-cache.yml` | Standard Capacitor build with caching. | **Most Users** (Faster builds) |
| `capacitor-workflow-build-no-cache.yml`| Capacitor build **without cache**. | Debugging dependency issues |
| `both-workflow-repo-cache.yml` | Universal workflow for repositories containing both frameworks. | Hybrid Projects |

---

## ⚡ How to Build

Choose the method that suits your workflow. Both options utilize **your GitHub Action minutes** for the build execution.

### Option A: Repository Builder (CI/CD Automation)
*Best for automated builds directly from your GitHub repository.*

> **Requirement:** To prevent the `.github` bridge folder from being included in your build artifact, you **must** organize your repository as a **Monorepo** (e.g., place your app source code inside a subfolder like `my-app`, not in the root).

1.  **Create Repository:** Click **Use this template** > **Create a new repository** (Select **Private**).
2.  **Access Service:** Log in to **[repository.swaplab.net](https://repository.swaplab.net)**.
3.  **Start Build:**
    * Select your repository.
    * Select **Capacitor** as the Framework Type.
    * **Project Folder Name:** ✍️ **ENTER FOLDER NAME** (e.g., `my-app`).
    * *Critical:* **DO NOT** leave this empty. You must specify the subfolder to ensure the `.github` folder is excluded.
    * Click **Build from Repository**.

### Option B: Capacitor Builder (Manual Upload)
*Best for quick builds via Zip upload. Also uses your GitHub Action minutes.*

1.  **Download:** Click **<> Code** > **Download ZIP**.
2.  **Extract & Prepare:** * Unzip the downloaded file.
    * Select your source folder (exclude the `.github` folder if possible).
    * **Zip** your source code.
3.  **Build:** Go to **[capacitor.swaplab.net](https://capacitor.swaplab.net)**.
4.  **Configure:**
    * Select **Capacitor** as the Framework Type.
    * Upload your zip file.
    * Click **Build**.

---

## 🛠 Open Source Environment

We believe in transparency. Our build infrastructure is open for inspection:

* **🐳 Capacitor Core:** [View Public Base Image](https://github.com/swaplab-engine/capacitor-core)
* **🐳 Cordova Core:** [View Public Base Image](https://github.com/swaplab-engine/cordova-core)
* **📦 Build Packages:** [View Engine Images Registry](https://github.com/orgs/swaplab-engine/packages)
* **⚙️ Workflow Templates:** [View Integration .yml Files](https://github.com/swaplab-engine/workflow-templates)

---

## 📚 Complete Service Information

Need more details about the service?
For comprehensive documentation, full guides, and other framework templates, please visit our central repository:

👉 **[SwapLab Service Documentation & Templates](https://github.com/swaplab-engine/template-capacitor)**