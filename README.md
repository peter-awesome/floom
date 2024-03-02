# Floom: a small hybrid syntax language for state reasoning.

contact us for licensing.
```python
    SETUP
    import time
    VAR
    var1 = 0
    MAIN
    (print("hello world")) #this is a standard line of floom
    [var1>=5]{END}
    (var1 = var1 + 1)
    (sleep(5))
    END # this is another label for a loop section - but it is empty - so we exit.
    
    #corresponding Python code
    import time
    var1 = 0
    def main():
    	print("hello world")
    	loop = True
        while loop==True:
        	if var1 >= 5:
        		exit()
        	var1=var1+1
        	sleep(5)
    
    if __name__ == "__main__":
        main()
```

# Why build floom? 
floom started as a thought experiment. 
Later, it was implemented for a Zach-Like game experience with a PLC theme.
Then we realized it could be a fun language for controlling microcontrollers.

# FLOW CONTROL
# LOOP BLOCK:
   ```python
    MAIN
        [ai1 > 100] [o2 = LO] (o2 = HI)
        (wait 200)
        [ai1 < 100] [o2 = HI] (o2 = LO)
```

This Floom Script features a loop block labeled MAIN. It repeatedly checks the status of analog input 1 (ai1). If ai1 exceeds 100, the script sets output 2 (o2) to HIGH; if ai1 falls below 100, it sets o2 to LOW. This maintains the ai1 value near 100 by controlling a valve linked to o2, demonstrating a basic control loop. This is similar to a Main Loop in Arduino code or a While: True==True construction in other languages.


# BOOLEAN GATE:
 ```python   
    x = 4
    [x>2]  (x=2)  #this line will execute - changing the value of x to 2.
    [x<3]  (x=4) # this line will execute - changing the value of x to 4.
```

In Floom, flow control operates through boolean gates, functioning similarly to 'If' statements. Place any boolean expression inside square brackets []. If true, the code following the brackets on the same line executes. For example, initially, x is set to 4. The script then checks if x is greater than 2; if so, x is set to 2. Next, it checks if x is less than 3; if so, x is set to 4. 

Floom evaluates each line left to right and continues to the next line if a boolean gate returns False. This eliminates the need for an 'Else' keyword.

Classical boolean constructs are expressed through flow structure in Floom. The recipes for common boolean expressions follow.


# AND
```python
    [i0==LOW] [i1==HIGH] (doSomething())
```
Logical And is achieved by placing two Boolean Gate expressions in sequence on a single line.
# OR (Branch Gate)
```python
    ┳[i1==HI][i2==LO]┳(LIGHT_UP)
    ┗[i1==LO][i2==HI]┛
```
In this structure, the ┳ symbol starts an OR condition, activating Conditional Expression Evaluation. Floom evaluates each Boolean condition from left to right. If any condition is FALSE, execution moves down one line from the ┳. The script expects a ┗ (Left Branch Terminator) or ┣ (Left Branch Continuator) next. If absent, execution stops due to an error.
If all conditions are TRUE, Floom ends the Conditional Expression Evaluation and continues normal execution. The ┗ and ┣ symbols in normal mode advance execution to the next line.
Commands between a Left Branch Terminator or Continuator are executed until a ┛ (Right Branch Terminator) or ┫ (Right Branch Continuator) is encountered. Execution then continues one line above at the corresponding ┳ position.
# Complex Branch Gate Construction
```python
      [i1==LO]┳[i2==LO]┳(LIGHTS_UP)
              ┗[i3==HI]┫
      [i1==HI]┳[i2==HI]┫
              ┗[i3==LO]┛
```
In complex OR structures, the evaluation mirrors that of a basic OR, but with multiple branching levels. Floom evaluates each set of conditions within branches. Upon reaching ┗ or ┣, it adheres to the branching logic, continuing conditional evaluations according to the script's flow until encountering a ┛ (Right Branch Terminator) or ┫ (Right Branch Continuator), which guide the return to standard execution flow or continuation within the complex structure.

# BLOCK JUMP:
```python
    MAIN
      [i0==LOW]              {SECOND}
```
In this Floom script, the MAIN loop block continuously checks the state of input 0 (i0). If i0 becomes LOW, the script performs a 'Block Jump' to the loop block labeled SECOND. 
A 'Block Jump' in Floom, denoted by a label within curly braces {}, directs code execution to the specified label. If the label is not found, an error occurs, stopping the script.

# Match Syntax (switch case)
```python
    Label
    ━(matchCase)┓
     ┣(condition1) {Jump1}
     ┣(condition2) [BooleanGate2] (action2)
     ┗┳(condition3)┳ (Action3)
       ┗(condition4)┛ 
```

In Floom, we start matching patterns with "━(matchCase)┓". Here, "matchCase" is the starting point or the first thing we check.
Here's how it works:
If "condition1" is the same as "matchCase", then "Jump1" happens.
Next, if "matchCase" fits "condition2", then "BooleanGate2" turns on, leading to "action2".
If "matchCase" is either "condition3" or "condition4", "Action3" happens. This is like saying "if this or that, then do this."
The line "━" means we're starting the matching process. It connects the starting point "matchCase" to other checks "┣" or the end "┗". This way, we clearly see what happens step by step, without needing the usual SWITCH or CASE methods.


