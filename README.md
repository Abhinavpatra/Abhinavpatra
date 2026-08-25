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
#include <stdio.h>
#include <stdlib.h>

void bresenham(int x1, int y1, int x2, int y2)
{
    int dx = abs(x2 - x1);
    int dy = abs(y2 - y1);

    int sx = (x1 < x2) ? 1 : -1;
    int sy = (y1 < y2) ? 1 : -1;

    int err = dx - dy;
    int e2;

    while (1)
    {
        printf("(%d, %d)\n", x1, y1);

        if (x1 == x2 && y1 == y2)
            break;

        e2 = 2 * err;

        if (e2 > -dy)
        {
            err -= dy;
            x1 += sx;
        }

        if (e2 < dx)
        {
            err += dx;
            y1 += sy;
        }
    }
}

int main()
{
    int x1, y1, x2, y2;

    printf("Enter x1 y1: ");
    scanf("%d %d", &x1, &y1);

    printf("Enter x2 y2: ");
    scanf("%d %d", &x2, &y2);

    bresenham(x1, y1, x2, y2);

    return 0;
}
```