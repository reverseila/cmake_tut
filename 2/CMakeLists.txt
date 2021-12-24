cmake_minimum_required(VERSION 3.22)

project(hello
    LANGUAGES CXX
    VERSION 1.0
    DESCRIPTION "This project simply prints hello to the stdout"
    HOMEPAGE_URL "https:/github.com/reverseila")

add_executable(hello hello.cpp)


###############################################################################
# --- Set Variables ---
###############################################################################

set(MYVAR "Hello, World")


###############################################################################
# --- Print Strings to stdout ----
###############################################################################

# you can de-reference variables like PROJECT_NAME to get back their values

message("PROJECT NAME = ${PROJECT_NAME}")
message(${MYVAR})
message("") # Empty line

message("")
message("-----------")
message("")

###############################################################################
# --- Write a function ---
###############################################################################

# Print local variables to cmake script
function(print_var var)
    message("${var} = ${${var}}")
endfunction()

print_var(MYVAR)

# Print project information
message("Project info:")
print_var(PROJECT_NAME)
print_var(PROJECT_VERSION)
print_var(PROJECT_DESCRIPTION)
print_var(PROJECT_HOMEPAGE_URL)

message("")
message("-----------")
message("")

# Print env variables
function(print_env)
    foreach(var ${ARGN})
        message("${var} = $ENV{${var}}")
    endforeach()
endfunction()

print_env(HOME)

# Variadic arguments
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

message("")
message("-----------")
message("")


###############################################################################
# --- Function vs Macro and note on scope ---
###############################################################################

set(VARIABLE "hello")

function(func)
    set(VARIABLE "bye")
    message("function scope: ${VARIABLE}")
endfunction()

macro(mac)
    set(VARIABLE "bye")
    message("macro scope: ${VARIABLE}")
endmacro()

func()                               # bye
message("global scope: ${VARIABLE}") # hello
mac()                                # bye
message("global scope: ${VARIABLE}") # bye

# Unless you need the side effect to leak out, use/prefer functions
