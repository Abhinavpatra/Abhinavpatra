<p align="center">
  <a href="https://abhinavpatra.tech">abhinavpatra.tech</a> | 
  <a href="https://linkedin.com/in/abhinavpatra">linkedin.com/in/abhinavpatra</a>
</p>


<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Abhinavpatra/AbhinavPatra/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Abhinavpatra/AbhinavPatra/output/github-snake.svg" />
  <img alt="github-snake" src="https://raw.githubusercontent.com/Abhinavpatra/AbhinavPatra/output/github-snake.svg" />
</picture>

---

<p align="center">
  Thanks for visiting my page.
</p>


```c
#include <graphics.h>
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

// Structure for a point
struct Point {
    float x, y;
};

// Rotate a point about the origin
struct Point rotateOrigin(struct Point p, float angle)
{
    struct Point r;
    float rad = angle * PI / 180.0;

    r.x = p.x * cos(rad) - p.y * sin(rad);
    r.y = p.x * sin(rad) + p.y * cos(rad);

    return r;
}

// Rotate a point about a fixed point (cx, cy)
struct Point rotateFixed(struct Point p, float angle, float cx, float cy)
{
    struct Point r;
    float rad = angle * PI / 180.0;

    // Translate point so fixed point becomes origin
    float x = p.x - cx;
    float y = p.y - cy;

    // Rotate
    r.x = x * cos(rad) - y * sin(rad);
    r.y = x * sin(rad) + y * cos(rad);

    // Translate back
    r.x += cx;
    r.y += cy;

    return r;
}

// Convert Cartesian coordinates to screen coordinates
int screenX(float x)
{
    return 400 + (int)x;
}

int screenY(float y)
{
    return 300 - (int)y;
}

// Draw triangle
void drawTriangle(struct Point p1, struct Point p2, struct Point p3)
{
    line(screenX(p1.x), screenY(p1.y),
         screenX(p2.x), screenY(p2.y));

    line(screenX(p2.x), screenY(p2.y),
         screenX(p3.x), screenY(p3.y));

    line(screenX(p3.x), screenY(p3.y),
         screenX(p1.x), screenY(p1.y));
}

int main()
{
    int gd = DETECT, gm;
    float angle, cx, cy;

    struct Point p1, p2, p3;
    struct Point r1, r2, r3;
    struct Point f1, f2, f3;

    printf("Enter coordinates of triangle:\n");

    printf("Point 1 (x y): ");
    scanf("%f %f", &p1.x, &p1.y);

    printf("Point 2 (x y): ");
    scanf("%f %f", &p2.x, &p2.y);

    printf("Point 3 (x y): ");
    scanf("%f %f", &p3.x, &p3.y);

    printf("Enter rotation angle: ");
    scanf("%f", &angle);

    printf("Enter fixed point (cx cy): ");
    scanf("%f %f", &cx, &cy);

    // Rotation about origin
    r1 = rotateOrigin(p1, angle);
    r2 = rotateOrigin(p2, angle);
    r3 = rotateOrigin(p3, angle);

    // Rotation about fixed point
    f1 = rotateFixed(p1, angle, cx, cy);
    f2 = rotateFixed(p2, angle, cx, cy);
    f3 = rotateFixed(p3, angle, cx, cy);

    initgraph(&gd, &gm, "");

    // Draw coordinate axes
    line(0, 300, 800, 300);   // X-axis
    line(400, 0, 400, 600);   // Y-axis

    // Original triangle
    setcolor(WHITE);
    drawTriangle(p1, p2, p3);

    // Rotated about origin
    setcolor(RED);
    drawTriangle(r1, r2, r3);

    // Rotated about fixed point
    setcolor(GREEN);
    drawTriangle(f1, f2, f3);

    // Mark fixed point
    setcolor(YELLOW);
    circle(screenX(cx), screenY(cy), 4);

    outtextxy(20, 20, "WHITE - Original Triangle");
    outtextxy(20, 40, "RED - Rotation about Origin");
    outtextxy(20, 60, "GREEN - Rotation about Fixed Point");
    outtextxy(20, 80, "YELLOW - Fixed Point");

    getch();
    closegraph();

    return 0;
}


```