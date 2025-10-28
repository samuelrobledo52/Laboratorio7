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



---

## 🧪 Pruebas realizadas
**Archivo:** `prueba.txt` (≈ 3.1 MB, 200 000 líneas)  
**Bloque:** 1 MiB  
**Sistema:** Ubuntu WSL — Intel i7, 8 hilos lógicos

| Prueba | Hilos | Archivo salida | Tiempo (s) |
|:------:|:------:|:---------------|:-----------:|
| 1 | 1 hilo | `p1.pzip` | 0.027 |
| 2 | 4 hilos | `p4.pzip` | 0.008 |
| 3 | 8 hilos | `p8.pzip` | 0.009 |

> Los tiempos se midieron con `std::chrono::high_resolution_clock`.

---

## 📊 Resultados

### Relación de compresión
| Archivo | Tamaño original | Tamaño comprimido | Relación |
|:---------|:----------------|:------------------|:----------|
| `prueba.txt` | 3.1 MB | 2.6 MB | 0.84 |

- Compresión con 4 hilos → **3.3× más rápida** que con 1 hilo.  
- Descompresión promedio ≈ **0.004 s**.  
- Verificación de integridad:

```bash
diff -s prueba.txt restaurado.txt
# → Files are identical
