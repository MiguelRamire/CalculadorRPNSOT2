\#include <stdio.h>

\#include <stdlib.h>

\#include <math.h>

\#include <string.h>



\#define MAX 100



double stack\[MAX];

int top = 0;



void push(double value) {

&nbsp;   if (top < MAX) {

&nbsp;       stack\[top++] = value;

&nbsp;   } else {

&nbsp;       printf("Error: Pila llena\\n");

&nbsp;   }

}



double pop() {

&nbsp;   if (top > 0) {

&nbsp;       return stack\[--top];

&nbsp;   } else {

&nbsp;       printf("Error: Pila vacía\\n");

&nbsp;       return 0;

&nbsp;   }

}



void printStack() {

&nbsp;   printf("\\n--- PILA ---\\n");

&nbsp;   for (int i = top - 1; i >= 0; i--) {

&nbsp;       printf("%g\\n", stack\[i]);

&nbsp;   }

&nbsp;   printf("------------\\n");

}



int main() {

&nbsp;   char input\[50];

&nbsp;   double a, b;



&nbsp;   printf("Calculadora RPN (escribe 'exit' para salir)\\n");

&nbsp;   printf("Operadores soportados: + - \* / pow sqrt sin cos tan log ln\\n\\n");



&nbsp;   while (1) {

&nbsp;       printStack();

&nbsp;       printf("> ");

&nbsp;       scanf("%s", input);



&nbsp;       if (strcmp(input, "exit") == 0) break;



&nbsp;       // Si es número

&nbsp;       char \*endptr;

&nbsp;       double num = strtod(input, \&endptr);

&nbsp;       if (\*endptr == '\\0') {

&nbsp;           push(num);

&nbsp;           continue;

&nbsp;       }



&nbsp;       // Operaciones binarias

&nbsp;       if (strcmp(input, "+") == 0) {

&nbsp;           if (top < 2) { printf("Error: se necesitan 2 operandos\\n"); continue; }

&nbsp;           b = pop(); a = pop();

&nbsp;           push(a + b);

&nbsp;       } 

&nbsp;       else if (strcmp(input, "-") == 0) {

&nbsp;           if (top < 2) { printf("Error: se necesitan 2 operandos\\n"); continue; }

&nbsp;           b = pop(); a = pop();

&nbsp;           push(a - b);

&nbsp;       } 

&nbsp;       else if (strcmp(input, "\*") == 0) {

&nbsp;           if (top < 2) { printf("Error: se necesitan 2 operandos\\n"); continue; }

&nbsp;           b = pop(); a = pop();

&nbsp;           push(a \* b);

&nbsp;       } 

&nbsp;       else if (strcmp(input, "/") == 0) {

&nbsp;           if (top < 2) { printf("Error: se necesitan 2 operandos\\n"); continue; }

&nbsp;           b = pop(); a = pop();

&nbsp;           if (b != 0) push(a / b);

&nbsp;           else printf("Error: División por cero\\n");

&nbsp;       }

&nbsp;       else if (strcmp(input, "pow") == 0) {

&nbsp;           if (top < 2) { printf("Error: se necesitan 2 operandos\\n"); continue; }

&nbsp;           b = pop(); a = pop();

&nbsp;           push(pow(a, b));

&nbsp;       }



&nbsp;       // Operaciones unarias

&nbsp;       else if (strcmp(input, "sqrt") == 0) {

&nbsp;           if (top < 1) { printf("Error: se necesita 1 operando\\n"); continue; }

&nbsp;           a = pop();

&nbsp;           if (a >= 0) push(sqrt(a));

&nbsp;           else printf("Error: Raíz negativa\\n");

&nbsp;       }

&nbsp;       else if (strcmp(input, "sin") == 0) {

&nbsp;           if (top < 1) { printf("Error: se necesita 1 operando\\n"); continue; }

&nbsp;           a = pop();

&nbsp;           push(sin(a));

&nbsp;       }

&nbsp;       else if (strcmp(input, "cos") == 0) {

&nbsp;           if (top < 1) { printf("Error: se necesita 1 operando\\n"); continue; }

&nbsp;           a = pop();

&nbsp;           push(cos(a));

&nbsp;       }

&nbsp;       else if (strcmp(input, "tan") == 0) {

&nbsp;           if (top < 1) { printf("Error: se necesita 1 operando\\n"); continue; }

&nbsp;           a = pop();

&nbsp;           push(tan(a));

&nbsp;       }

&nbsp;       else if (strcmp(input, "log") == 0) {

&nbsp;           if (top < 1) { printf("Error: se necesita 1 operando\\n"); continue; }

&nbsp;           a = pop();

&nbsp;           if (a > 0) push(log10(a));

&nbsp;           else printf("Error: log de número no positivo\\n");

&nbsp;       }

&nbsp;       else if (strcmp(input, "ln") == 0) {

&nbsp;           if (top < 1) { printf("Error: se necesita 1 operando\\n"); continue; }

&nbsp;           a = pop();

&nbsp;           if (a > 0) push(log(a));

&nbsp;           else printf("Error: ln de número no positivo\\n");

&nbsp;       }

&nbsp;       else {

&nbsp;           printf("Comando no reconocido\\n");

&nbsp;       }

&nbsp;   }



&nbsp;   return 0;

}



