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

int main()
{
    int n, epochs;
    double learning_rate;

    printf("Weighted Linear Regression using Gradient Descent\n");
    printf("--------------------------------------------------\n");

    printf("Enter number of data points: ");
    scanf("%d", &n);

    double x[n], y[n], weight[n];

    printf("Enter X, Y and Weight values:\n");

    for (int i = 0; i < n; i++)
    {
        printf("Data %d (X Y Weight): ", i + 1);
        scanf("%lf %lf %lf", &x[i], &y[i], &weight[i]);
    }

    printf("Enter Learning Rate: ");
    scanf("%lf", &learning_rate);

    printf("Enter Number of Epochs: ");
    scanf("%d", &epochs);

    // Initial values of slope and intercept
    double w = 0.0;   // slope
    double b = 0.0;   // intercept

    printf("\nTraining Started...\n");

    for (int epoch = 1; epoch <= epochs; epoch++)
    {
        double dw = 0.0;
        double db = 0.0;
        double weighted_error = 0.0;
        double total_weight = 0.0;

        // Calculate gradients
        for (int i = 0; i < n; i++)
        {
            double predicted = w * x[i] + b;
            double error = predicted - y[i];

            dw += weight[i] * error * x[i];
            db += weight[i] * error;

            weighted_error += weight[i] * error * error;
            total_weight += weight[i];
        }

        // Average gradients
        dw = (2.0 / total_weight) * dw;
        db = (2.0 / total_weight) * db;

        // Update parameters
        w = w - learning_rate * dw;
        b = b - learning_rate * db;

        // Calculate WMSE
        double wmse = weighted_error / total_weight;

        printf("Epoch %d WMSE = %.6f\n", epoch, wmse);
    }

    printf("----------------------------------------\n");
    printf("Training Completed Successfully\n");
    printf("----------------------------------------\n");

    printf("Final Weight (Slope) = %.4f\n", w);
    printf("Final Bias (Intercept) = %.4f\n", b);

    printf("Regression Equation:\n");
    printf("Y = %.4fX + %.4f\n", w, b);

    printf("--------------------------------------------------\n");
    printf("X\tActual Y\tWeight\tPredicted Y\n");
    printf("--------------------------------------------------\n");

    double final_wmse = 0.0;
    double total_weight = 0.0;

    for (int i = 0; i < n; i++)
    {
        double predicted = w * x[i] + b;
        double error = predicted - y[i];

        final_wmse += weight[i] * error * error;
        total_weight += weight[i];

        printf("%.2f\t%.2f\t\t%.2f\t%.2f\n",
               x[i], y[i], weight[i], predicted);
    }

    final_wmse /= total_weight;

    printf("--------------------------------------------------\n");
    printf("Final Weighted Mean Squared Error (WMSE) = %.6f\n",
           final_wmse);

    return 0;
}

```