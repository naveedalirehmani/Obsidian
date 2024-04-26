## Compilers
Most of the programming languages are either compiled or interpreted. But what does this mean and what is the difference between a compiler and an interpreter? Before you understand this you need to understand some of the operations that a compiler and interpreter execute.  

Let’s say in case of a file being compiled a compiler will compile this file in multiple steps these steps are as follow

#### 1. Lexical analysis.
In this process the compiler tries to understand the syntax of our code. It tries to break down our code in to groups by identifying the keywords that we use in a programming language in case of javascript this can be const name = “Karim”.  

#### 2. Parsing  
in this step the parser will parse the out from the lexical analysis and try to create a AST (abstract syntax tree). An AST is basically our code but in a different format. Think of this as converting our code into a structure that the compiler can understand and compile. this is very common in general programming as well lets say when we create a function we expect the input to be in a specific structure because the algorithm we wrote fro this functions was written keeping in mind a input in a specific structure. So parsing is same just converting our code in a structure that the compiler expects to be and can execute.  
  
#### 3. Code optimisation  
before compiler moves onto converting our source code into object code it also does code optimisation that is it tries to understand our code and tries to skip what is not necessary. compiler understands this and does not actually runs the loop 100 times excepts outputs the function output 1— times. And here it also utilises code cache such as the compiler does not even has to execute the function 100 times it just remembers the output after the first run and just returns the out in subsequent calls.  

## Interpreters  
interpreters also go through all of these steps except code optimisation, why so? Because interpreters execute code at runtime that means that the interpreter unlike the compiler will not go through all these steps one by one and then execute the source code rather it will try to do all this together this means that it understands the code and performs lexical analysis and parsing line by line and also keeps executing it line by line. Since it is not doing all this before hand it cannot perform certain steps like code optimisation.