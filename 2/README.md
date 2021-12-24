# 2. Functions and Macros

## Setting variables (local to script)

```cmake
set(MYVAR "Hello")
```

## Print stuff to stdout

```cmake
message("Hello, World!")
message("") # empty line

# Dereference variables with ${var}
message(${MYVAR})
message(${PROJECT_NAME})
```

## Define Functions and Macros!

- Funcitons have scope, but Macros are inline and side effect of them can leak

- Print local (to cmake script) variables
```cmake
function(print_var var)
    message("${var} = ${${var}}")
endfunction()

print_var(MYVAR)
```

- Print env variables

```cmake
function(print_env)
    foreach(var ${ARGN})
        message("${var} = $ENV{${var}}")
    endforeach()
endfunction()

print_env(HOME)
```

- Variadic arguments
```cmake
function(print_many)
    # message("Argument list: ${ARGN}")
    # message("Argument count: ${ARGC}")
    # message("0th Argument: ${ARGV0}")
    # message("1nd Argument: ${ARGV1}")
    # message("2rd Argument: ${ARGV2}")

    # Loop over list of argument
    foreach(var ${ARGN})
        print_var(${var})
    endforeach()
endfunction()

print_many(MYVAR PROJECT_NAME)
```

NOTE: Prefer funcitons over macros unless you have a good reason not to do so
