# Prevention against Command Injection

The most effective way to prevent OS command injection vulnerabilities is to never call out to OS commands from application-layer code.

In almost all cases, there are different ways to implement the required functionality using safer platform APIs.

## Defence Option 1

Avoid calling OS command directly. Built in library functions are a very good alternate to OS commands, as they cannot be manipulated to do something other than what they are intended to do.

## Defence Option 2

The `escapeshellarg()` surrounds the user input in single quotes, so if malformed user input is something like `& echo "hello"`. 
In this defense type, even thouse the shell arguments are escaped it can still pass one OS command from the user.

For example:

```bash
whoami & echo "hello"
```

This user input will be treated as `whoami '& echo "hello"'`, thus it will execute only whoami command.

This is not a effective a solution as a threat actor would still be able to execute a Os command of his wish.

## Defence Option 3

Parameterization in conjuction with input validation

If a system incorporates user-supplied input and system command, and if it cannot be avoided, the following   two layer of defence should be used to prevent OS injection attacks.

Layer 1: Parameterization

Use structured mechanisms that automatically enforces the separation of data and command.

Layer 2: Input validation

- Allow list input validation: Where the arguments allowed are explicitly defined.
- Allowlist regular expression: regular expression only allows lowercase letters and numbers and does not contain metacharacters.
- he length is also being limited to 3-10 characters: `^[a-z0-9]{3,10}$`
