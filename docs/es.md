# 🔰 1) OBJETIVO DEL PROCEDIMIENTO

Este procedimiento instala un entorno **limpio, estable y completo** para desarrollar y desplegar una aplicación Angular.
Partimos de un sistema Windows vacío y configuramos: editor, gestores de paquetes, Git, SSH, Angular, Netlify, Node, Volta, VSCodium + Marketplace.

---

# 🟦 2) APERTURA DE PRIVILEGIOS

Abrir **PowerShell como administrador**, necesario para ejecutar comandos a nivel del sistema.

---

# 🟧 3) INSTALACIÓN DE CHOCOLATEY

Chocolatey es el gestor de paquetes de Windows utilizado para automatizar todas las instalaciones.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

---

# 🟩 4) INSTALACIÓN DE VSCODIUM

Editor de código ligero basado en VSCode, sin telemetría.

```powershell
choco install vscodium
```

---

# 🟩 5) ACTIVACIÓN DEL MARKETPLACE DE MICROSOFT

Permite usar las extensiones oficiales que no vienen incluidas por defecto en VSCodium.

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

# 🟦 6) INSTALACIÓN DE GIT

Herramienta central para versionar y subir tu proyecto a GitHub.

```powershell
choco install git
```

---

# 🟦 7) INSTALACIÓN DE ICONOS PARA VSCODIUM

Mejora la legibilidad de los archivos en el editor.

Extensión a instalar:

```
vscode-icons-team
```

---

# 🟥 8) INSTALACIÓN DE WINGET

Gestor de paquetes de Microsoft.

Método rápido:

```powershell
choco install winget
```

Alternativa desde Microsoft (si necesitas una versión más reciente):
Descargar este archivo `.msixbundle`:

```
Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle
```

Desde:
[https://github.com/microsoft/winget-cli/releases/tag/v1.12.350](https://github.com/microsoft/winget-cli/releases/tag/v1.12.350)

---

# 🟫 9) INSTALACIÓN DE VOLTA + NODE

Volta permite una gestión limpia, aislada y estable de Node y npx.

```powershell
winget install Volta.Volta
volta install node
```

---

# 🟨 10) CREACIÓN DEL ESPACIO DE TRABAJO

Carpeta donde se guardarán tus proyectos.

```powershell
cd $HOME
mkdir WORK
cd WORK
```

---

# 🟥 11) CREACIÓN DEL REPOSITORIO EN GITHUB

Entrar a GitHub → crear un repositorio privado llamado:
**angular_boiler_room_windows**

---

# 🟫 12) GENERACIÓN DE LA CLAVE SSH

Autenticación segura para GitHub.

```powershell
ssh-keygen -t ed25519 -C "robot@timetraveler.com"
```

Mostrar la clave:

```powershell
cat ~/.ssh/id_ed25519.pub
```

Agregar en GitHub → *Settings* → *SSH Keys*.

---

# 🟦 13) CONFIGURACIÓN DE GIT (IDENTIDAD)

Necesario para los commits.

```powershell
git config --global user.name "robot"
git config --global user.email "robot@timetraveler.com"
```

---

# 🟧 14) CREACIÓN DEL PROYECTO ANGULAR

Genera la estructura del proyecto.

```powershell
npx @angular/cli@20 new frontend --standalone=false
```

Respuestas a las preguntas:

* dir: **no**
* otras preguntas: **no**
* estilo: **SCSS**

Luego:

```powershell
cd frontend
```

---

# 🟩 15) CONEXIÓN A NETLIFY

Permite desplegar el proyecto en Netlify.

```powershell
npx --yes netlify-cli@latest login
```

→ Esperar la apertura del enlace
→ Autorizar en Netlify (cuenta ya creada)

---

# 🟦 16) BUILD DE ANGULAR

Compila el proyecto.

```powershell
npx ng build
```

---

# 🟦 17) DESPLIEGUE EN NETLIFY

### Despliegue en modo preview:

```powershell
npx --yes netlify-cli@latest deploy
```

### Despliegue en producción:

```powershell
npx --yes netlify-cli@latest deploy --prod
```

---

# 🟩 18) PRUEBA LOCAL DEL PROYECTO ANGULAR

Inicia un servidor de desarrollo.

```powershell
npx ng s
```

Acceso:
[http://localhost:4200](http://localhost:4200)

---


Install tailwind 
```
npm install tailwindcss @tailwindcss/postcss postcss --force
```

add in styles.scss

```
@import "tailwindcss";

```


make page 

```
 npx ng generate component pages/drawing --style=scss
```