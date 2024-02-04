# floom: a small hybrid syntax language for state reasoning.

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

# Why build floom? 
floom started as a thought experiment. 
Later, it was implemented for a Zach-Like game experience with a PLC theme.
Then we realized it could be a fun language for controlling microcontrollers.
