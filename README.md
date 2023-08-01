# Code review checklist

This is a base checklist for code reviews. It stars with basics for most technologies and languages followed by more specific items regarding the language or technology.

It is based on my knowledge and included resources. It is not complete and will be updated.


## General

#### 1. Code is readable and understandable

- I know that you want to show your powers and write oneliners everywhere or technology specific hacks, but please don't. Write the code as simple as possible. You are not writing code for yourself, but for your colleagues. Even your future self will be thankful for that.

#### 2. Do not use comments

- Try not to use comments in your code. If you need to write comments, it means that the code is not readable enough.

#### 3. Code consistency within project
    
- Code is consistent with the rest of the project even if it's not most cutting edge formatting, naming, etc. --> If you want to change it, do it in the whole project (could end up badly).

#### 4. Follow naming conventions

- Every language has its own naming conventions. Follow them. 

#### 5. DRY (Don't repeat yourself)

- If you have to repeat yourself, you are doing something wrong. Try to find a way to reuse your code. Introduce abstraction, do some refactoring, etc.

#### 6. Use meaningful names

- Use meaningful names for variables, methods, classes, etc. Do not use abbreviations. Do not use single letter names. Do not use names like `v`, `value`, `res`, `data`, etc. Use names that describe what the variable, method, class, etc. is doing (e.g. `courseDurationInDays`)
- Use prefix `is` or `has` for booleans. Do not use negations in variable names (e.g. `isUserNotActive`).
- Add units to variables (e.g. `courseDurationInDays` instead of `courseDuration`)

#### 7. Never use string literals or magic numbers

- Do not use string literals or magic numbers in your code. Use constants or variables instead.

    ```java
    // Bad
    void printParkingSpots() {
        for (int i = 0; i < 100; i++) {
            System.out.println(parkingSpots[i]);
        }
    }

    // Good
    final int NUMBER_OF_PARKING_SPOTS = 100;

    void printParkingSpots() {
        for (int i = 0; i < NUMBER_OF_PARKING_SPOTS; i++) {
            System.out.println(parkingSpots[i]);
        }
    }
    ```

#### 8. Refactoring is a must for bigger projects

- Before submitting your code for review, look at your code one more time and think what can be improved. Do some refactoring.

#### 9. Test your code

- Just write the tests. (It's really important)

#### 10. Clean Git history and descriptive commit messages

- Well, this is hard. Set up with your team clear rules how branches and commit messages should look like.
- Commit, commit, commit. Smaller commits are better than one big commit.
- I like adding ticket (issue) number to the end of the message (e.g. `Add new document file input (#123)`).
- Check out this [article](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/) for more information about commit messages.

#### 11. SOLID

- S : The single-responsibility principle: "There should never be more than one reason for a class to change. In other words, every class should have only one responsibility."
- O : The open–closed principle: "Software entities ... should be open for extension, but closed for modification."
- L : The Liskov substitution principle: "Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it. See also design by contract."
- I : The interface segregation principle: "Many client-specific interfaces are better than one general-purpose interface."
- D : The dependency inversion principle: "Depend upon abstractions, [not] concretions."

#### 12. Design patterns

- Use design patterns when needed. Do not overuse them. Do not use them just because you can.
- Check out [Refactoring Guru](https://refactoring.guru/design-patterns) for GoF design patterns.
- Check out POSA patterns.
- Check out AOM patterns.

## 1. TypeScript

1. Use variable or helper method for complicated expression. Do not use complicated expression directly in `if` statement.

    ```typescript
    // Bad
    if (user.active && user.name === 'John') {
        // ...
    }

    // Good
    const isJohnActive = user.active && user.name === 'John';
    if (isJohnActive) {
        // ...
    }
    ```

2. Use `const` for variables that are not reassigned and `let` for variables that are reassigned.
    
    ```typescript
    // Bad
    let user = this.props.user;
    user = { name: 'John' };

    // Good
    const user = this.props.user;
    user.name = 'John';
    ```




### 1.1 React 
1. Use functional components. Classes and constructors are obsolete.
2. Use at least ES6 syntax with hooks (useState, useEffect, useRef, etc.)
3. Use arrow functions for callbacks with async/await.



## Resources
- https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/
- https://www.techighness.com/post/react-js-code-review-checklist/
- https://dev.to/michi/tips-on-naming-boolean-variables-cleaner-code-35ig
- https://workat.tech/machine-coding/tutorial/writing-meaningful-variable-names-clean-code-za4m83tiesy0