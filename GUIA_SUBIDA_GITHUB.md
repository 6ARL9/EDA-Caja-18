# Guía paso a paso para subir el proyecto a GitHub

Esta guía contiene **dos rutas** para publicar tu repositorio en GitHub. Elige la que más te acomode.

> Tu usuario de GitHub: `6ARL9`
> Nombre del repositorio: `EDA-Caja-18`
> URL final: `https://github.com/6ARL9/EDA-Caja-18`

---

## Ruta A — Subida con Git desde la terminal (recomendada)

### Paso 1. Crear el repositorio vacío en GitHub

1. Entra a https://github.com/new
2. Completa los campos:
   - **Repository name:** `EDA-Caja-18`
   - **Description:** `Análisis exploratorio de datos (EDA) sobre datasets pseudonimizados del sistema P18 (Caja 18) y subsistemas asociados. 7 notebooks Jupyter con metodología reproducible.`
   - **Visibility:** Public
   - **NO marques** "Add a README", "Add .gitignore" ni "Choose a license" (ya los creamos localmente).
3. Click en **Create repository**.

### Paso 2. Inicializar Git en tu carpeta local

Abre una terminal **PowerShell o CMD** en `C:\Users\Dumpeal\Documents\Proyectos Python` y ejecuta los comandos en orden:

```bash
# 1. Inicializar repositorio
git init

# 2. Configurar tu identidad (si no lo has hecho antes)
git config user.name "Alexis Rossel Leal"
git config user.email "alexis.rossel.leal@gmail.com"

# 3. Verificar qué archivos se incluirán (los CSV deben quedar excluidos)
git status

# 4. Añadir todos los archivos (excepto los del .gitignore)
git add .

# 5. Primer commit
git commit -m "Initial commit: 7 notebooks EDA + documentación profesional"

# 6. Renombrar la rama principal a 'main'
git branch -M main

# 7. Conectar con el repositorio remoto en GitHub
git remote add origin https://github.com/6ARL9/EDA-Caja-18.git

# 8. Subir todo a GitHub
git push -u origin main
```

> En el paso 8, GitHub te pedirá autenticación. Si nunca lo has hecho, te recomiendo configurar **GitHub CLI** (`gh auth login`) o usar un **Personal Access Token (PAT)** desde https://github.com/settings/tokens.

### Paso 3. Verificar

Visita https://github.com/6ARL9/EDA-Caja-18 y confirma que:

- El README se renderiza correctamente con badges, tablas y emojis.
- Los 7 notebooks aparecen y GitHub los muestra renderizados al hacer click.
- `LICENSE` aparece marcada como MIT.
- **Los archivos `.csv` NO están subidos** (deben estar excluidos por el `.gitignore`).

---

## Ruta B — Subida manual desde la web de GitHub (sin Git)

Útil si no tienes Git instalado.

### Paso 1. Crear el repositorio vacío en GitHub

Igual que en la Ruta A, paso 1.

### Paso 2. Subir archivos por la web

1. En la página recién creada del repositorio, click en **uploading an existing file** (link al centro de la página).
2. Arrastra **TODOS los archivos de tu carpeta `Proyectos Python`** EXCEPTO los `.csv`. Asegúrate de incluir:
   - Los 7 notebooks `EDA_*.ipynb`
   - `README.md`
   - `requirements.txt`
   - `.gitignore`
   - `LICENSE`
   - `GUIA_SUBIDA_GITHUB.md` (opcional, puedes excluirlo si no quieres que aparezca)
   - La carpeta `docs/` (con `descripcion_datasets.md`)
   - La carpeta `data/` (vacía con `.gitkeep`)
3. Escribe un mensaje de commit: `Initial commit: 7 notebooks EDA + documentación profesional`.
4. Click en **Commit changes**.

> **Importante:** la subida web no respeta `.gitignore`. Si arrastras los CSV por error, quedarán expuestos. Revisa cuidadosamente lo que subes.

---

## Después de subir

### Personaliza la página de tu repositorio

1. Click en el ícono de engranaje (⚙️) junto a "About" en la página principal del repo.
2. Añade:
   - **Description:** `Análisis exploratorio de datos (EDA) sobre datasets pseudonimizados del sistema P18 (Caja 18) y subsistemas asociados.`
   - **Website:** déjalo vacío o pon tu LinkedIn.
   - **Topics (etiquetas):** `python`, `pandas`, `jupyter-notebook`, `data-analysis`, `eda`, `data-visualization`, `seaborn`, `matplotlib`, `data-science`, `chile`.

### Comparte el enlace

`https://github.com/6ARL9/EDA-Caja-18`

### Próximos pasos sugeridos

- Añade un GIF o screenshot de uno de los notebooks renderizados.
- Crea un *release* (`v1.0.0`) cuando estés conforme.
- Considera añadir GitHub Pages para publicar los notebooks como HTML estático.

---

## Solución de problemas frecuentes

| Problema | Solución |
|----------|----------|
| `git: command not found` | Instala Git desde https://git-scm.com/download/win. |
| Error de autenticación al hacer `push` | Usa `gh auth login` (GitHub CLI) o un Personal Access Token. |
| El README no se ve bien | Asegúrate de que el archivo se llama exactamente `README.md` (mayúsculas correctas). |
| Subí un CSV por error | Bórralo con `git rm <archivo.csv>`, luego `git commit -m "Remove CSV"` y `git push`. |
| Quiero cambiar la URL del remote | `git remote set-url origin <nueva-url>`. |
