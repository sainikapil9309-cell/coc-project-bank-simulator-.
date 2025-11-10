# coc-project-bank-simulator-.
coc project about bank simulation
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>

// Function to generate a random number from Poisson(λ)
int poisson(double lambda) {
    double L = exp(-lambda);
    double p = 1.0;
    int k = 0;

    while (p > L) {
        p *= (rand() / (double)RAND_MAX);
        k++;
    }
    return k - 1;
}

int main() {
    double lambda;
    int minute, arrivals;
    int count0 = 0, count1 = 0, count2 = 0, count3plus = 0;

    srand(time(NULL));  // seed random number generator

    // Step 1: Ask user for λ
    printf("Enter the average number of customers per minute (λ): ");
    scanf("%lf", &lambda);

    // Step 2: Simulate 480 minutes
    for (minute = 1; minute <= 480; minute++) {
        arrivals = poisson(lambda);  // get number of arrivals this minute

        // Count categories
        if (arrivals == 0) count0++;
        else if (arrivals == 1) count1++;
        else if (arrivals == 2) count2++;
        else count3plus++;

        // Optional: print each minute
        // printf("Minute %3d: %d arrivals\n", minute, arrivals);
    }

    // Step 3: Print summary
    printf("\n--- Simulation Summary ---\n");
    printf("Minutes with 0 arrivals : %d\n", count0);
    printf("Minutes with 1 arrival  : %d\n", count1);
    printf("Minutes with 2 arrivals : %d\n", count2);
    printf("Minutes with 3+ arrivals: %d\n", count3plus);

    return 0;
}
