# CGM Lab Assignment 01: Basic Graphics Primitives

**Student Name:** Layak Rathore  
**Roll Number:** IC-2K24-52  
**Lab Assignment:** 01  
**Subject:** Computer Graphics & Multimedia (CGM)

---

## 🎯 Objective

The objective of this assignment is to understand the fundamentals of computer graphics rendering in C++ using the **Borland Graphics Interface (BGI)** (`graphics.h`), and to design and implement a program that renders four basic 2D geometric primitives within an organized multi-pane viewport:
1. **Straight Line**
2. **Circle**
3. **Rectangle**
4. **Triangle** (constructed via connected line segments)

---

## 📚 Theoretical Knowledge & Concepts Learned

### 1. The Screen Coordinate System
Unlike standard mathematical Cartesian coordinates where $(0, 0)$ is at the center or bottom-left with $Y$ increasing upwards:
- In computer display adapters and BGI graphics, the origin $(0, 0)$ is located at the **top-left corner** of the screen.
- **$X$-coordinates** increase from left to right across horizontal scanlines.
- **$Y$-coordinates** increase from top to bottom down vertical columns.

```text
(0, 0) ---------------------> +X
  |
  |      [Display Screen]
  |
  v
 +Y
```

### 2. Graphics Driver Initialization
- **`DETECT` Macro:** Automatically queries the display adapter hardware to determine the optimal graphics driver.
- **`initgraph(&gd, &gm, path)`:** Initializes the graphics subsystem by loading the BGI driver from disk, switching the video card into graphics mode, and creating the display window.
- **`closegraph()`:** Shuts down the graphics subsystem, deallocating graphics memory and returning the system to standard text mode.

### 3. Basic Primitives & Function Signatures

| Primitive | BGI Function Signature | Description |
| :--- | :--- | :--- |
| **Line** | `line(x1, y1, x2, y2)` | Draws a continuous 1-pixel-wide line from point $(x_1, y_1)$ to $(x_2, y_2)$. |
| **Circle** | `circle(x, y, radius)` | Draws a circle centered at $(x, y)$ with the specified radius using integer midpoint or trigonometric rasterization. |
| **Rectangle** | `rectangle(left, top, right, bottom)` | Draws an axis-aligned bounding box defined by its top-left and bottom-right corner coordinates. |
| **Triangle** | *Composed Primitive* | Since standard BGI lacks a dedicated `triangle()` function, it is synthesized by interconnecting three vertices using 3 successive `line()` calls: $V_1 \to V_2 \to V_3 \to V_1$. |

### 4. Text Rendering in Graphics Mode
- **`settextstyle(font, direction, charsize)`:** Customizes font typeface, text orientation (`HORIZ_DIR` vs. `VERT_DIR`), and scaling factor.
- **`outtextxy(x, y, string)`:** Outputs a string directly to the raster display buffer at coordinate $(x, y)$.

---

## 🛠️ What I Did (Implementation Details)

1. **Structured Canvas & Viewport Partitioning:**
   - Instead of drawing overlapping primitives randomly, I designed a partitioned **4-quadrant layout**.
   - Created an outer boundary box in **RED** (`rectangle(20, 110, 620, 430)`).
   - Bisected the canvas horizontally (`line(20, 270, 620, 270)`) and vertically (`line(320, 110, 320, 430)`), yielding four symmetrical quadrants.

2. **Header & Identification Banner:**
   - Displayed an assignment title (`CGM LAB ASSIGNMENT - 01`) using size-2 horizontal text.
   - Displayed subtitle (`Basic Shapes`) and student credentials (`Name: LAYAK RATHORE | Roll No: IC-2K24-52`).

3. **Drawing Primitives in Dedicated Panes:**
   - **Quadrant 1 (Top-Left):** Rendered a horizontal straight line spanning from $(60, 190)$ to $(280, 190)$ under the label `"Straight Line"`.
   - **Quadrant 2 (Top-Right):** Rendered a circle centered at $(470, 190)$ with radius $r = 45$ under the label `"2. Circle"`.
   - **Quadrant 3 (Bottom-Left):** Rendered a distinct rectangle with bounds $(70, 320)$ to $(270, 400)$ under the label `"3. Rectangle"`.
   - **Quadrant 4 (Bottom-Right):** Defined three vertices for an isosceles triangle:
     - Peak vertex $T_1 = (470, 310)$
     - Bottom-left vertex $T_2 = (390, 400)$
     - Bottom-right vertex $T_3 = (550, 400)$
     - Connected them with three line segments under the label `"4. Triangle"`.

4. **Event Handling & Graceful Teardown:**
   - Kept the graphics window open using `getch()` to capture user keystroke prior to termination.
   - Safely deallocated graphics system resources via `closegraph()`.

---

## 💻 Source Code Overview

The complete implementation is in [`CGMLabAssignment01BasicShapes.cpp`](./CGMLabAssignment01BasicShapes.cpp).

```cpp
#include <graphics.h>
#include <conio.h>

int main()
{
    int gd = DETECT, gm;
    initgraph(&gd, &gm, (char*)"");

    // Title and Student Info
    settextstyle(DEFAULT_FONT, HORIZ_DIR, 2);
    setcolor(WHITE);
    outtextxy(140, 25, (char*)"CGM LAB ASSIGNMENT - 01");

    settextstyle(DEFAULT_FONT, HORIZ_DIR, 1);
    outtextxy(200, 55, (char*)"Basic Shapes");
    outtextxy(140, 80, (char*)"Name: LAYAK RATHORE  |  Roll No: IC-2K24-52");

    // Partition Grid (Red boundaries)
    setcolor(RED);
    rectangle(20, 110, 620, 430); 
    line(320, 110, 320, 430);     
    line(20, 270, 620, 270);     

    // 1. Straight Line
    setcolor(WHITE);
    outtextxy(40, 125, (char*)"Straight Line");
    line(60, 190, 280, 190);

    // 2. Circle
    outtextxy(340, 125, (char*)"2. Circle");
    circle(470, 190, 45);

    // 3. Rectangle
    outtextxy(40, 285, (char*)"3. Rectangle");
    rectangle(70, 320, 270, 400);

    // 4. Triangle
    outtextxy(340, 285, (char*)"4. Triangle");
    int tx1 = 470, ty1 = 310; 
    int tx2 = 390, ty2 = 400;
    int tx3 = 550, ty3 = 400; 
    line(tx1, ty1, tx2, ty2);
    line(tx2, ty2, tx3, ty3);
    line(tx3, ty3, tx1, ty1);

    getch();
    closegraph();
    return 0;
}
```

---

## 🖼️ Program Output

The program produces the following graphical display containing the formatted header and four quadrants:

![Lab 01 Output Screenshot](./CGMLabAssignment01BasicShapesOUTPUT.png)

---

## 🚀 How to Compile & Run

### Using MinGW / GCC (Windows with WinBGIm):
```bash
g++ CGMLabAssignment01BasicShapes.cpp -o lab01.exe -lbgi -lgdi32 -lcomdlg32 -luuid -loleaut32 -lole32
./lab01.exe
```

### Using Turbo C++ / Borland C++:
1. Open `CGMLabAssignment01BasicShapes.cpp` in Turbo C++.
2. Ensure BGI directory path is set in `Options -> Directories`.
3. Press `Ctrl + F9` to compile and run.

---

## 💡 Key Takeaways
- Learned how raster screen coordinate mapping differs from standard Cartesian planes.
- Mastered window layout planning and coordinate positioning for clean UI presentation.
- Understood that complex polygons (such as triangles) can be synthesized by linking elementary geometric primitives.
