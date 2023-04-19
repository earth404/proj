#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *gp;
    gp = popen("gnuplot -persistent", "w");
    if (gp == NULL) {
        printf("Error opening pipe to gnuplot.\n");
        return 1;
    }

    double grade, x = 1.0, y;
    char grade_str[3];
    printf("Enter grade (or -1 to end): ");
    scanf("%lf", &grade);
    double grade_y_prev = 0.00;
    while (grade != -1) {
        if (grade >= 80) {
            y = grade;
            sprintf(grade_str, "A");
        } else if (grade >= 70) {
            y = grade;
            sprintf(grade_str, "B");
        } else if (grade >= 60) {
            y = grade;
            sprintf(grade_str, "C");
        } else if (grade >= 50) {
            y = grade;
            sprintf(grade_str, "D");
        } else {
            y = grade;
            sprintf(grade_str, "F");
        }

        fprintf(gp, "set object %lf circle at %lf,%lf fillcolor \"black\" size 0.01\n", x, x, grade);
        fprintf(gp, "set label \"%s\" at %lf,%lf center font \"Arial,7\"\n", grade_str, x, grade+0.02);

        double grade_x = x;
        double grade_y = y;

        fprintf(gp, "set arrow from %lf,%lf to %lf,%lf nohead\n", grade_x-1, grade_y_prev, grade_x, grade_y);
        grade_y_prev = grade_y;
        x++;
        printf("Enter grade (or -1 to end): ");
        scanf("%lf", &grade);
    }

    fprintf(gp, "set xrange [0:%lf]\n", x);
    fprintf(gp, "set yrange [0:100]\n");
    fprintf(gp, "set xlabel \"Grade\"\n");
    fprintf(gp, "set ylabel \"Grade Point\"\n");
    fprintf(gp, "set title \"Grade Distribution\"\n");
    fprintf(gp, "plot NaN notitle\n");

    pclose(gp);

    return 0;
}
