
# GoodStrings Engineering Team Coding Standards

This document serves as the a guide of GoodStrings Inc. Engineering Team’s codebases, covering how the codes should be formatted as well as efficiently using version control. Our goal is to ensure a consistently high-quality codebase that is easy to read and contribute to, especially for newcomers.

You are not forced to follow these standards. However, you are expected to at least meet the bare minimum.

---

## General Guidelines
- Write **clean and readable code**.
- Follow the **DRY (Don't Repeat Yourself)** and **KISS (Keep It Simple, Stupid)** principles.
- Use meaningful and descriptive variable and function names.
- Add comments and documentation where necessary.
- Use version control (e.g., Git) with meaningful commit messages.

---

## PHP Standards
### General Guidelines
- Use the latest supported PHP version.
- Adhere to [PSR-12 coding style](https://www.php-fig.org/psr/psr-12/).

### File conventions
- It is recommended to use 4 spaces instead of tabs as indents.
- Files must start with `<?php` and you must omit `?>` at the end of file.
- There must always be a `namespace` on each file.
- `namespace` must be written on one newline after `<?php`.

### Naming Conventions
- Class names: `PascalCase` (e.g., `UserController`).
- Method names: `camelCase` (e.g., `getUserData`).
- Variable names: `camelCase` (e.g., `$userName`).
- Constants: `UPPER_SNAKE_CASE` (e.g., `MAX_ATTEMPTS`).

### Code Structure
- Separate logic into classes and methods.
- Use namespaces to avoid class name conflicts.
- Avoid mixing HTML and PHP; use templates for rendering views.

### Security
- Use prepared statements for database queries to prevent SQL injection.
- Validate and sanitize user input.
- Avoid exposing sensitive information in error messages.


### Defining class
- You must put a newline before `{` in class definitions. Also `extends` and `implements` must be written on the same line as the class name.
- The `abstract`/`final`/`trait` keywords must come before class definition.
- You must add an `Abstract` prefix to an abstract class name.
- You must add an `Interface` suffix to an interface class name.
- You must add a `Trait` suffix to a trait name.
```php
class ClassName extends AnotherClassName implements Interface
{
    // Code here...

    return $someStuffs;
}
...
abstract class AbstractClassName
{
    // Code here...

    return $something;
}
...
interface ClassNameInterface
{
    // Code here...
}
...
trait SomeTrait
{
    // Code here...
}
```

### Defining properties
- You must not omit `public`/`private`/`protected` modifiers.
- You should always explicitly write `public` as the default modifier.
- The `static` keyword must come after the modifiers.
- You must not use `var` when defining properties because you can't add modifiers.
- You must not define two or more properties in one statement.
```php
class ClassName
{
    public $propertyOne;
    private $propertyTwo;
    protected static $staticProperty;
}
```

### Defining functions/methods
- You must put a new line before `{` in function definitions.
- You must not omit `public`/`private`/`protected` modifiers.
- You should always explicitly write `public` as the default modifier.
- The `abstract`/`final` keywords must come before the modifiers.
- You must not put any spaces before `(` and after `)`.
- You must not put any whitespaces before commands in arguments, put them after instead.
- You must always use type hinting on arguments to specify the expected data type.
- When possible, you must declare the return type of a function/method.
- If there are too many arguments, you must put a newline after `(` and write one argument per line. You should also write `)` and `{` on the same line, seperated by a whitespace.
```php
class ClassName
{
    abstract protected function doSomething(array $data): Array
    {
        // Code here...

        return $array;
    }

    public function somethingWasDone(string $status, int $code): Class
    {
        // Code here...

        return $classInstance;
    }

    public function tooMany(
        string $name,
        int $status,
        array $otherData
    ) {
        // Code here...
    }
}
```

### Defining conditional statements
- You must not put newline before curly braces.
- You must put one space before `(` and after `)`.
- You must not put any whitespaces after `(` and before `)`.
- If there are too many arguments, you must put a newline after `(` and write one argument per line. You should also write `)` and `{` on the same line, seperated by a whitespace.
```php
if ($condition == true) {
    // Code here...
}
...
if (
    $condition == true &&
    ($condition1 == $condition2) ||
    $condition3 != 'some condition here'
) {
    // Code here...
}
```

### Conditional statements comparison
- You must have the check target of the comparison on the right.
```php

if ($condition == null) {
    // Code here...
}
```

### Commenting/Documenting code
- Single-line and multi-line comments must start with `/**` and end with `*/`.
- You must always include a comment on class variables.
- Refrain from commenting on a function if the function name already explains what the function is for, except for functions in `repository` interfaces.
- `Repository` interface functions must always have a comment on what the function is for.
- `Repository` class functions must not have any comments.
- You must always use `@var` for variable type comments.
- You must always use `@param` for parameter type in comments.
- You must always use `@return` for return type in comments.
- There must always be two whitespaces between `@param` and `data type`.
- There must always be a short description on each `@param` comments.
```php
class ClassName
{
    /** @var VariableType */
    public $classVariable;

    /**
     * This is the function description where you explain what
     * the function does.
     *
     * @param  Model $id the user's unique id
     * @param  array $otherData user's other data
     * @return Array
     */
    public function someFunction(Model $id, array $otherData): Array
    {
        // Code here...

        return $arrayType;
    }
}
```

---


## Laravel Standards
### Folder Structure
- Follow Laravel's default structure.
- Place business logic in **Service** or **Repository** classes, not controllers.

### Naming Conventions
- Controllers: Singular and descriptive (e.g., `UserController`).
- Models: Singular (e.g., `User`).
- Routes: Use snake_case for route names (e.g., `get_user_profile`).

### Best Practices
- Use **Eloquent ORM** for database interactions.
- Use **Form Requests** classes for validation to keep controllers clean.
- Use relationships and scopes to simplify database queries
- Use **database transactions** where `multiple` related database operations occur, especially during `create`, `update`, or `delete` processes across multiple tables
- Leverage Laravel's **events, queues, and jobs** for heavy or background tasks.
- Avoid logic in `Blade` templates; use `controllers` or view composers.
- Use environment variables for configuration (`.env` file) for example `config('app.timezone')` instead of hardcoding

### Database Management
- Use `migrations` for all database schema changes.
- Use `seeders` for test or initial data population.
- Use `factories` for creating test data in tests

### Error Handling
- Use Laravel’s built-in `exception` handling for consistency.
- Customize exceptions when necessary (`app/Exceptions`).

### Security
- Use **CSRF protection** for forms.
- Sanitize user inputs to prevent SQL injection.
- Use `$request->input()` or `$request->get()` instead of `$_POST` or `$_GET`.
- Avoid mass assignment vulnerabilities; use `$fillable` or `$guarded` in models.
- Hash passwords using Laravel's built-in `Hash` facade.
- Enable HTTPS and use middleware like `VerifyCsrfToken`

---


## JavaScript Standards
### General Guidelines
- It is recommended to use `2 spaces` instead of tabs as indents.
- `import` of modules must always be at the top.
- `export` statements must always be at the bottom.
- You must omit `;` as it makes chaining easier and commit diffs cleaner.

### Naming Conventions
- Variables and functions: `camelCase` (e.g., `fetchData`).
- Constants: `UPPER_SNAKE_CASE` (e.g., `API_BASE_URL`).

### Best Practices
- `var` should not be used when defining variables, use `let` or `const` instead.
- Use `async/await` for asynchronous operations.
- Use modern array methods like `.map()`, `.filter()`, and `.reduce()` instead of loops where applicable.
- Lint your code using ESLint with a consistent configuration.

### Security
- Avoid using `eval()` or dynamically building code.
- Validate user input to prevent XSS (Cross-Site Scripting).
- Use HTTPS and secure cookies when working with APIs.

### Other JavaScript rules
- For rules that are not mentioned here, please refer to [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

---


### NPM
- When installing third-party packages, it should always be the latest version when available.
- Third-party packages in `package.json` file must have a fixed version number to avoid breaking changes.
```json
{
    "dependencies": {
        "npm-package": "1.10.11"
    }
}
```

---


## Vue.js Standards
### File Structure
- Organize files by feature/module (e.g., `components`, `views`, `store`)
- Limit folder nesting to keep the structure simple and easy to navigate
- Use `PascalCase` for component file names (e.g., `UserProfile.vue`).
- For additional VueJS style guide, please refer to [VueJS Style Guide](https://vuejs.org/v2/style-guide/)
- For additional VueJS best practices, please refer to [VueJS Best Practices](https://012.vuejs.org/guide/best-practices.html)

### Naming Conventions
- Component names: `PascalCase` (e.g., `<UserProfile />`).
- Props: `camelCase` (e.g., `userName`).

### Component Structure
- Template: Place HTML structure.
- Script: Add logic and data management.
- Style: Scoped CSS for local styles.

### Best Practices
- Use **Vuex** for state management in large applications.
- Use **props** to pass data to child components and **emit** for communication back to parent components.
- Avoid large components; split them into smaller, reusable components.
- Use **key** attributes for lists and dynamic elements
- Validate props with `types` and `default` values

---

## CSS
- You are to follow [Airbnb CSS Style Guide](https://github.com/airbnb/css)

---

## Git
### Workflow
- The [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) must be strictly followed.
- While it's easier to use the `git-flow` library, it's recommended to use vanilla git instead.

### Branches
- The `main` branch is the default branch and is also a protected branch.
- The `develop` branch will contain the complete history of the project. This is also the parent branch of all `feature` branches.
- The `feature` branch will contain the code for each product feature. Each new product feature should reside in its own branch. When a feature is complete, it gets merge back into `develop` branch.
- The `hotfix` branch will be used to quickly patch critical bugs in production releases, it will branch-out of the `master` branch and be merged back into it and `develop` as soon as the fix is complete.
- The `release` branch will branch-out of the `develop` branch once it has acquired enough features for a release. Once it's ready to ship, it will merge into `master` and tagged with a version number and should also be merged back into `develop` if changes occured since the release was initiated.
- `feature`, `hotfix`, and `release` branches must be deleted right after they are merged to reduce clutter.

### Naming conventions
- `feature` branches should be have a prefix of `feature/`.
- `hotfix` branches should have a prefix of `hotfix/`.
- `release` branches should have a prefix of `release/`.
- `Alpha` and `Beta` releases must have a prefix of `alpha_` and `beta_`.
- All versions must have a prefix of `v` (i.e v1.0.1).
```sh
git checkout -b feature/feature-name
git checkout -b hotfix/hotfix-name
git checkout -b release/beta_v1.0.1
```

### Commits
- Commit messages should briefly explain what the changes are.
- You must follow the "commit small, commit often" practice which makes it easier for everyone to integrate changes regularly and avoid massive merge conflicts.
- Do not commit half-done work, specially if it's a breaking change.

### Pull Requests
- Pull Request titles should briefly explain what the PR is for.
- Pull Request descriptions should include a list of changes included in the PR and other relevant information.
- You must update your branch and fix merge conflicts on your local machine before creating a Pull Request.

### Code Reviews
- All code must be reviewed by at least one team member before merging.
- Code review must be requested to the Engineering Lead or CTO.
- During code review, there will be checks including but is not limited to:
    - Formatting and architecture
    - Reusability and reliability
    - Scalability and performance
    - Security and documentation
 
---

## Testing
- TODO

---

## Additional Notes
- Keep dependencies updated.
- Write unit tests and integration tests.
- Use environment variables (`.env`) for sensitive data.
  
---

### License
MIT License

**Copyright (c) 2020 GoodStrings Inc.**

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

