# Refactoring

We've scanned our projects using the [SonarCloud](https://sonarcloud.io/) to identify common code smells. The following points were found:

## 🧠 Cognitive Complexity

Cognitive complexity in programming refers to the level of mental effort required to understand and reason about a piece of code. 
It's a measure of how difficult it is to comprehend the flow of data and control within a program. 
When code has a high level of cognitive complexity, it can be difficult to maintain, debug, and extend.

To reduce cognitive complexity, we need to write code that is easy to understand and follow. 
There are several techniques we used to help accomplish this, such as:

* Breaking up code into smaller, more manageable functions or modules.
* Using clear and descriptive names for variables, functions, and classes.
* Avoiding deep nesting of control structures like if-else statements and loops.
* Writing comments and documentation to explain the intent and purpose of the code.

## 🛴 TODO

Dangling TODO comments are leftover comments in the code that indicate unfinished work or areas that require further attention. 
These comments can be helpful during development but can be problematic when left in the codebase after the work is complete. 
They can accumulate over time, making it difficult to determine which comments are still relevant and which ones have been resolved.

For example, the [RALF-engine](https://github.com/RALF-Life/engine) contained this dangling TODO comment:

```go
if err := yaml.Unmarshal(ctx.Body(), &cnt); err != nil {
    // TODO: close body?
    return err
}
```

To identify dangling TODO comments in the future, we will make use of JetBrains IDEs which warn you if you push commits to Git containing TODO comments.

## 🐳 Dockerfile

It was also identified that some of our `Dockerfile`s contain the following line:

```dockerfile
COPY . .
```

which can lead to sensitive data being copied to the Docker image because of recursively copying the data.

To fix this, we added a `.dockerignore` file which explicitly ignores files that can contain sensitive data.
