# 📌 Pipeline CI Reutilizable para Pruebas Automatizadas

## 📋 Descripción
Este es un **workflow reutilizable de GitHub Actions** diseñado para automatizar la ejecución de pruebas en diferentes repositorios. Permite que cualquier repositorio público ejecute pruebas utilizando este workflow, garantizando coherencia y eficiencia en los procesos de CI/CD.

## ⚙️ Cómo Funciona
Este pipeline:
- **Clona el repositorio** donde se encuentran las pruebas.
- **Configura Java** (versión configurable).
- **Instala dependencias** utilizando un comando proporcionado por el usuario.
- **Ejecuta pruebas automatizadas** con un comando especificado por el usuario.

## 📂 Ubicación del Archivo Workflow
El workflow reutilizable se encuentra en este repositorio en:
```
.github/workflows/reusable-ci-tests.yml
```

## 🚀 Uso en Otro Repositorio
Para usar este pipeline en un repositorio diferente, crea un nuevo archivo de workflow de GitHub Actions dentro de:
```
.github/workflows/run-tests.yml
```
Y agrega el siguiente contenido:

```yaml
name: Ejecutar Pruebas con Pipeline Reutilizable

on:
  push:
    branches:
      - master  # Cambiar si es necesario

jobs:
  call-reusable-workflow:
    uses: charliesan16/<repo-del-pipeline>/.github/workflows/reusable-ci-tests.yml@master
    with:
      repository: "<repo-con-codigo-de-pruebas>"  # Nombre del repositorio de pruebas
      java-version: "17"  # Versión de Java (por defecto: 11)
      command-install: "npm install"  # Instalar dependencias
      command-execute: "npm test"  # Ejecutar pruebas
```

## 📌 Parámetros
| Parámetro         | Obligatorio | Descripción |
|------------------|-------------|-------------|
| `repository`      | ✅ Sí       | Nombre del repositorio que contiene el código de prueba. |
| `java-version`    | ❌ No       | Versión de Java a utilizar (por defecto: `11`). |
| `command-install` | ✅ Sí       | Comando para instalar dependencias. |
| `command-execute` | ✅ Sí       | Comando para ejecutar las pruebas. |

## ✅ Requisitos Previos
- El repositorio **que llama al pipeline debe ser público**.
- El **pipeline debe estar en un repositorio público**.
- El archivo workflow (`run-tests.yml`) debe colocarse en `.github/workflows/`.

## 🎯 Ejemplo de Ejecución
Una vez configurado, este pipeline reutilizable ejecutará automáticamente las pruebas en **cada push a la rama `master`** en el repositorio que lo utiliza.

🚀 **¡Esto garantiza un proceso de pruebas CI/CD eficiente y escalable!**

