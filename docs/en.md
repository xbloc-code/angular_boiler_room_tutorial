# 🔰 1) PURPOSE OF THE PROCEDURE

This procedure installs a **clean, stable, and complete** environment for developing and deploying an Angular application.
We start from an empty Windows system and set up: editor, package managers, Git, SSH, Angular, Netlify, Node, Volta, VSCodium + Marketplace.

---

# 🟦 2) ELEVATING PRIVILEGES

Open **PowerShell as Administrator**, required to execute system-level commands.

---

# 🟧 3) INSTALLING CHOCOLATEY

Chocolatey is the Windows package manager used to automate all installations.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

---

# 🟩 4) INSTALLING VSCODIUM

Lightweight code editor based on VSCode, without telemetry.

```powershell
choco install vscodium
```

---

# 🟩 5) ENABLING THE MICROSOFT MARKETPLACE

Allows access to official extensions, not included by default in VSCodium.

```powershell
$settingsPath = "$env:APPDATA\\VSCodium\\User\\settings.json"
$newDir = Split-Path $settingsPath
if (-not (Test-Path $newDir)) { New-Item -ItemType Directory -Path $newDir -Force | Out-Null }

$json = @'
{
    "extensionsGallery": {
        "serviceUrl": "https://marketplace.visualstudio.com/_apis/public/gallery",
        "cacheUrl": "https://vscode.blob.core.windows.net/gallery/index",
        "itemUrl": "https://marketplace.visualstudio.com/items"
    },
    "telemetry.telemetryLevel": "off",
    "update.mode": "none"
}
'@

$json | Out-File -FilePath $settingsPath -Encoding utf8 -Force
```

---

# 🟦 6) INSTALLING GIT

Central tool for versioning and pushing your project to GitHub.

```powershell
choco install git
```

---

# 🟦 7) INSTALLING VSCODIUM ICONS

Improves file readability inside the editor.

Extension to install:

```
vscode-icons-team
```

---

# 🟥 8) INSTALLING WINGET

Microsoft’s package manager.

Quick method:

```powershell
choco install winget
```

Alternative via Microsoft (if a more recent version is needed):
Download the `.msixbundle` here:
[https://github.com/microsoft/winget-cli/releases/tag/v1.12.350](https://github.com/microsoft/winget-cli/releases/tag/v1.12.350)

The file is:

```
Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle
```

---

# 🟫 9) INSTALLING VOLTA + NODE

Volta provides clean, isolated, and stable management of Node and npx.

```powershell
winget install Volta.Volta
volta install node
```

---

# 🟨 10) CREATING THE WORKSPACE

Folder where your projects will be stored.

```powershell
cd $HOME
mkdir WORK
cd WORK
```

---

# 🟥 11) CREATING THE GITHUB REPOSITORY

Go to GitHub → create a private repository named:
**angular_boiler_room_windows**

---

# 🟫 12) GENERATING THE SSH KEY

Secure authentication for GitHub.

```powershell
ssh-keygen -t ed25519 -C "robot@timetraveler.com"
```

Show the key:

```powershell
cat ~/.ssh/id_ed25519.pub
```

Add it on GitHub → *Settings* → *SSH Keys*.

---

# 🟦 13) CONFIGURING GIT (IDENTITY)

Required for commits.

```powershell
git config --global user.name "robot"
git config --global user.email "robot@timetraveler.com"
```

---

# 🟧 14) CREATING THE ANGULAR PROJECT

Generates the project structure.

```powershell
npx @angular/cli@20 new frontend --standalone=false
```

Answers to the prompts:

* dir: **no**
* other questions: **no**
* style: **SCSS**

Then:

```powershell
cd frontend
```

---

# 🟩 15) CONNECTING TO NETLIFY

Allows you to deploy the project on Netlify.

```powershell
npx --yes netlify-cli@latest login
```

→ Wait for the link to open
→ Authorize in Netlify (account already created)

---

# 🟦 16) BUILD ANGULAR

Compiles the project.

```powershell
npx ng build
```

---

# 🟦 17) NETLIFY DEPLOYMENT

### Preview deployment:

```powershell
npx --yes netlify-cli@latest deploy
```

### Production deployment:

```powershell
npx --yes netlify-cli@latest deploy --prod
```

---

# 🟩 18) LOCAL TEST OF THE ANGULAR PROJECT

Starts a development server.

```powershell
npx ng s
```

Access:
[http://localhost:4200](http://localhost:4200)
