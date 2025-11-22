## Presentation

Present code in such a way to maximise readability, without affecting the program logic.

### Layout

Good use of space in both dimensions to make the code more readable:

- horizontal indentation to create code blocks
- horizontal alignment to make pattern-matching & guards more easily readable.
- vertical spacing between functions and code blocks in larger functions to visualise structure
- ordering of code withing larger functions according to functionality
- ordering of functions to create groups with similar functionality.
- breaking up long lines of code to form a code block (different clauses of a list comprehension, aligned horizontally)

Avoid very long lines or large or dense blocks of code.

### Naming

Balance between concise and descriptive

- fixed naming convention such as camelCase or snake_case
- defined functions should be given descriptive names, never single letters. Avoid abbreviations.
- parameters should generally be given single letter names, except when there are many of them or when used in larger functions with a large distance between input and calculation.
- consistency with variable names, especially for single letter variables (`f`, `g`, `h` for functions, `i`, `j`, `k` for indices, `n`, `m` for numbers, and `str` for strings) and using a prime for very similar or derived values (`xs` and `xs'`).
- adhere to conventional nomenclature, such as:
	- nouns for values,
	- verbs for functions,
	- plural (`xs`) for lists,
	- `show-` for returning displayed strings
	- `print-` for printing to console
	- `is` for boolean checks

### Commenting

Purpose is to provide formal documentation of written code, including an informative description of the functionality implemented aimed at professional maintainers.

Code should generally be “self-commenting”, such that it is transparent and can be read English-like.

Mid-function comments should be used sparingly. They can be used to introduce code blocks in longer IO functions, to recall conditions in conditional branches (particularly `else` branches), or to recall implicit constraints in data being processed (for instance that an input list is assumed to be sorted)

Comments should describe what your code intends to do, not how it does it. They are about meaning, not the implementation itself. The exception here is when a familiar, popular algorithm is being implemented (i.e. BFS, DQN).

## Technique

### Constructions

The best method to use for a particular scenario is one that maximises transparency and readability

#### List Processing and Iteration

| Level         | High Priority                                   | Medium Priority                                                                                | Low Priority                                                  |
| ------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Name          | List Comprehensions                             | Map, Filter, Fold                                                                              | Explicit Recursion                                            |
| Justification | “highly transparent”                            | “concise”, but “not very flexible”                                                             | “extremely powerful”, however “verbose, not very transparent” |
| Use           | Must be returning a list                        | The operation is a standard mapping or filtering where intent is obvious without complex logic | When you cannot achieve the result with the other method.     |
| Note          | When breaking up long lines, align horizontally |                                                                                                | Avoid mutual recursion if not necessary.                      |

#### Conditional Logic and Control Flow

| Level         | Top Priority                                                           | Lower Priority                                            |
| ------------- | ---------------------------------------------------------------------- | --------------------------------------------------------- |
| Name          | Pattern Matching & Guards                                              | If-Then-Else                                              |
| Justification | “Visualise the structure of the code”                                  | Nesting is discouraged                                    |
| Use           | Avoid redundant pattern matching where branches are treated similarly. | When nesting does not take place                          |
| Note          | Horizontal alignment is necessary.                                     | Never use `if x then True else False` as this is just `x` |

#### Code Organisation and Abstraction

| Level         | High Priority                                     | Conditional Priority                                                                      |
| ------------- | ------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Name          | where clauses                                     | Partial Application & Function Composition                                                |
| Justification | Useful to “organise your code”                    | Make most of the code obscure, can only be used in special cases.                         |
| Use           | Break complex calculations down into named parts. | Do not use if they obscure parameters or behaviour, only if they make code more readable. |

### Functions

Clear functions with a logical purpose, so they can be readily understood and remembered.

Avoid obscure parameters and/or behaviour.

Purpose of a function should be obvious from its name and type signature and, if absolutely necessary, comments.

---

Large function bodies are difficult to inspect.

### Algorithms

Simple, transparent algorithms of the right complexity.

Readability > Pure speed, however an obviously inefficient algorithm is unexpected, meaning it takes more time to understand the program.

### Abstraction

Same functionality that is required in multiple places should be abstracted into a single function called several times.

Should serve a logical purpose rather than carrying a large number of parameters to handle different cases.