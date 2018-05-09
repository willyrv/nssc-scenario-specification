# Specifications for describing a scenario under the NSSC framework

A scenario is described in plain text. The scenario will be composed by one or more blocks indicating the parameters of the model in each time period backwards in time and starting from the present (time zero). Each block contains three parameters: **Time**, **Deme sizes** and **Migration matrix** in that order. The value corresponding to **Time** in the first block will be always zero. For example, a valid description of a scenario could be:

```
-Beginning of file-
# Time
0

# Deme sizes
1 1 1

# Migration matrix
0 1 1
1 0 1
1 1 0

# Time
2.5

# Deme sizes
1 1 3

# Migration matrix
0 2.42 1
2 0 1
1 4 0

-End of file-
```

  

Each block begins with a line containing

  

```
# Time
```

followed by a line with a floating point value. Then there is a white line followed by the line:

```
# Deme sizes
```

The next line is a vector of floats, each separated by a single space. The next line is:

```
# Migration matrix
```

followed by some lines of vectors of floats.

The block ends with a white line.
 

# Grammar:
Following is the grammar description for a scenario file in Backus-Naur form. The initial production is ```<scenario>```. Terminals are enclosed in double quotation marks ```"like this"``` in the case of printable characters, or by directly specifying the Unicode codes in simple quotation marks ```'like this'``` otherwise. Optional productions are enclosed in square brackets ```[<like-this>]```. 

```bash
          <scenario> ::= <scenario-component> 
                       | <scenario>

<scenario-component> ::= "# Time" <LB> <float> <LB> <LB>
                         "# Sizes" <LB> <vector-literal> <LB> <LB>
                         "# Migration Matrix" <LB> <matrix-literal> <LB> <LB>

    <matrix-literal> ::= <vector-literal> 
                       | <vector-literal> <LB> <matrix-literal>

    <vector-literal> ::= <float> 
                       | <float> " " <vector-literal>

    <matrix-literal> ::= <vector-literal> 
                       | <vector-literal> <LB> <matrix-literal>

             <float> ::= <integer> [<fraction-part>] [<exponent-part>]

     <fraction-part> ::= "." <integer>

     <exponent-part> ::= "e" [<sign>] <integer>

           <integer> ::= <digit> 
                       | <digit> <integer>

              <sign> ::= "+" | "-"

             <digit> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" 

                <LB> ::= 'U+000A' | 'U+000D' 'U+000A'
```
