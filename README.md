# floom: a small language for hardware control.

    MAIN
    [i0:LOW]------{SECOND}
    [i1:HIGH]---[i2:LOW]---┬-(LIGHT_UP)
    [i1:LOW]----[i2:HIGH]--┘
    SECOND
    [A]----{MAIN}
    [ai3 < 12]---(LIGHT_DOWN)
    BRIDGET
    [i1:HIGH]---[i2:LOW]---┬-(LIGHT_UP)
    [i1:LOW]----[i2:HIGH]--|
    [i1:HIGH]---[i2:LOW]---|
    [i1:LOW]----[i2:HIGH]--┘
    
    //TESTS
    [A] ai3 > 100
    
    //EFFECTS
    (LIGHT_UP) ao0 = 1000
    (LIGHT_DOWN) ao0 = 500

# Why build floom? 
floom started as a thought experiment. 
Later, it was implemented for a Zach-Like game experience with a PLC theme.
Then we realized it could be a fun language for controlling microcontrollers.
