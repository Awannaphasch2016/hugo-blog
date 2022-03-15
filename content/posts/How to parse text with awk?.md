+++
title = "How to parse text with awk?"
author = ["Anak Wannaphaschaiyong"]
tags = ["awk", "blog"]
draft = false
+++

-   ref
    -   <https://stackoverflow.com/questions/6284560/how-to-split-a-variable-by-a-special-character/6284596>


## Awk Syntax {#awk-syntax}

```sh
awk '(PATTERN1){...print something..} (PATTERN2){..print something..}'
awk 'PATTERN1{...print something..} PATTERN2{..print something..}'
```

for each line, if PATTERNN is matched, command in {} will be executed.


### syntax {#syntax}

\`awk 'NR==1{print}' [FILE]\`
\`awk 'NR==1' [FILE]\`
note
    for line 1, print whole line
\`awk 'NR==1{}' [FILE]\`
note
    for line 1, {} = don't do anything
\`awk 'NR==1{print} {print}' [FILE]\`
note
    {} without condition is the same as condition always set to True.
    for eaech line, each condition will be read 1 time
    so this example line 1 will be printed 2 times while the rest of the line
        will be printed 1 time.
\`awk '($0 ~ _e$_){print $0}' [FILE]\`
\`awk '$0 ~ _e$/{print $0}' [FILE]\`
\`awk '/e$/{print $0}' [FILE]\`
:awk:regex:example:terminology
note
    print line if first value ends with e.
    ~ indicate that if statement of the rigth is matched, condition will be true.
    /\\&lt;\\&gt;_ is regex


## Usecase of how to use awk. {#usecase-of-how-to-use-awk-dot}


### split input text by 'x' {#split-input-text-by-x}

```sh
echo 1920x1080 | awk -F"x" '{print $1, $2}'
```


### split input text from a line {#split-input-text-from-a-line}

```sh
echo '$2 = 1920x1080' | awk -F"x" 'sub(/\$[0-9] += +/, "", $1){print $1, $2}'
```


### writing function in .awk extension file {#writing-function-in-dot-awk-extension-file}


#### example 1 {#example-1}

Goal: rounding number using awk

1.  create 'test.awk'

    ```sh
       func round(n){
           n = n + 0.5
           n = int(n)
           return  n
           }
       /^w/ && $2 9000 (print $1, $2/1024, round($2/1024) "K")
    ```
2.  run

    ```sh
          awk -f test.awk [FILE]`
    ```


#### example 2 {#example-2}

Goal: print number that is less than the current line number (line number start from 1)

expected output:

```nil
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
1 2 3 4 5 6
1 2 3 4 5 6 7
1 2 3 4 5 6 7 8
1 2 3 4 5 6 7 8 9
1 2 3 4 5 6 7 8 9 10
```

Solutions:

1.  create loop.awk

    ```sh
       func printloop(n){
           for(i=1;i<=n;i++){
               printf("%d ", i)
               }
           printf("
       ")
       }

       {printloop($1)}
    ```

2.  run

    ```sh
       seq 10 | awk -f loop.awk
    ```
