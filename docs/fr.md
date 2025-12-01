# Angular Boiler room Windows


# 🔰 1) OBJECTIF DE LA PROCÉDURE

Cette procédure installe un environnement **propre, stable et complet** pour développer et déployer une application Angular.
On part d’un Windows vide et on met en place : éditeur, gestionnaires de paquets, Git, SSH, Angular, Netlify, Node, Volta, VSCodium + Marketplace.

---

# 🟦 2) OUVERTURE DES PRIVILÈGES

Ouvrir **PowerShell en administrateur**, indispensable pour exécuter les commandes système.

---

# 🟧 3) INSTALLATION CHOCOLATEY

Chocolatey est le gestionnaire de paquets Windows utilisé pour automatiser toutes les installations.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

---

# 🟩 4) INSTALLATION VSCODIUM

Éditeur de code léger, basé sur VSCode, sans télémétrie.

```powershell
choco install vscodium
```

---

# 🟩 5) ACTIVATION DU MARKETPLACE MICROSOFT

Permet d’utiliser les extensions officielles, absentes par défaut dans VSCodium.

```powershell
$settingsPath = "$env:APPDATA\VSCodium\User\settings.json"
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

# 🟦 6) INSTALLATION GIT

Outil central pour versionner et pousser ton projet vers GitHub.

```powershell
choco install git
```

---

# 🟦 7) INSTALLATION ICÔNES VSCODIUM

Améliore la lisibilité des fichiers dans l’éditeur.

Extension à installer :

```
vscode-icons-team
```

---

# 🟥 8) INSTALLATION WINGET

Gestionnaire de paquets Microsoft.

Méthode rapide :

```powershell
choco install winget
```

Alternative via Microsoft (si besoin d’une version récente) :
Télécharger le fichier `.msixbundle` ici :
[https://github.com/microsoft/winget-cli/releases/tag/v1.12.350](https://github.com/microsoft/winget-cli/releases/tag/v1.12.350)

donc ce fichier 

```
Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle

```

---

# 🟫 9) INSTALLATION VOLTA + NODE

Volta permet une gestion propre, isolée et stable de Node et npx.

```powershell
winget install Volta.Volta
volta install node
```

---

# 🟨 10) CRÉATION DE L’ESPACE DE TRAVAIL

Dossier où seront stockés tes projets.

```powershell
cd $HOME
mkdir WORK
cd WORK
```

---

# 🟥 11) CRÉATION DU DÉPÔT GITHUB

Aller sur GitHub → créer un repo privé nommé :
**angular_boiler_room_windows**

---

# 🟫 12) GÉNÉRATION DE LA CLÉ SSH

Authentification sécurisée pour GitHub.

```powershell
ssh-keygen -t ed25519 -C "robot@timetraveler.com"
```

Afficher la clé :

```powershell
cat ~/.ssh/id_ed25519.pub
```

Ajouter sur GitHub → *Settings* → *SSH Keys*.

---

# 🟦 13) CONFIGURATION GIT (IDENTITÉ)

Nécessaire pour les commits.

```powershell
git config --global user.name "robot"
git config --global user.email "robot@timetraveler.com"
```

---

# 🟧 14) CRÉATION DU PROJET ANGULAR

Génère la structure du projet.

```powershell
npx @angular/cli@20 new frontend --standalone=false
```

Réponses aux questions :

* dir : **non**
* autres questions : **non**
* style : **SCSS**

Puis :

```powershell
cd frontend
```

---

# 🟩 15) CONNEXION NETLIFY

Permet de déployer le projet sur Netlify.

```powershell
npx --yes netlify-cli@latest login
```

→ Attendre l’ouverture du lien
→ Autoriser dans Netlify (compte déjà créé)

---

# 🟦 16) BUILD ANGULAR

Compile le projet.

```powershell
npx ng build
```

---

# 🟦 17) DÉPLOIEMENT NETLIFY

### Déploiement preview :

```powershell
npx --yes netlify-cli@latest deploy
```

### Déploiement production :

```powershell
npx --yes netlify-cli@latest deploy --prod
```

---

# 🟩 18) TEST LOCAL DU PROJET ANGULAR

Lance un serveur de développement.

```powershell
npx ng s
```

Accès :
[http://localhost:4200](http://localhost:4200)
