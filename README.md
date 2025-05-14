# Mini Curso de Github

En este curso podras encontrar algunos comandos basicos para que puedas entender el uso de esta herramienta y pueda ser más facil tu desarrollo.

Aquí toda la documentación que debes saber:


## 📌 Introducción a Git

**¿Qué es Git?**  
Es un sistema de control de versiones que te permite llevar el historial de cambios en tus archivos. Ideal para trabajar en equipo y no morir en el intento.

**¿Qué es GitHub?**  
Una plataforma en la nube donde puedes guardar tus repositorios Git y colaborar con otras personas.

**Diferencias:**
| Git         | GitHub                   |
|-------------|--------------------------|
| Herramienta local | Plataforma online |
| Se usa en tu computadora| Se conecta a Git |
| No necesitas internet | Necesita Git para funcionar |

---

## 🧑‍💻 GitHub: Primeros pasos

1. Crea una cuenta en [github.com](https://github.com)
2. Crea tu primer repositorio desde el botón **"New"**
3. Nómbralo, elige si es público o privado y agrega un README si quieres

---

## 🖥️ GitHub Client (Git CLI)

**¿Por qué instalarlo?**  
- Para usar Git desde tu computadora (VSCode, terminal, etc.)
- Para trabajar offline
- Para automatizar cosas

**Instalación:**  
[Descargar Github Client](https://cli.github.com/)

**Autenticación:**  
Para autenticarte necesitarás una vez instalado el gh-client ejecutar el siguiente comando:
```bash
gh auth login
```
Te pedirá que selecciones la forma para iniciar sesión (te recomiendo la que es en la página oficial de GitHub), sigues las indicaciones que te dice y ¡listo!.

---

# 💻 Git

**Instalación:**
[Descargar Git](https://git-scm.com/)

Despues de instalarto te recomiendo que pongas las configuraciones de abajo 👇.

## ⚙️ Configuración Inicial

```bash
git config --global user.name "tu_nombre"
git config --global user.email "tucorreo@gmail.com"
git config --global core.editor "code --wait"
git config --global core.autocrlf true
git config --global -e   # Revisa tu configuración
```

> Esto define tu identidad en todos los proyectos Git que uses en tu compu. También se puede configurar por proyecto (sin `--global`).

---

## 🔧 Comandos básicos de Git

### Crear repositorio

```bash
git init           # Inicia repositorio local
code .             # Abre proyecto en VSCode
```
> `git init` convierte una carpeta común en un repositorio Git.  
> `code .` abre esa carpeta en VSCode (requiere tener VSCode instalado).


### Estado del repositorio

```bash
git status         # Ver archivos modificados
git status -s      # Vista rápida
```
> Muestra qué archivos han cambiado desde el último commit. Muy útil para saber qué vas a subir.

### Agregar y confirmar cambios

```bash
git add .                       # Todos los archivos
git add *.txt                   # Solo archivos .txt
git add archivo.txt             # Un archivo específico
git commit -m "Mensaje"         # Confirmar cambios
git commit                      # Abre editor para mensaje
```
> `add` prepara archivos para el commit.  
> `commit` guarda los cambios como una "foto" del estado del proyecto.

### Guardar cambios sin confirmar (stash)

```bash
git stash           # Guarda los cambios temporalmente
git stash list      # Lista de stashes guardados
git stash apply     # Aplica sin borrar
git stash pop       # Aplica y elimina el stash
git stash push --include-untracked -m "Tu mensaje descriptivo" # PRO 😎 (si necesitas guardar todo (archivos creados, modificados, etc.) para guardar tu progreso y cambiar de rama si necesitas hacer cambios)
```
> Útil cuando tienes cambios pero necesitas cambiar de rama o trabajar en otra cosa sin perder el progreso.

### Comparar cambios

```bash
git diff                    # Cambios no agregados
git diff --staged           # Cambios en staging listos para commit
```
> Compara versiones del archivo actual vs lo que está en staging o ya confirmado.

### Recuperar o eliminar archivos

```bash
git restore archivo.ext                 # Deshacer cambios
git restore --staged archivo.ext        # Sacar del staging
git rm archivo.ext                      # Eliminar y hacer seguimiento
rm archivo.ext                          # Solo eliminar
```
> Te ayuda a volver a una versión anterior o borrar archivos del repo correctamente.

### Renombrar archivos

```bash
mv viejo.ext nuevo.ext          # Renombrar sin seguimiento
git mv viejo.ext nuevo.ext      # Renombrar y seguir en Git
```
> Git detecta cambios si usas `git mv`, así no confunde "eliminado + nuevo archivo".

### Historial de cambios

```bash
git log                   # Ver historial completo
git log --oneline         # Historial resumido
```
> Muestra todos los commits realizados. Con `--oneline` es mucho más legible.

## 🌿 Ramas y trabajo en equipo

```bash
git branch                          # Ver ramas
git checkout master                 # Cambiar a master
git checkout -b feature/nueva       # Crear y cambiar de rama
git merge rama                      # Unir rama actual con otra
```
> Git usa ramas para probar cosas sin romper el proyecto principal.  
> Muy útil para trabajo en equipo o pruebas.

## ☁️ Subir y bajar del repositorio remoto

```bash
git remote add origin https://github.com/usuario/repositorio.git
git remote -v                             # Ver URL remota
git remote set-url origin nueva_url.git  # Cambiar URL
git push -u origin main                  # Subir primera vez
git push                                 # Subir cambios
git pull                                 # Traer cambios del remoto
```
> Aquí es donde Git y GitHub se conectan.  
> `push` sube, `pull` baja cambios.

---

## 😨 Problemas frecuentes al desarrollar.

| 🧩 Problema | 🛠️ Solución | 💬 Explicación rápida |
|------------|-------------|------------------------|
| Me equivoqué de rama al hacer commit, quiero conservar los cambios | `git reset --soft HEAD~1` | Quita el último commit pero mantiene los cambios listos para re-commitear |
| Quiero deshacer el último commit pero seguir editando los archivos | `git reset --mixed HEAD~1` | Borra el commit y saca los archivos del staging |
| Quiero borrar el commit y todo lo que cambié | `git reset --hard HEAD~1` | ⚠️ Elimina commit y archivos modificados sin recuperación |
| Subí un commit por error y quiero quitarlo del repo | `git reset --hard HEAD~1` + `git push --force` | ⚠️ Reescribe el historial remoto, cuidado en equipos |
| Quiero revertir cambios de un commit sin borrarlo | `git revert <id>` | Crea un nuevo commit que revierte otro, ideal para colaborar |
| Quiero que mi repo local esté igual al remoto | `git fetch origin` + `git reset --hard origin/main` | Borra todo localmente y clona desde el remoto |

---

## 💡 ProTip: Evita hacer commit en ramas protegidas

Puedes crear un alias para asegurarte de no hacer commits por error en ramas importantes como `main`, `master` o `dev`.

```bash
git config --global alias.safe-commit '!f() { \
branch=$(git rev-parse --abbrev-ref HEAD); \
if [ "$branch" = "main" ] || [ "$branch" = "master" ] || [ "$branch" = "dev" ]; then \
echo "Estás en la rama protegida: $branch"; \
read -p "¿Estás seguro de que quieres hacer commit? (y/n): " response; \
if [ "$response" != "y" ]; then \
echo "Commit cancelado."; \
exit 1; \
fi; \
fi; \
git commit "$@"; \
}; f'
```

> Luego, usa `git safe-commit` en lugar de `git commit` para tener esa protección.

---

## 🚫 .gitignore

Evita subir cosas como contraseñas, logs o carpetas pesadas.

Ejemplo:
```
.env
node_modules/
*.log
```

---

## 🧪 Ejercicios prácticos por módulo

Te recomiendo hacer estos ejercicios para que puedas entender un poco mas y lo puedas poner en practica.

### 📁 Repositorio y configuración
- [ ] Crea una carpeta nueva y conviértela en repositorio con `git init`
- [ ] Configura tu nombre y correo con `git config`
- [ ] Abre el proyecto en VSCode con `code .`

### ✏️ Primeros commits
- [ ] Crea un archivo `index.html` con cualquier contenido
- [ ] Haz `git add` y `git commit`
- [ ] Modifica el archivo y usa `git diff` para ver los cambios

### 🧼 Stash
- [ ] Modifica el archivo pero **no hagas commit**
- [ ] Usa `git stash` para guardar los cambios y cambia hacia otra rama.
- [ ] Vuelve a tu rama en donde hiciste el stash y recupera los cambios con `git stash pop`

### 🌿 Ramas y cambios
- [ ] Crea una rama `feature/prueba`
- [ ] Modifica algo en esa rama y haz commit
- [ ] Cambia a `main`, modifica algo diferente y haz commit
- [ ] Intenta hacer `git merge feature/prueba` en `main`

### ☁️ GitHub y remoto
- [ ] Crea un repositorio en GitHub
- [ ] Conéctalo con tu proyecto con `git remote add origin`
- [ ] Usa `git push -u origin main` para subir tu repo
- [ ] Modifica algo desde GitHub (web) y usa `git pull` para traerlo localmente

**Puedes utilizar este repo para hacer las practicas, por defecto ya viene un html con el cual puedes practicar. Ya sea que clones este repositorio o lo descargues con ZIP. Incluso si lo prefieres, puedes hacer un fork :)**
