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


> [!TIP]
> **🛡️ Security & Trial Options (Zero-Trust)**
>
> If you are hesitant about uploading your **Keystore/Signing Keys** to a cloud service, you have a safe alternative:
> * **Local Signing:** Choose **`Export Android Studio`** or **`Export Xcode`** as your build type. We will compile the native project structure for you, and you can sign the final app locally on your own machine.
> * **Plugin Devs & Testing:** Use **`Debug APK`** (Unlimited/Free). It requires no keys and is perfect for testing **Capacitor/Cordova plugins** or evaluating the service without a subscription.


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




## 📺 Video Tutorials

Visual learner? Watch our step-by-step guides directly on YouTube.

* **🎥 [Getting Started: Connect Qwik Repo to SwapLab (GitHub App Integration)](https://youtu.be/TehmU1-lnq8)**
* **🚀 [Qwik Mobile Testing: Generate Debug APK & Run on Emulator](https://youtu.be/URWGhDdiA3w)**
* **🚀 [Qwik to Android Studio: No CLI, Drag & Drop to Emulator](https://youtu.be/So42rRI_cZk)**
* **🍎 [Qwik to iOS: Capacitor Build & Run in Xcode Simulator](https://youtu.be/eMI-FLVkIS4)**



## 🔐 Signing Production Builds (Repository Builder Only)

> **Important:** This section applies **ONLY** to users using **Option A (Repository Builder)**.
> If you are using Option B (Manual Upload), you do not need to configure these secrets.

To generate signed **Release APKs** or **AAB (Android App Bundle)** automatically via GitHub Actions, you **MUST** configure the following Secrets in your GitHub Repository settings.

### 1. Add Secrets to GitHub
Go to **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.

**🛠️ Workflow Implementation Details:**
If you inspect the workflow file ([`both-workflow-repo-no-cache.yml`](https://github.com/swaplab-engine/qwik-swaplab-template/blob/main/.github/workflows/both-workflow-repo-no-cache.yml)), you will see exactly how these credentials are passed to the container:

| Secret Name | Description |
| :--- | :--- |
| `KEYSTORE_BASE64` | Your `.jks` or `.keystore` file converted to a Base64 string. |
| `KEYSTORE_PASSWORD` | The password for your Keystore. |
| `KEY_ALIAS` | The alias name of your key. |
| `KEY_PASSWORD` | The password for your specific key alias. |

### 2. How to generate KEYSTORE_BASE64
You cannot upload the binary keystore file directly to GitHub Secrets. You must convert it to a text string first.

**Mac/Linux:**
```bash
base64 -i your-keystore.jks > base64-keystore.txt
# Open base64-keystore.txt, copy the content, and paste it into the Secret value.
```

**Windows (PowerShell):**
```bash
[Convert]::ToBase64String([IO.File]::ReadAllBytes("your-keystore.jks")) | Out-File base64-keystore.txt
```

### 3. 🔍 Transparency: How Secrets are Used (Secure & Ephemeral)
We prioritize security by using **Just-In-Time (JIT) Processing**.

Your signing keys and passwords are handled with strict isolation rules to ensure they cannot be leaked or retrieved:

1.  **Memory-Only:** Your secrets are processed entirely in **Volatile Memory (RAM)**.
2.  **No Disk IO:** We strictly **do not** write your passwords to any persistent configuration files or logs on the server.
3.  **Zero Trace:** The build environment is ephemeral. Once the build process finishes, the isolated container is immediately destroyed, wiping all data from memory.

```yaml
# From the .yml workflow (Inputs):
-e INPUT_KEYSTORE_BASE64=${{ secrets.KEYSTORE_BASE64 }} \
-e INPUT_KEYSTORE_PASSWORD=${{ secrets.KEYSTORE_PASSWORD }} \
-e INPUT_KEY_ALIAS=${{ secrets.KEY_ALIAS }} \
-e INPUT_KEY_PASSWORD=${{ secrets.KEY_PASSWORD }} \
```
* **Security Note (Silent Mode):** To guarantee zero leakage, the GitHub Actions log output is intentionally **restricted**.
    * **Where to watch:** A secure, sanitized log stream is transmitted exclusively to your **SwapLab Live Dashboard**.


---


<br>

<details>
<summary><strong>🔍 Transparency: GitHub Permissions & API Usage (Click to expand)</strong></summary>

<br>


<img width="431" height="741" alt="GitHub-Permissions" src="https://github.com/user-attachments/assets/cfdc1b35-517a-4b9e-9c29-300fd7b93aac" />


In this workflow, SwapLab acts as a **Digital Bridge (Trigger)**. It connects your SwapLab dashboard to your private GitHub Workspace, allowing you to trigger builds that run *inside* your own repository using standard GitHub Actions.

We believe in radical transparency. Here is the exact technical breakdown of why we request specific permissions and which GitHub APIs are triggered:

### 1. 🔑 Authentication
We use **Firebase Authentication (GitHub OAuth)** to verify your identity. We never see, store, or access your GitHub password.
* **Ref:** [Firebase GitHub Auth Documentation](https://firebase.google.com/docs/auth/web/github-auth)

### 2. ⚡ Workflows (Actions: Write)
**Why it's required:**
To act as a "Remote Control" for your build button. This allows the SwapLab Dashboard to start a build or cancel a hanging process.

**API Endpoints Used:**
* **Trigger Build:** `POST /repos/{owner}/{repo}/actions/workflows/{workflow_id}/dispatches`
* **Cancel Build:** `POST /repos/{owner}/{repo}/actions/runs/{run_id}/cancel`
* **Ref:** [GitHub: Manually run a workflow](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/manually-run-a-workflow)

### 3. 📂 Contents (Read & Write)
**Why it's required:** `repository.swaplab.net`

* **(Read) To Check Out Code:**
    This allows the GitHub Actions runner to securely `checkout` your source code into the temporary, isolated build environment so it can be compiled.
* **(Write) To Upload Build Artifacts:**
    This permission supports our **Artifact Storage** feature. If you select the *"GitHub Repository (Releases)"* option, we use this permission to automatically create a new GitHub Release and upload your finished build file (e.g., `.apk` or `.aab`) as an asset to that release.

> **⚠️ Note:** We only use this permission to **Create** releases. We **do not** automate the deletion of your files. Full control to delete old releases or assets remains manually in your hands via:
> `https://github.com/{owner}/{repo}/releases`

**API Tool Used:**
We utilize the official GitHub CLI (`gh api`) within the workflow:
```bash
gh api \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  /repos/OWNER/REPO/releases

```
**🛠️ Workflow Implementation Details:**
If you inspect the workflow file ([`both-workflow-repo-no-cache.yml`](https://github.com/swaplab-engine/qwik-swaplab-template/blob/main/.github/workflows/both-workflow-repo-no-cache.yml)), you will see exactly how these credentials are passed to the container:

* `-e GITHUB_SHA=${{ github.sha }}`: **Unique Release Code.**
    We use the unique Commit ID to tag the release version. This ensures you can trace every APK/AAB back to the exact code change that generated it.
* `-e GITHUB_TOKEN=${{ secrets.GITHUB_TOKEN }}`: **Automatic Token.**
    This is a temporary, auto-generated token provided by GitHub Actions. It is strictly used to authenticate the upload of the artifact back to your repository and expires immediately after the job finishes.



### 4. ℹ️ Metadata (Read-only)
**Why it's required:**
This is a default permission. We use it to read basic information about your repository (like its name and visibility) to display it correctly in your Dashboard list.

</details>

<br>



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