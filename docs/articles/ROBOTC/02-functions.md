# Functions

This document will explain what functions in ROBOTC are, and how to use them to facilitate your programming experience.

# What is a function?

Functions are a group of operations or instructions that will run together and return a value.

It is way easier and much faster to use functions while coding, in any coding scenario.

Please supplement this reading with [this link](https://www.tutorialspoint.com/cprogramming/c_functions.htm) for more information about functions, how to define them, and how to use them.

# Declaring and Defining a function

Here is the basic structure behind declaring and defining a function:

``` c
return_type function_name( parameters ) {
    // Instructions here!
}
```

Of course, you would have to replace return_type, function_name, and parameters with your desired return type, function name, and parameters.

## Return type

Your return_type can be any variable type (`int, float, double, short, etc `). Return type `void` will not return anything.

At the end of your function, for all functions that are not of ```void ```, you will need to put a return statement, using `return calculated_value`, where you would replace calculated_value with your calculated value.

## Function Names

Your function name should describe the function you are creating, for easy usage later. It can be really annoying to have to find out which function you need to call in certain scenarios, so be sure to name your function something easy to remember and understand.

When naming both variables and functions, it is nice to use proper naming conventions, such as camelCase, PascalCase, snake_case, etc.

## Parameters

Your parameters are your use-specific variables, that will change based on the different places you will call them. This will make more sense in practice and by viewing examples.

To define your wanted parameters, use a comma separated list. For example, in the structure above, replace "parameters" with: `parameter1_type parameter1_name, parameter2_type parameter2_name, etc`

# Calling a function

To call a function after it has been named, do the following:

```
function_name( param_value, param_value, etc );
```

This will execute the instructions provided in the function definition!

# Issues with function declaration order

One unfortunate aspect of C is the fact that function declaration order matters. In order to use a function, you would have to declare it before you call it. Luckily, we can declare a function without defining it by doing the following:

``` c
return_type function_name( parameters );
```

You will have to define the function again later like normal, but by putting these at the top of our file, the compiler will know that the function is coming.

# Examples

Let's use functions to simplify the driver control program we made in the previous lesson.

``` c



```

By using functions, we eliminate the need to write motor[ ... ] every time we want to power a motor, making it really easy to power multiple motors at once.
