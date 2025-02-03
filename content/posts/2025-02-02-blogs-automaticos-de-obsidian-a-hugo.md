---
title: Automatizando la Publicación de Blogs de Obsidian a Hugo
date: 2025-02-02
---

Disclaimer:  99.9% AI written. I really didn't want to write the documentation for this one. Fyi this one is also in spanish. ALSOO, this is heavily inspired by Hardware Chuck's go at it, pls check out his yt video on the topic [I started a blog.....in 2024 (why you should too)](https://www.youtube.com/watch?v=dnE7c0ELEH8)
# 🚀 Automatizando la Publicación de Blogs de Obsidian a Hugo

Si utilizas **Obsidian** para escribir tus notas y **Hugo** para tu sitio web, puede ser tedioso copiar manualmente cada nueva publicación e imagen. Para solucionar esto, he creado un flujo de trabajo automatizado usando **PowerShell y Python** que copia tus archivos y ajusta los enlaces de imágenes para que sean compatibles con Hugo. 💡

---

# Pre-requisitos

1. Configurar obsidian para que almancene las imagenes en un solo lugar
![](/personal-website/images/20250202185104.png)

2. Desabilita los wikilinks!! Esto nos salva muchos dolores de cabez
![](/personal-website/images/20250202185236.png)

# 🛠️ ¿Qué hace este sistema?

1. **Copia los archivos Markdown** de Obsidian a Hugo.
2. **Copia las imágenes** asociadas a los posts.
3. **Corrige los enlaces de imágenes** en los archivos Markdown para que se visualicen correctamente en Hugo.
4. **Todo con un solo comando.**

# 📜 1️⃣ Script `robocopy-posts-and-images.ps1`

Este script usa **Robocopy** para copiar las publicaciones de Obsidian a Hugo, junto con las imágenes asociadas.

```bash
# Copiar los posts de Obsidian a Hugo
robocopy "C:\ALMACENAMIENTO\acer\personal-website\blog-posts" "C:\Users\crrvg\w11-codebases\personal-website\content\posts" /MIR /Z /W:5 /R:3

# Copiar imágenes de Obsidian a Hugo
robocopy "C:\ALMACENAMIENTO\acer\personal-website\images" "C:\Users\crrvg\w11-codebases\personal-website\static\images" /MIR /Z /W:5 /R:3
```

✅ **Explicación:**

- `/MIR`: Mantiene sincronizados los directorios (copia nuevas y elimina las que ya no están en el origen).
- `/Z`: Permite reanudar copias interrumpidas.
- `/W:5` y `/R:3`: Reduce tiempos de espera entre intentos fallidos.

# 🐍 2️⃣ Script `hugo-obsidian-image-copier.py`

Este script Python busca imágenes en los archivos Markdown y modifica sus rutas para que sean compatibles con Hugo.

```python
import os
import re
# Rutas
hugo_blog_dir = r"C:\Users\crrvg\w11-codebases\personal-website\content\posts"
# 🔹 Modificar los enlaces a imágenes en los Markdown
for filename in os.listdir(hugo_blog_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(hugo_blog_dir, filename)

        with open(filepath, "r", encoding="utf-8") as file:
            content = file.read()

        # Encontrar imágenes en el formato `![](/personal-website/images/test%201.png)`
        images = re.findall(r'!\[\]\(([^)]+\.png)\)', content)

        for image in images:
            new_image_path = f"/personal-website/images/{image}"
            content = content.replace(f"![]({image})", f"![]({new_image_path})")

        # Guardar cambios en el archivo Markdown
        with open(filepath, "w", encoding="utf-8") as file:
            file.write(content)

print("✅ Links de imágenes en Markdown modificados para Hugo.")
```

✅ **Explicación:**
- **Busca imágenes** en los archivos `.md`.
- **Corrige las rutas** para que Hugo pueda encontrarlas correctamente en la carpeta `static/images`.

# 🔁 3️⃣ Script Final `automated-obsidian-hugo-blog.ps1`

Este script une todo el proceso en un solo comando:
```bash
# Definir rutas de los scripts
$robocopyScript = "C:\Users\crrvg\w11-codebases\programming-journey\02.02.2025\robocopy-posts-and-images.ps1"
$pythonExecutable = "C:/Users/crrvg/w11-codebases/programming-journey/.venv/Scripts/python.exe"
$pythonScript = "C:/Users/crrvg/w11-codebases/programming-journey/02.02.2025/hugo-obsidian-image-copier.py"

# Ejecutar el script de robocopy
Write-Output "🚀 Ejecutando copia de posts e imágenes..."
& $robocopyScript

# Ejecutar el script de Python
Write-Output "🐍 Ejecutando script de conversión de imágenes..."
& $pythonExecutable $pythonScript

Write-Output "✅ Links de imágenes en Markdown modificados para Hugo."
```

# 🚀 ¿Cómo Ejecutarlo?

Solo necesitas correr este comando en PowerShell:

```bash
.\automated-obsidian-hugo-blog.ps1
```

🔥 ¡Listo! Tus posts e imágenes estarán sincronizados con Hugo sin esfuerzo. 🚀

# Code!
Puedes revisar el codigo en my [programming journey](https://github.com/NotYetFound404/programming-journey)

Casi me olvido, `pip freeze > requirements.txt` siempreee. Comparto las librerias que utilicé

Este proyecto en especifico por ahora está en [02.02.2025](https://github.com/NotYetFound404/programming-journey/tree/main/02.02.2025), tal vez luego este enlace se rompa. If so, refer to the programming journey repo instead