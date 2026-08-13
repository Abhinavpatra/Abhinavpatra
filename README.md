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

#include <GL/glut.h>
#include <math.h>

int xst = 60, yst = 50;
int xend = 400, yend = 300;

void drawPixel(int x, int y)
{
    glBegin(GL_POINTS);
    glVertex2i(x, y);
    glEnd();
}

void DDA(int xs, int ys, int xe, int ye)
{
    int dx = xe - xs;
    int dy = ye - ys;

    int steps = (abs(dx) > abs(dy)) ? abs(dx) : abs(dy);

    float Xinc = (float)dx / steps;
    float Yinc = (float)dy / steps;

    float x = xs;
    float y = ys;

    for (int i = 0; i <= steps; i++)
    {
        drawPixel((int)round(x), (int)round(y));

        x += Xinc;
        y += Yinc;
    }
}

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    glColor3f(1.0, 1.0, 1.0);

    DDA(xst, yst, xend, yend);

    glFlush();
}

void init()
{
    glClearColor(0.0, 0.0, 0.0, 1.0);

    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();

    gluOrtho2D(0, 500, 0, 500);
}

int main(int argc, char **argv)
{
    glutInit(&argc, argv);

    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);

    glutInitWindowSize(500, 500);
    glutInitWindowPosition(100, 100);

    glutCreateWindow("DDA Line Drawing Algorithm");

    init();

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}

```