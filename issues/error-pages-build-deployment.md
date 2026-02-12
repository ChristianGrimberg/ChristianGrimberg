---

Durante la ejecución del job pages-build-deployment de GitHub Actions (ver logs: https://github.com/ChristianGrimberg/ChristianGrimberg/actions/runs/21931311677/job/63335643517), ocurre el siguiente error:

```
Conversion error: Jekyll::Converters::Scss encountered an error while converting 'assets/css/style.scss':
No such file or directory @ dir_chdir0 - /github/workspace/docs
```

**Causa:**
La acción intenta acceder al directorio `/docs`, pero este no existe en el repositorio. Esto provoca que el compilador de Jekyll falle durante la conversión del archivo SCSS.

**Solución propuesta:**
1. Si el sitio debe construirse desde la carpeta `docs`:
   - Crear el directorio y un archivo base:
     ```bash
     mkdir docs
     echo "# Bienvenido" > docs/index.md
     ```
   - Añadir contenido relevante en la carpeta para permitir el correcto despliegue.

2. Si el sitio no debería usar la carpeta `docs`:
   - Revisar el archivo `_config.yml` y la configuración de la acción para asegurarse de que el path de origen sea el correcto y no dependa de `/docs`.

**Recomendación:**
Por favor, revisar y aplicar la solución que corresponda según la estructura del proyecto.

---