# 🧩 Laboratorio 7 — Compresión y Descompresión Paralela

**Autor:** Samuel Robledo (241282)  
**Curso:** Microprocesadores  
**Entorno:** Ubuntu (WSL) · C++17 · pthreads · zlib  

---

## 🧠 Objetivo
Implementar y analizar un compresor y descompresor paralelo en **C++** utilizando **pthread** y la biblioteca **zlib**, evaluando el impacto del número de hilos en el rendimiento.

---

## ⚙️ Descripción del programa
El programa divide el archivo de entrada en **bloques de 1 MiB** y asigna cada bloque a un hilo para compresión concurrente.

### Flujo de ejecución:
1. Lectura del archivo completo.
2. División en bloques (`BlockIn`).
3. Compresión en paralelo con `compress2` de zlib.
4. Escritura del contenedor **PZIP** con metadatos por bloque.
5. Descompresión paralela con `uncompress`.

### Formato del contenedor PZIP
