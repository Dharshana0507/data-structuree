#include <stdio.h>
#include <ctype.h>

#define SIZE 100

char stack[SIZE];
int top = -1;

// Stack operations
void push(char c) {
    stack[++top] = c;
}

char pop() {
    return stack[top--];
}

char peek() {
    return stack[top];
}

int precedence(char op) {
    if (op == '^') return 3;
    else if (op == '*' || op == '/') return 2;
    else if (op == '+' || op == '-') return 1;
    else return 0;
}

void infixToPostfix(char infix[]) {
    char postfix[SIZE];
    int i = 0, j = 0;
    char symbol;

    while ((symbol = infix[i++]) != '\0') {
        if (isalnum(symbol)) {
            postfix[j++] = symbol;  // Operand goes to output
        } else if (symbol == '(') {
            push(symbol);
        } else if (symbol == ')') {
            while (peek() != '(')
                postfix[j++] = pop();
            pop(); // pop '('
        } else {  // Operator
            while (top != -1 && precedence(peek()) >= precedence(symbol))
                postfix[j++] = pop();
            push(symbol);
        }
    }

    while (top != -1)
        postfix[j++] = pop();

    postfix[j] = '\0';

    printf("Postfix: %s\n", postfix);
}

int main() {
    char infix[] = "A+B*C";
    printf("Infix: %s\n", infix);
    infixToPostfix(infix);
    return 0;
}
#include <stdio.h>
#include <ctype.h>

#define SIZE 100

char stack[SIZE];
int top = -1;

// Push operation
void push(char c) {
    stack[++top] = c;
}

// Pop operation
char pop() {
    return stack[top--];
}

// Peek operation
char peek() {
    return stack[top];
}

// Precedence function
int precedence(char op) {
    if (op == '^') return 3;
    else if (op == '*' || op == '/') return 2;
    else if (op == '+' || op == '-') return 1;
    else return 0;
}

// Infix to postfix conversion
void infixToPostfix(char infix[]) {
    char postfix[SIZE];
    int i = 0, j = 0;
    char symbol;

    while ((symbol = infix[i++]) != '\0') {
        if (isalnum(symbol)) {
            postfix[j++] = symbol;  // Operand → output
        } else if (symbol == '(') {
            push(symbol);  // Push '(' to stack
        } else if (symbol == ')') {
            while (peek() != '(')
                postfix[j++] = pop();  // Pop until '('
            pop(); // Remove '('
        } else {
            while (top != -1 && precedence(peek()) >= precedence(symbol))
                postfix[j++] = pop();  // Pop higher or equal precedence
            push(symbol);
        }
    }

    while (top != -1)
        postfix[j++] = pop();  // Pop remaining operators

    postfix[j] = '\0';

    printf("Postfix: %s\n", postfix);
}

int main() {
    char infix[] = "(A+B)*C";
    printf("Infix: %s\n", infix);
    infixToPostfix(infix);
    return 0;
}
#include <stdio.h>
#include <ctype.h>  // for isalnum()
#define MAX 100

char stack[MAX];
int top = -1;

void push(char c) {
    stack[++top] = c;
}

char pop() {
    return stack[top--];
}

int precedence(char c) {
    if (c == '+' || c == '-') return 1;
    if (c == '*' || c == '/') return 2;
    if (c == '^') return 3;
    return 0;
}

void infixToPostfix(char infix[]) {
    char postfix[MAX];
    int i = 0, k = 0;
    char symbol;

    while ((symbol = infix[i++]) != '\0') {
        if (isalnum(symbol)) {
            postfix[k++] = symbol;
        } 
        else if (symbol == '(') {
            push(symbol);
        } 
        else if (symbol == ')') {
            while (stack[top] != '(')
                postfix[k++] = pop();
            pop(); // remove '('
        } 
        else { // operator
            while (top != -1 && precedence(stack[top]) >= precedence(symbol))
                postfix[k++] = pop();
            push(symbol);
        }
    }

    while (top != -1)
        postfix[k++] = pop();

    postfix[k] = '\0';
    printf("Postfix: %s\n", postfix);
}

int main() {
    char infix[] = "A+B-C";
    printf("Infix: %s\n", infix);
    infixToPostfix(infix);
    return 0;
  }
  #include <stdio.h>
#include <ctype.h>  // for isalnum()
#define MAX 100

char stack[MAX];
int top = -1;

void push(char c) {
    stack[++top] = c;
}

char pop() {
    return stack[top--];
}

int precedence(char c) {
    if (c == '+' || c == '-') return 1;
    if (c == '*' || c == '/') return 2;
    if (c == '^') return 3;
    return 0;
}

void infixToPostfix(char infix[]) {
    char postfix[MAX];
    int i = 0, k = 0;
    char symbol;

    while ((symbol = infix[i++]) != '\0') {
        if (isalnum(symbol)) {  
            postfix[k++] = symbol;  // operand directly to output
        } 
        else if (symbol == '(') {
            push(symbol);
        } 
        else if (symbol == ')') {
            while (stack[top] != '(')
                postfix[k++] = pop();
            pop(); // remove '('
        } 
        else { // operator
            while (top != -1 && precedence(stack[top]) >= precedence(symbol))
                postfix[k++] = pop();
            push(symbol);
        }
    }

    while (top != -1)
        postfix[k++] = pop();

    postfix[k] = '\0';
    printf("Postfix: %s\n", postfix);
}

int main() {
    char infix[] = "A+B*C-D/E";
    printf("Infix: %s\n", infix);
    infixToPostfix(infix);
    return 0;
}
