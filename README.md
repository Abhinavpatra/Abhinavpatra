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
#include <math.h>

#define N 10
#define LEARNING_RATE 0.0001
#define MAX_ITERATIONS 100000

// Sigmoid function
double sigmoid(double z) {
    return 1.0 / (1.0 + exp(-z));
}

int main() {

    /*
        Training data

        Features:
        height     = feet
        weight     = kg
        foot_size  = inches

        Label:
        1 = Male
        0 = Female

        Replace these samples with the "given training dataset"
        provided by your instructor if it is different.
    */

    double height[N] = {
        5.9, 5.5, 6.0, 5.8, 5.7,
        5.2, 5.4, 5.3, 5.6, 5.1
    };

    double weight[N] = {
        75, 60, 80, 72, 70,
        52, 55, 50, 58, 48
    };

    double foot[N] = {
        11, 9, 12, 10, 11,
        7, 8, 7, 9, 7
    };

    double y[N] = {
        1, 0, 1, 1, 1,
        0, 0, 0, 0, 0
    };

    // Model parameters
    double bias = 0.0;
    double w_height = 0.0;
    double w_weight = 0.0;
    double w_foot = 0.0;

    double cost = 0.0;
    double previous_cost = 0.0;

    printf("============================================\n");
    printf("       LOGISTIC REGRESSION TRAINING\n");
    printf("============================================\n");

    printf("Learning Rate: %.6f\n", LEARNING_RATE);

    /*
        Gradient Descent
    */

    for (int iteration = 0; iteration < MAX_ITERATIONS; iteration++) {

        double db = 0.0;
        double dw_height = 0.0;
        double dw_weight = 0.0;
        double dw_foot = 0.0;

        cost = 0.0;

        for (int i = 0; i < N; i++) {

            // Linear combination
            double z = bias
                     + w_height * height[i]
                     + w_weight * weight[i]
                     + w_foot * foot[i];

            // Sigmoid
            double prediction = sigmoid(z);

            // Avoid log(0)
            if (prediction < 1e-15)
                prediction = 1e-15;

            if (prediction > 1.0 - 1e-15)
                prediction = 1.0 - 1e-15;

            // Logistic regression cost
            cost += -(y[i] * log(prediction)
                    + (1 - y[i]) * log(1 - prediction));

            // Error
            double error = prediction - y[i];

            // Gradients
            db += error;
            dw_height += error * height[i];
            dw_weight += error * weight[i];
            dw_foot += error * foot[i];
        }

        // Average cost
        cost /= N;

        // Average gradients
        db /= N;
        dw_height /= N;
        dw_weight /= N;
        dw_foot /= N;

        // Update parameters
        bias -= LEARNING_RATE * db;
        w_height -= LEARNING_RATE * dw_height;
        w_weight -= LEARNING_RATE * dw_weight;
        w_foot -= LEARNING_RATE * dw_foot;

        // Check convergence
        if (iteration > 0 &&
            fabs(previous_cost - cost) < 1e-10) {
            break;
        }

        previous_cost = cost;
    }

    printf("Training Complete.\n");

    printf("\nOptimal Weights:\n");
    printf("Bias      = %.6f\n", bias);
    printf("Height    = %.6f\n", w_height);
    printf("Weight    = %.6f\n", w_weight);
    printf("Foot Size = %.6f\n", w_foot);

    /*
        Prediction
    */

    double input_height;
    double input_weight;
    double input_foot;

    printf("\nEnter details for prediction:\n");

    printf("Enter Height (feet): ");
    scanf("%lf", &input_height);

    printf("Enter Weight (kg): ");
    scanf("%lf", &input_weight);

    printf("Enter Foot Size: ");
    scanf("%lf", &input_foot);

    // Calculate linear combination
    double z = bias
             + w_height * input_height
             + w_weight * input_weight
             + w_foot * input_foot;

    // Calculate probability
    double probability = sigmoid(z);

    printf("\nProbability of Male: %.6f\n", probability);

    // Threshold = 0.5
    if (probability >= 0.5)
        printf("Predicted Gender: Male\n");
    else
        printf("Predicted Gender: Female\n");

    return 0;
}


```
