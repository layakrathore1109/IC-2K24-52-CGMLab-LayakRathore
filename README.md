# Computer Graphics & Multimedia (CGM) Lab

**Student Name:** Layak Rathore  
**Roll Number:** IC-2K24-52  
**Academic Course:** Computer Graphics and Multimedia Laboratory (C++ / BGI Graphics)

---

## 📌 Repository Overview

This repository contains lab assignments and implementations completed as part of the **Computer Graphics & Multimedia (CGM)** coursework. Each lab focuses on foundational raster graphics principles, ranging from basic 2D geometric primitive rendering to mathematical scan-conversion algorithms implemented in **C++** using the **Borland Graphics Interface (BGI / graphics.h)**.

---

## 📂 Directory Structure

```text
IC-2k24-52_layak/
│
├── Lab-01/                                      # Lab 1: Basic 2D Graphics Primitives
│   ├── CGMLabAssignment01BasicShapes.cpp        # Source code for drawing basic primitives
│   ├── CGMLabAssignment01BasicShapesOUTPUT.png  # Rendered GUI output screenshot
│   └── README.md                                # Detailed documentation for Lab 1
│
├── Lab-02/                                      # Lab 2: DDA Line Drawing Algorithm
│   ├── dda_line.cpp                             # Source code for DDA scan-conversion algorithm
│   ├── output.png                               # Rendered GUI output screenshot
│   └── README.md                                # Detailed documentation for Lab 2
│
├── .gitignore
└── README.md                                    # Repository overview (this file)
```

---

## 🔬 Lab Modules Summary

| Lab | Title | Key Topics & Algorithms Covered | Primary Functions / Techniques |
| :--- | :--- | :--- | :--- |
| **[Lab 01](./Lab-01/)** | **Basic Graphics Primitives** | Screen coordinate system, viewport partitioning, 2D primitives (Line, Circle, Rectangle, Triangle), text formatting | `initgraph()`, `line()`, `circle()`, `rectangle()`, `settextstyle()`, `outtextxy()` |
| **[Lab 02](./Lab-02/)** | **DDA Line Drawing Algorithm** | Scan conversion, differential equation $\frac{dy}{dx}$, incremental calculation, floating-point rounding, boundary clipping & validation | Custom `ddaLine()`, `putpixel()`, `roundOff()`, dynamic HUD metrics display |

---

## 🧠 Core Computer Graphics Knowledge Acquired

1. **Raster Graphics Coordinate System:**
   - In standard computer graphics systems (including `graphics.h`), the origin $(0, 0)$ is situated at the **top-left corner** of the display window.
   - The $X$-axis increases positively to the **right**, while the $Y$-axis increases positively **downwards** (inverted relative to Cartesian geometry).

2. **Primitive Rendering vs. Algorithmic Scan Conversion:**
   - **High-level primitives** (Lab 1): Utilize library functions that encapsulate underlying rasterization pipelines.
   - **Low-level scan conversion** (Lab 2): Translates continuous geometric representations ($y = mx + c$) into discrete raster pixels using the **Digital Differential Analyzer (DDA)** algorithm.

3. **Incremental Computation:**
   - Replacing costly multiplicative formulas with unit incremental additions ($\Delta x$, $\Delta y$) per iteration drastically optimizes rasterization loops.

4. **Coordinate Space & Boundary Clipping:**
   - Enforcing workspace boundaries $(20 \le x \le 620, 110 \le y \le 430)$ prevents buffer overruns and ensures graphics elements remain within the designated viewport.

---

## ⚙️ Environment Setup & Compilation

These programs use the `graphics.h` (WinBGIm / Borland BGI) library on Windows.

### Prerequisites
- **Compiler:** MinGW (32-bit recommended for WinBGIm) or Code::Blocks / Dev-C++ configured with `libbgi.a` and `graphics.h`.
- **System Libraries:** GDI32, Comdlg32, UUID, OLE32, OLEAut32.

### Compilation Command (GCC / MinGW)

```bash
# Lab 01
g++ Lab-01/CGMLabAssignment01BasicShapes.cpp -o Lab-01/lab1.exe -lbgi -lgdi32 -lcomdlg32 -luuid -loleaut32 -lole32

# Lab 02
g++ Lab-02/dda_line.cpp -o Lab-02/lab2.exe -lbgi -lgdi32 -lcomdlg32 -luuid -loleaut32 -lole32
```

---

## 👤 Author Information

- **Student:** Layak Rathore
- **Roll Number:** `IC-2K24-52`
- **Class / Batch:** 2K24
