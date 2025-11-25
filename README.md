# Data Structure Guided Decision System

**Equipo:**
María Fernanda Sierra Guzmán - 179422
Axel Chávez Hernández - 180999
Diego Bedolla Carrillo - 181439

**Curso:** Data Structure Course
**Fecha:** Noviembre 2025

## 📖 Overview
Este proyecto implementa un **Sistema de Decisión Guiada** diseñado para ayudar a desarrolladores y estudiantes a seleccionar la estructura de datos más adecuada para un problema específico.

A través de una serie de 6 a 8 preguntas interactivas sobre la naturaleza de los datos y los requisitos de rendimiento, el sistema analiza las respuestas y recomienda una estructura (como Arrays, Linked Lists, BSTs, Grafos, etc.).

El sistema no solo da el nombre de la estructura, sino que proporciona un contexto educativo completo:
1.  **Racional:** ¿Por qué se eligió esta estructura?
2.  **Ilustración:** Representación visual (Arte ASCII).
3.  **Pseudocódigo:** Algoritmos principales con complejidad Big-O.
4.  **Ejemplo Real:** Un caso de uso práctico basado en tareas académicas.

## ✨ Features
* **Lógica de Decisión Robusta:** Distingue entre estructuras lineales, jerárquicas y relacionales.
* **Cobertura Amplia:** Soporta Arrays, Listas (Simples/Circulares), Stacks, Queues, BST, AVL, Heaps y Grafos.
* **Visualización Integrada:** Muestra diagramas ASCII directamente en la consola.
* **Run-Anywhere:** Escrito en C estándar, compatible con Windows, Linux y macOS.
* **Script de Automatización:** Incluye `run.bat` para ejecución rápida en Windows.

## 📂 Project Structure
La estructura del repositorio sigue los estándares de ingeniería de software:

* `/src`: Código fuente (`main.c`, `results.c`, `results.h`).
* `/docs`: Documentación de la lógica de decisión y el cuestionario.
* `/diagrams`: Recursos visuales y capturas de demostración.
* `/example`: Documentación detallada del ejemplo de uso ("Homework Example").
* `/tests`: Casos de prueba y planes de validación.

## 🚀 Run Instructions (Native)

### Prerrequisitos
* Compilador **GCC** instalado (MinGW en Windows, o build-essential en Linux).

### Opción A: Ejecución Rápida (Windows)
Simplemente haz doble clic en el archivo `run.bat` ubicado en la raíz del proyecto. Esto compilará y ejecutará el programa automáticamente.

### Opción B: Compilación Manual (Cualquier S.O.)
Abre tu terminal en la carpeta raíz del proyecto y ejecuta:

**1. Compilar:**
```bash
gcc src/main.c src/results.c -o decision_system
