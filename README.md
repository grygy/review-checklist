# Code review checklist

This is a base checklist for code reviews. It starts with basics for most technologies and languages, followed by more specific items regarding the language or technology.

It is based on my knowledge and included resources. It is not complete and will be updated.


## General

#### 1. Code is readable and understandable

- I know that you want to show your powers and write oneliners everywhere or technology specific hacks, but please don't. Write the code as simple as possible. You are not writing code for yourself but for your colleagues. Even your future self will be thankful for that.

#### 2. Minimize the use of comments

- Try not to use comments in your code. If you need to explain your code, it means that it is not readable enough.

#### 3. Code consistency within the project
    
- Code is consistent with the rest of the project even if it's not the most cutting edge formatting, naming, etc. --> If you want to change it, do it in the whole project (could end up badly).

#### 4. DRY (Don't repeat yourself)

- If you have to repeat yourself, you are doing something wrong. Try to find a way to reuse your code. Introduce abstraction, do some refactoring, etc.

#### 5. Use meaningful names

- Use meaningful names for variables, methods, classes, etc. Do not use abbreviations. Do not use single letter names. Do not use names like `v`, `value`, `res`, `data`, etc. Use names that describe what the variable, method, class, etc. is doing (e.g. `courseDurationInDays`)
- Use prefix `is` or `has` for booleans. Do not use negations in variable names (e.g. `isUserNotActive`).
- Add units to variables (e.g. `courseDurationInDays` instead of `courseDuration`)
- Every language has its own naming conventions. Follow them. 

#### 6. Never use string literals or magic numbers

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

#### 7. Refactoring is a must for bigger projects

- Before submitting your code for review, look at your code one more time and think about what can be improved. Do some refactoring.

#### 8. Test your code

- Just write the tests. (It's essential)

#### 9. Clean Git history and descriptive commit messages

- Well, this is hard. Set up with your team clear rules on how branches and commit messages should look like.
- Commit, commit, commit. Smaller commits are better than one big commit.
- I like adding the ticket (issue) number to the end of the message (e.g. `Add new document file input (#123)`).
- Check out this [article](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/) for more information about commit messages.

#### 10. SOLID

- S : The single-responsibility principle: "There should never be more than one reason for a class to change. In other words, every class should have only one responsibility."
- O : The open–closed principle: "Software entities ... should be open for extension, but closed for modification."
- L : The Liskov substitution principle: "Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it. See also design by contract."
- I : The interface segregation principle: "Many client-specific interfaces are better than one general-purpose interface."
- D : The dependency inversion principle: "Depend upon abstractions, [not] concretions."

#### 11. Design patterns

- Use design patterns when needed. Do not overuse them. Do not use them just because you can.
- Check out [Refactoring Guru](https://refactoring.guru/design-patterns) for GoF design patterns.
- Check out POSA patterns.
- Check out AOM patterns. You can read the basics [here](https://www.adaptiveobjectmodel.com/WICSA3/ArchitectureOfAOMsWICSA3.pdf).

#### 12. Pipelines checking

- Implement pipelines that will statically check the code before merging it to the main branch. 

## 1. TypeScript

1. Use variable or helper method for complicated expressions. Do not use complicated expressions directly in `if` statement.

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

3. Use linter and formatter like [ESLint](https://eslint.org/) and [Prettier](https://prettier.io/).

    - Set up pipelines for checking the code before merging it to the main branch.
    - Set up your IDE to format the code on save.
    - I recommend using `@haaxor1689/eslint-config` and `@haaxor1689/prettier-config` packages.



4. Don't be lazy and use meaningful names in `map`, `filter`,... functions.
    
    ```typescript
    // Bad
    const userNames = users.map((u) => u.name);

    // Good
    const userNames = users.map((user) => user.name);
    ```

5. Do not use `any`
    
    - Use specific type instead of `any`.
    - I recommend using [Zod](https://zod.dev/) library for types and type checks.
    - Use `type` instead of `interface`.

6. Use arrow functions
    ```typescript
    // Bad
    function sum(a: number, b: number): number {
        return a + b;
    }

    // Good
    const sum = (a: number, b: number): number => a + b;
    ```

7. Use `async/await` instead of `then` chains
    ```typescript
    // Bad
    fetch('https://example.com')
        .then((usersResponse) => usersResponse.json())
        .then((users) => console.log(users));

    // Good
    const usersResponse = await fetch('https://example.com');
    const users = await usersResponse.json();
    console.log(users);
    ```


### 1.1 React 
1. Use functional components. Classes and constructors are obsolete.
2. Use at least ES6 syntax with hooks (useState, useEffect, useRef, etc.)
4. Check incoming data from server with `zod` or another library. (It's good to use GraphQL)
5. Use `useMemo` and `useCallback` for memoization.
6. Handle errors with `try/catch/finally` blocks, especially from Backend.
7. Use [TanStack Query](https://tanstack.com/query/latest) for managing async calls to backend.
    1. You can use it for managing the cache.

        ```typescript
        // Bad
        const [users, setUsers] = useState<User[]>([]);
        useEffect(() => {
            fetch('https://example.com/users')
                .then((usersResponse) => usersResponse.json())
                .then((users) => setUsers(users));
        }, []);

        // Good
        const { data: users } = useQuery<User[]>(['get', 'users'], () => {
            const usersResponse = await fetch('https://example.com/users');
            return usersResponse.json();
        });
        ```


## Resources
- https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/
- https://www.techighness.com/post/react-js-code-review-checklist/
- https://dev.to/michi/tips-on-naming-boolean-variables-cleaner-code-35ig
- https://workat.tech/machine-coding/tutorial/writing-meaningful-variable-names-clean-code-za4m83tiesy0
- https://microsoft.github.io/code-with-engineering-playbook/code-reviews/process-guidance/reviewer-guidance/