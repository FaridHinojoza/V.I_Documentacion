# V.I_Documentacion — Investigación Científica y Manuscrito Académico (ESPE)

Repositorio oficial de investigación científica, revisión sistemática **PRISMA 2020** y redacción del manuscrito académico en formato **Springer LNCS**:
> **"Evaluación de cercos virtuales dinámicos para la detección de merodeo peatonal y trayectorias recurrentes mediante visión artificial en videovigilancia inteligente"**  
> **Autores:** Denilson Celi y Raúl Hinojoza  
> **Institución:** Universidad de las Fuerzas Armadas ESPE (Sangolquí, Ecuador)

---

## 1. Arquitectura de Contexto Compartido y Optimización de Tokens (Antigravity)

Este proyecto está conectado de forma remota al Hub central de skills (**[`Shairr/Skills-proyectos`](https://github.com/Shairr/Skills-proyectos.git)**) mediante el submódulo `.agents/hub` y se encuentra **100 % aislado** del repositorio de código del aplicativo (**[`FaridHinojoza/V.I`](https://github.com/FaridHinojoza/V.I.git)**).

* **Reglas Globales (`AGENTS.md`):** Fuerza el cumplimiento estricto de las normas de redacción académica ESPE (prosa continua en Introducción, párrafos en 4 pasos en Trabajos Relacionados, cero emojis, cero dos puntos/paréntesis en prosa y corpus cerrado).
* **Filtrado de Skills (`.agents/skills.json`):** Carga exclusivamente `redaccion-cientifica-espe` y `sincronizacion-contexto-vi`.
* **Auto-Sincronización al Iniciar Sesión (`.agents/hooks.json`):** En cada nueva conversación (`SessionStart`), Antigravity actualiza automáticamente `.agents/hub` desde GitHub y verifica mediante hashes `SHA-256` (`manifest_hashes.json`) que los 21 PDFs y el Excel PRISMA no hayan cambiado, **evitando releer los PDFs en cada sesión (Zero-Token Waste)**.

---

## 2. Estructura del Repositorio

* `final_20_samplepaper.tex`: Manuscrito principal en LaTeX (plantilla Springer LNCS) con Introducción, Trabajos Relacionados, Tablas 1 y 2 y bibliografía verificada.
* `ARTICULOS-INVESTIGACION-PREVIA/`: 7 artículos científicos base de contextualización y antecedentes.
* `ARTICULOS-TRABAJOS-RELACIONADOS/`: 14 artículos científicos del estado del arte y comparativa experimental.
* `PRISMA/`: Base de datos Excel `T4_Grupo2_Celi_Hinojoza.xlsx` y reporte de selección bibliográfica PRISMA 2020 (`prisma_2020.png`).
* `GUIAS/`: Guías metodológicas oficiales de la asignatura Lectura y Redacción de Textos Académicos (ESPE).
* `INTRODUCCION/`: Entregables previos, matriz de observaciones docentes (`Correcciones.pdf`) y bitácora `Implementacion_Correcciones.md`.
* `Arquitectura_Sistema_Cercos_Virtuales*.png/.svg` y `Flujo_Aplicacion_Cercos_Virtuales.png/.svg`: Diagramas vectoriales y de alta resolución de la investigación.

---

## 3. Comandos Rápidos para Colaboradores

```bash
# Clonar el repositorio incluyendo el Hub de Skills (.agents/hub):
git clone --recurse-submodules https://github.com/FaridHinojoza/V.I_Documentacion.git

# Si ya lo clonaste, inicializar o actualizar el submódulo de skills:
git submodule update --init --recursive
```
