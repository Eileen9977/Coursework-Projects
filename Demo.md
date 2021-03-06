# Calculator-in-Scheme Demo

## Basic Information
-> A calculator that allows arithmetic calculations and functions definitions with if statements and while loops

-> Calculator is in post-fix style

-> spaces-using is sensitive in this program; spaces are used to seperate operands and operators

-> The result of calculation would be stored in a stack; as long as the program is running the data stored in the stack would not be erased 

-> Functions need to be defined before being called; that said, function definition and function call should not be in the same line of input

-> Allows using previous user-defined functions as the definition of a new user-defined function

-> Operands implemented based on the concepts provided by gForth

-> Download all files. Compile and run the "multi-functional-calculator.scm" file to use the calculator . 

## Operands and Instructions 

" + "       add

" - "       subtract  

" * "       multiply

" . "       pop up the last inserted element in the stack and print out the element being printed out

" .s "      print out the stack size and the whole stack

" = "       compare whether the top two elements in the stack are equal

" < "       compare whether the second top element is smaller than the top element in the stack: if true replace these two                             elements with -1, otherwise replace them with 0; example: 2 3 1 1 =   -->   2 3 -1  

" > "       compare whether the second top element is bigger than the top element in the stack: if true replace these two                             elements with -1, otherwise replace them with 0;

" dup "     duplicate the top element in the stack; example: 1 2 3 dup   -->    1 2 3 3 

" nip "     remove the second top element in the stack; example:  1 2 3 4 nip    -->    1 2 3

" drop "    remove the top element in the stack without printing out the element; exmaple : 1 2 3 drop   -->    1 2 

" swap "    swap the top two elements in the stack; example: 1 2 3 4 swap    --->   1 2 4 3 

" tuck "    insert the value of the top element in the stack before the second top element in the stack; example: 1 2 3 4 tuck  --> 1 2 4 3 4

" over "    insert the value of the second top element on the top of the stack; example: 1 2 3 4 over  --> 1 2 3 4 3
                     
                     

## Function Definition

" : "       signal the beginning of function define, followed by function name and function definition; space between the colon and function name is required;

" ; "       signal marking the end of function define, followed right after the definition of the function; once " ; " is read in the program would print out the name of the function defined and the definition of the function

example for define simple functions
: getThree 1 2 + ;           --> when type in    1 2 getThree    we get    1 2 3 



## Function Definition with if statements and while loops

-> attention: if statements and while loops can only be used through function definition; that to say, we can only apply if statement and while loops when they are defined inside of a function

-> both if statements and while loops allow nesting

-> while loop would not break until the condition is evaluted to false;


### if statement
(1) if statement contains three signals:   *condition*  if  *if-true statements*  else  *if-false statements*  endif  

" if "      checks the top element in the stack to determine if the condition is true; if the top element is -1, then the condition is true; if the top element is 0, then the condition is false; after "if" the top element in the stack is removed

" else "    seperates the statement applied when condition is true and the statement applied when condition is false

" endif "   marks the end of if statement

### while loop
(2) while loop contains three signals:    begin  *loop-condition*  while  *loop commands to apply when condition is true*  repeat

" begin "   marks the begin of a while loop, should be followed by the loop condition

" while "   check the condition by checking the top element in the stack; if it is -1 then apply the commands inside of the loop; if it is 0 then quit the loop; after " while " the top element in the stack is dropped

" repeat "  " repeat " jumps back to the top of the loop, which is the "begin" in the loop in this program. "repeat" will forces the program to evaluate the loop condition again and decide whether to enter the loop; if the condition is false the program will apply whatever commands following the "repeat"


## Some Examples

 -> the program output would be in quotations
 
 (1)  Defined a function named example1 that would insert 2, compare 2 with the former top element; if equal then insert 42; if not then         insert 17

      : example1 2 = if 42 else 17 endif ;   
      
       2 3 2 example1    
       "2 3 42" 
 
 (2)  Defined a function named fac that applies the commands 1 begin over 0 > whle over * swap 1 - swap repeat nip, which contains a              while loop;
 
      : fac 1 begin over 0 > while over * swap 1 - swap repeat nip ;    
      
       5 fac 42 120 - +      
       "42"     
 
 (3)  Defined two functions if_call and ifcall; ifcall is defined by if_call; ifcall has nesting if statements
 
      : if_call if 6 else 5 endif ;
      : ifcall 6 0 1 < if 0 1 < if_call 0 1 > if_call * else 2 endif + 6 + . ;

      ifcall
      "42"
      
 (4)  Defined a function named loop1 that applies this loop when being called; defined a function named loopnest with nesting loops
 
     : loop1 5 8 * 2 - 5 begin 1 - dup while swap 1 + dup . swap repeat . ;
     : loopnest 2 3 begin = while loop1 repeat . ;
     
     loop1 
     "42"
       
     loopnest
     "42"
 
 
 
 
 
 
