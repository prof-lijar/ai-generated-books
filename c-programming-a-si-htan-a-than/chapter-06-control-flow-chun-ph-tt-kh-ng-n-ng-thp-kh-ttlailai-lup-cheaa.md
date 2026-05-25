---
chapter: 6
title: "Control Flow — ဆုံးဖြတ်ခြင်းနှင့် ထပ်ခါတလဲလဲ လုပ်ဆောင်ခြင်း"
generated_at: "2026-05-25T14:05:11.333170+00:00"
---

# Chapter 6: Control Flow — ဆုံးဖြတ်ခြင်းနှင့် ထပ်ခါတလဲလဲ လုပ်ဆောင်ခြင်း

## 1. Introduction: The Logic of Program Execution (အစပျိုးခြင်းနှင့် ပရိုဂရမ် အလုပ်လုပ်ပုံ၏ ကျိုးကြောင်းဆင်ခြင်မှု)

When we write a program, we are essentially giving a set of instructions to the computer. In the simplest form, these instructions are executed one after the other, sequentially. The computer reads the code from the top to the bottom and executes each instruction in turn. However, the real power of programming lies not just in this sequential execution, but in the ability to make decisions and repeat actions based on specific conditions. How does the computer decide *when* to do *what* instead of just executing instructions in a rigid line? This is where the concept of **Control Flow** becomes paramount.

Control Flow is the framework or the roadmap that dictates the order in which the instructions in a program are executed. It manages the path that the program takes through the various blocks of code. Without control flow mechanisms, programs would be reduced to simple, linear scripts, capable only of performing a single, fixed sequence of tasks. To handle real-world problems—which are inherently complex and involve dynamic situations—we need the ability to introduce logic that allows the program to branch, iterate, and repeat actions based on changing conditions.

The importance of Control Flow cannot be overstated. It transforms a simple sequence of commands into a dynamic and intelligent system. If we lacked control flow, every program would be a static document, incapable of responding to user input, handling errors gracefully, or performing complex calculations that depend on variables. Control flow allows us to build programs that can adapt to different scenarios, making them powerful tools for solving complex problems in mathematics, data processing, graphics, and artificial intelligence. Mastering control flow is the fundamental step toward writing sophisticated and robust software.

## 2. Conditional Statements: Decision Making (အခြေအနေအလိုက် ဆုံးဖြတ်ခြင်း)

The ability to make decisions is the first major step in controlling program flow. Conditional statements allow the program to execute different blocks of code based on whether a specified condition is true or false. This mechanism introduces the concept of branching, allowing the program to choose one path among many possibilities.

### 2.1. If-Else Structure (အခြေခံ ဆုံးဖြတ်ချက်များ)

The most basic decision-making structure is the `if-else` statement. The `if` statement checks a condition; if the condition evaluates to true, the code block inside the `if` statement is executed. If the condition is false, the program skips that block. The `else` part provides an alternative path to execute if the initial `if` condition is false.

This structure is fundamental for basic decision-making. For instance, we can use it to determine access based on age or to check if a number is positive or negative.

Consider the example of age-based access control. If a user is old enough, they are granted access; otherwise, they are denied.

```c
#include <stdio.h>

int main() {
    int age = 20;

    if (age >= 18) {
        printf("Access Granted. You are eligible.\n");
    } else {
        printf("Access Denied. You must be 18 or older.\n");
    }

    return 0;
}
```

In this simple example, the program checks the condition `age >= 18`. If this condition is true (as in our example where age is 20), the code inside the `if` block is executed. If the condition is false, the code inside the `else` block is executed. This simple branching mechanism is the foundation for all complex decision logic in programming.

### 2.2. Advanced Conditional Techniques (အဆင့်မြင့် ဆုံးဖြတ်ချက် နည်းစနစ်များ)

As programs become more complex, we often need to test multiple, mutually exclusive conditions. This leads us to more advanced conditional techniques.

#### Nested If Statements: အခြေအနေအောက်မှ ဆက်လက်စစ်ဆေးခြင်း

Nested `if` statements involve placing one `if` statement inside another `if` or `else` block. This allows us to test a secondary condition only if a primary condition has already been met. This technique is incredibly useful for handling hierarchical decision structures and for defining complex patterns.

For example, when drawing geometric shapes or checking multiple criteria simultaneously, nesting is essential. Imagine we want to check if a number is both positive AND even.

```c
#include <stdio.h>

int main() {
    int num = 10;

    if (num > 0) {
        printf("%d is positive.\n", num);
        if (num % 2 == 0) {
            printf("%d is also even.\n", num);
        } else {
            printf("%d is odd.\n", num);
        }
    } else {
        printf("%d is not positive.\n", num);
    }

    return 0;
}
```

In this example, the outer `if` checks if `num > 0`. Only if this condition is true, the program proceeds to the inner `if` statement to check if `num % 2 == 0`. This demonstrates how nested statements allow us to build intricate decision trees, which is crucial when dealing with multi-layered constraints. This is particularly useful when trying to define complex rules or draw intricate geometric patterns based on coordinate systems.

#### Ternary Operator (`? :`): အတိုချုပ်ပြီး ဆုံးဖြတ်ချက်ပေးခြင်း

For simple conditional assignments, we can use the ternary operator (`? :`). This operator provides a concise, one-line way to assign a value based on a condition. It is a shorthand for a simple `if-else` statement when you need to assign a value to a variable based on a condition.

The syntax is as follows: `condition ? expression_if_true : expression_if_false;`

This operator is excellent for situations where you need to assign one of two possible values to a variable based on a condition. It makes the code more compact and easier to read for simple assignments.

```c
#include <stdio.h>

int main() {
    int score = 85;
    char result;

    // Using the ternary operator to assign a grade
    result = (score >= 60) ? 'P' : 'F';

    printf("The result is: %c\n", result);

    return 0;
}
```

In this example, we are determining the value of the `result` character based on whether the `score` is greater than or equal to 60. If the condition `score >= 60` is true, the value 'P' is assigned to `result`. If the condition is false, the value 'F' is assigned to `result`. This is a powerful tool for concise conditional assignments, saving us from writing lengthy `if-else` blocks when the task is a simple assignment.

As we have seen, conditional statements allow the program to choose different execution paths. Understanding how these paths are chosen is the first step. Now, having established the decision-making capabilities, the next logical step is to learn how to repeat these actions—how to execute the chosen path multiple times.

## 3. Selection Structures: Switch-Case (လမ်းကြောင်းခွဲခြင်း)

While `if-else` structures are excellent for checking a series of conditions, the `switch-case` statement provides a more elegant and often more efficient way to handle multi-way branching based on the value of a single variable.

### 3.1. The Switch Statement (Switch-Case):

The `switch` statement allows the program to execute different blocks of code based on the value of a single expression. Instead of writing a long chain of `if-else if-else` statements to check for multiple possible values, `switch` allows us to compare a variable against a list of constant values (cases).

The structure involves a `switch` expression, which is the variable whose value we want to test. Then, it is followed by one or more `case` labels. Each `case` label specifies a value to compare against the switch expression. If a match is found, the code block associated with that `case` is executed.

A crucial element in the `switch` statement is the `break` statement. The `break` statement is essential because, by default, if a `case` matches, the program will execute the code for that `case` and then continue executing the code in the subsequent `case` labels, regardless of whether they match. The `break` statement explicitly tells the program to exit the `switch` block once a match is found and the corresponding code has been executed.

Furthermore, the `default` statement plays an important role. The `default` statement is executed if none of the `case` labels match the value of the switch expression. This provides a way to handle unexpected or invalid input values, making the program more robust and error-tolerant.

For example, when creating a menu selection system, we might want to perform different actions based on a user's choice from a menu. The `switch` statement is perfectly suited for this.

```c
#include <stdio.h>

int main() {
    int choice = 2;
    char message;

    switch (choice) {
        case 1:
            printf("Option 1 selected: Perform Addition.\n");
            break;
        case 2:
            printf("Option 2 selected: Perform Subtraction.\n");
            break;
        case 3:
            printf("Option 3 selected: Perform Multiplication.\n");
            break;
        default:
            printf("Invalid option selected. Please choose 1, 2, or 3.\n");
            break;
    }

    return 0;
}
```

In this example, the program checks the value of the `choice` variable. If `choice` is 1, the code under `case 1` is executed, and then the `break` statement ensures the program exits the `switch` block. If `choice` is 2, the code under `case 2` is executed, and so on. If the `choice` does not match any of the `case` values, the code under the `default` block is executed. This makes menu-driven programs much cleaner and more manageable than using a long series of `if-else if-else` statements.

### 3.2. Comparison and Flow Management:

The proper use of the `break` statement is vital when working with `switch` statements. As mentioned before, without `break`, the program will "fall through" to the next `case` block after a match is found. This can lead to unintended execution of code, which is a common source of bugs in programming. Therefore, always remember to include `break` after each `case` to ensure that only the intended block of code is executed.

Understanding how control flow works within `switch` statements, and the importance of the `break` statement, is a fundamental skill for managing program flow effectively. This principle extends to all control flow structures: if you are looping, you need to know how to exit the loop correctly, and if you are making decisions, you need to understand the branching logic.

## 4. Iteration Structures: Loops (ထပ်ခါတလဲလဲ လုပ်ဆောင်ခြင်း)

If conditional statements allow a program to make decisions, loops provide the mechanism to perform those decisions or actions repeatedly. Iteration structures, or loops, allow us to execute a block of code multiple times without having to write the same code repeatedly. This is essential for tasks involving large datasets, repetitive calculations, or generating patterns.

### 4.1. The For Loop (အကြိမ်ရေ သတ်မှတ်၍ ပတ်ခြင်း)

The `for` loop is a control structure designed for situations where we know exactly how many times we want a block of code to be executed. The `for` loop consolidates the three essential components required for loop control into a single, concise structure: initialization, condition, and iteration.

The structure of a `for` loop is as follows: `for (initialization; condition; increment/decrement) { ... }`

1.  **Initialization:** This part is executed only once at the beginning of the loop. It's used to declare and initialize a loop control variable. This is where we typically set the starting point for our counting.
2.  **Condition:** This is a boolean expression that is evaluated before each iteration of the loop. If the condition is true, the loop body will be executed. If the condition is false, the loop will terminate.
3.  **Increment/Decrement:** This part is executed after each iteration of the loop. It's used to update the loop control variable, moving it towards the termination condition.

The `for` loop is particularly useful when working with arrays. We can use a `for` loop to iterate through all the elements of an array, accessing each element one by one.

For example, to calculate the sum of numbers from 1 to 10:

```c
#include <stdio.h>

int main() {
    int sum = 0;
    // Loop from 1 to 10, incrementing by 1 in each step
    for (int i = 1; i <= 10; i++) {
        sum = sum + i;
    }
    printf("The sum of numbers from 1 to 10 is: %d\n", sum);
    return 0;
}
```

In this example, `int i = 1;` initializes a loop counter `i` to 1. The condition `i <= 10` checks if `i` is less than or equal to 10. If true, the loop body executes, where we add the current value of `i` to the `sum`. Then, `i++` increments the value of `i` by 1 before the next iteration. This process repeats until `i` becomes greater than 10, at which point the loop terminates. This demonstrates the power of the `for` loop in efficiently performing repetitive calculations.

### 4.2. The While Loop (အခြေအနေအပေါ် အခြေခံ၍ ပတ်ခြင်း)

The `while` loop is another fundamental iteration structure, designed for situations where the number of iterations is not known beforehand. The `while` loop repeatedly executes a block of code as long as a specified condition remains true.

The structure of a `while` loop is: `while (condition) { ... }`

The loop's execution depends entirely on the condition provided in the parentheses. Before each iteration, the condition is checked. If the condition evaluates to true, the code block inside the loop is executed. If the condition is false from the very beginning, the loop body will not execute even once.

Consider the difference between `while` and `do-while` loops. The primary distinction lies in when the condition is checked. In a `while` loop, the condition is checked *before* the loop body is executed. In a `do-while` loop, the loop body is executed *at least once* before the condition is checked.

The structure of a `do-while` loop is: `do { ... } while (condition);`

The `do-while` loop guarantees that the code inside the `do` block will be executed at least one time, regardless of whether the `condition` is initially true or false. This makes `do-while` loops suitable for scenarios where an action must be performed at least once, such as prompting a user for input.

```c
#include <stdio.h>

int main() {
    int count = 5;

    // While loop example
    printf("--- While Loop Example ---\n");
    while (count > 0) {
        printf("%d\n", count);
        count--;
    }
    printf("While loop finished.\n\n");

    // Do-while loop example
    printf("--- Do-While Loop Example ---\n");
    int num = 5;
    do {
        printf("%d\n", num);
        num++;
    } while (num <= 5); // Condition is checked after execution

    printf("Do-while loop finished.\n");

    return 0;
}
```

In the `while` loop example, the loop will continue to execute as long as `count` is greater than 0. In the `do-while` loop example, the code inside the `do` block is executed first, printing the initial value of `num` (which is 5), and *then* the condition `num <= 5` is checked. Since the condition is true initially, the loop body executes at least once. This distinction is important when designing programs that require mandatory initial execution, such as reading input from a user or performing an initial operation before checking further conditions.

### 4.3. Nested Loops (အလွှာလိုက် ထပ်ခါတလဲလဲ လုပ်ဆောင်ခြင်း)

When we need to perform repetitive actions across multiple dimensions, such as in two-dimensional structures, nested loops become indispensable. Nested loops involve placing one loop structure inside another loop. The inner loop is executed completely for every single iteration of the outer loop.

Nested loops are the key to working with multi-dimensional data structures, such as matrices or grids. A classic and practical example is generating multiplication tables or printing patterns.

Consider generating a multiplication table for numbers 1 through 5. We want to print the product of each number multiplied by every other number in the range. This naturally calls for nested loops.

```c
#include <stdio.h>

int main() {
    int start = 1;
    int end = 5;

    printf("--- Multiplication Table (Nested Loops) ---\n");

    // Outer loop controls the rows (the first factor)
    for (int i = start; i <= end; i++) {
        // Inner loop controls the columns (the second factor)
        for (int j = start; j <= end; j++) {
            printf("%d x %d = %d\t", i, j, i * j);
        }
        printf("\n"); // Move to the next line after finishing a row
    }

    return 0;
}
```

In this example, the outer loop, controlled by `i`, iterates from 1 to 5. For each value of `i`, the inner loop, controlled by `j`, iterates from 1 to 5. This means that for `i=1`, the inner loop will execute for `j=1, 2, 3, 4, 5`, printing `1x1=1`, `1x2=2`, ..., `1x5=5`. Then, the outer loop increments `i` to 2, and the inner loop runs again for `j=1, 2, 3, 4, 5`, printing `2x1=2`, `2x2=4`, ..., `2x5=10`, and so on. This nested structure allows us to systematically generate all the products within a defined range, which is the essence of creating multi-dimensional patterns.

As we delve deeper into nested loops, we begin to see how complex, two-dimensional logic can be managed by combining simple looping mechanisms. However, as we combine decision-making (conditionals) with repetition (loops), we must also learn how to manage the flow *within* those repetitive structures.

## 5. Loop Control Statements (Loop ထိန်းချုပ်ခြင်း)

When we use loops, we often need the ability to alter their execution flow mid-iteration. Control flow statements within loops allow us to fine-tune how the loop behaves.

### 5.1. Controlling Loop Flow:

#### `break` Statement:

The `break` statement is used to immediately terminate the execution of the innermost loop it is contained within. When the program encounters a `break` statement, it jumps out of the loop entirely and continues execution at the statement immediately following the loop. This is useful when a specific condition within the loop is met, and there is no need to continue iterating through the rest of the loop.

For instance, in a search algorithm, if we find the item we are looking for, there is no need to continue searching the rest of the list. We can use `break` to stop the search immediately upon finding the target.

#### `continue` Statement:

The `continue` statement serves a different purpose. When the `continue` statement is encountered within a loop, it immediately skips the rest of the current iteration of the loop and proceeds to the next iteration. The loop's control mechanism is then used to evaluate the loop condition again.

This is useful when we want to skip processing for a particular iteration but still want the loop to continue running for the remaining iterations. For example, in processing a list of numbers, if we encounter a number that is negative and we only want to process positive numbers, we can use `continue` to skip the processing of negative numbers and move to the next one.

```c
#include <stdio.h>

int main() {
    int num = 10;

    printf("--- Continue Example ---\n");
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            // Skip the even numbers and go to the next iteration
            continue;
        }
        printf("%d is odd.\n", i);
    }
    printf("Continue loop finished.\n");

    return 0;
}
```

In this example, the loop iterates from 1 to 10. When `i` is even, the `continue` statement is executed, which skips the `printf` statement and jumps directly to the next iteration where `i` is odd. This effectively skips printing the even numbers and only prints the odd numbers.

### 5.2. The Caution of `goto` Statement (goto Statement ၏ သတိထားရမည့်အချက်)

In C programming, there exists a statement called `goto`. The `goto` statement allows for an unconditional jump to a specific labeled point within the same function. While it offers a way to jump control flow, it is crucial to understand why it should generally be avoided in modern, well-structured programming.

The main reason to avoid `goto` is that it can lead to what is often called "Spaghetti Code." Spaghetti code refers to code that has a convoluted and tangled control flow, making it extremely difficult for a human reader to follow the logic of the program. When a program relies heavily on `goto` statements, tracing the execution path becomes a nightmare, especially in larger and more complex programs.

Control flow should ideally be managed by the structured constructs we have already discussed: `if`, `switch`, `for`, and `while` loops. These structures provide clear, well-defined ways to control the flow of execution in a predictable manner. Using `goto` to manage simple branching or iteration introduces arbitrary jumps that obscure the logical flow and make the code much harder to debug, maintain, and understand for both the programmer and other developers. Therefore, we should strive to use structured control flow mechanisms to build logical and readable programs.

## 6. Practical Application: Real-World Programming (လက်တွေ့ အသုံးချခြင်း)

The theoretical understanding of control flow becomes truly tangible when we apply it to solve real-world problems. By combining conditional logic, looping, and flow control, we can build interactive and dynamic programs.

### 6.1. Pattern Printing Programs:

One of the most illustrative applications of nested loops is the printing of patterns. We can use nested `for` loops to control the rows and columns of output, allowing us to print patterns of stars, triangles, or other geometric shapes.

Let's demonstrate how to print a right-angled triangle pattern using nested loops.

```c
#include <stdio.h>

int main() {
    int rows = 5;

    printf("--- Right-Angled Triangle Pattern ---\n");

    // Outer loop controls the number of rows
    for (int i = 1; i <= rows; i++) {
        // Inner loop controls the number of stars to print in the current row
        for (int j = 1; j <= i; j++) {
            printf("* ");
        }
        printf("\n"); // Move to the next line after printing a row
    }

    return 0;
}
```

In this program, the outer loop iterates from 1 to 5, controlling the number of rows. The inner loop iterates from 1 to the current value of `i`. This means in the first row (`i=1`), the inner loop runs once, printing one star. In the second row (`i=2`), the inner loop runs twice, printing two stars, and so on. This nested structure allows us to dynamically print a triangle of stars with the correct number of stars in each row.

### 6.2. Number Guessing Games:

Interactive games are excellent ways to apply control flow concepts in a practical context. A number guessing game is a perfect example. We can use a `while` loop to keep prompting the user for input until they enter a correct guess.

```c
#include <stdio.h>

int main() {
    int secretNumber = 42;
    int guess;

    printf("Welcome to the Number Guessing Game!\n");

    // Use a while loop to keep asking for input until the guess is correct
    do {
        printf("Please guess a number between 1 and 100: ");
        scanf("%d", &guess);

        if (guess < 1 || guess > 100) {
            printf("Please enter a number within the range (1-100).\n");
        } else if (guess < secretNumber) {
            printf("Too low! Try again.\n");
        } else if (guess > secretNumber) {
            printf("Too high! Try again.\n");
        } else {
            printf("Congratulations! You guessed the correct number: %d!\n", secretNumber);
        }
    } while (guess != secretNumber);

    return 0;
}
```

This program uses a `do-while` loop to ensure that the user is prompted for input at least once. The loop continues as long as the `guess` is not equal to `secretNumber`. Inside the loop, we use `if-else if-else` statements to provide feedback to the user based on whether their guess is too low, too high, or correct. This demonstrates how conditional statements and loops work together to create an interactive and responsive experience.

### 6.3. Simple Game Logic:

Game logic is heavily dependent on decision-making. We can use `if-else` statements to manage the different states of a game. For example, in a simple game, we can check the player's score to determine if they have won, lost, or need to continue playing.

```c
#include <stdio.h>

int main() {
    int score = 0;
    int game_over = 0;

    printf("--- Simple Game Logic ---\n");

    // Simulate a few turns
    for (int i = 0; i < 3; i++) {
        printf("Turn %d: You scored 10 points.\n", i + 1);
        score += 10;
    }

    // Decision making based on score
    if (score >= 30) {
        printf("Congratulations! You won the game!\n");
    } else {
        printf("Game Over. You need more points to win.\n");
    }

    return 0;
}
```

Here, we use a `for` loop to simulate a game progression and accumulate a score. After the loop finishes, we use an `if-else` statement to check the final `score` and determine the outcome of the game. This shows how control flow allows us to manage the sequence of events and make decisions based on the accumulated results, forming the core logic of any game.

## 7. Chapter Summary (အခန်းအကျဉ်းချုပ်)

Control Flow is the fundamental concept that governs the entire execution of a program. It is the mechanism that allows a program to make decisions and repeat actions, moving beyond simple sequential execution.

**Key Takeaways:**

*   **Decision Making:** We learned that `if/else` and `switch` statements provide the means to implement conditional logic, allowing the program to choose different paths based on conditions.
*   **Repetition:** We explored the power of loops—`for`, `while`, and `do-while`—to execute blocks of code multiple times, which is essential for efficiency and handling large datasets.
*   **Control:** Statements like `break` and `continue` allow us to precisely manage the flow *within* loops, enabling fine-grained control over the iteration process.
*   **Avoid `goto`:** We emphasized that while `goto` exists, it should be avoided in favor of structured control flow mechanisms (`if`, `switch`, loops) to write clear, maintainable, and bug-free code.

**Final Thought:** Mastering Control Flow is not just about learning syntax; it is about understanding the logic of how instructions are sequenced, branched, and repeated. It is the foundational bedrock upon which all complex, intelligent, and functional software is built. By mastering these concepts, you gain the ability to write programs that are not just instruction sets, but dynamic systems capable of responding intelligently to the world.