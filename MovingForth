[http://zetetics.com/bj/papers/ Moving Forth: a series on writing Forth kernels] by Brad Rodriguez has good tips for ForthImplementation.



== tiny little nit-picks ==

In
"MOVING FORTH: Part 3: Demystifying DOES>",
Rodriguez points out a little gotcha
that occurs when trying to implement ENTER and EXECUTE in a JMP-threaded DTC Forth.

 ; subtly incorrect code:

 DTC-NEXT:
    JMP [,Y++] ; (IP)->temp, IP++, temp->PC


    JMP ENTER ; in the Code Field of a colon definition
    ...
 ENTER:
    PSHS IP ; save the old IP
    LDX -2, IP ; re-fetch the Code Field address
    LEAY 3,X ; add 3 and put it into the IP (Y) register
    NEXT

 EXECUTE:
    TFR TOS,W ; put address of word in W
    PULU TOS ; pop new TOS
    JMP ,W ;

Rodriguez points out that this does the Wrong Thing when we push the address of a high-level colon definition on the stack, and do EXECUTE.

To solve this problem, Rodriguez claims that NEXT /must/ leave the Parameter Field Address (PFA) of the word-being-executed /somewhere/.

Either
* change NEXT to leave W containing the PFA (Or some "nearby" address -- perhaps PFA-2 or PFA-1 -- as long as it's consistent). Or
* change the JMP in the Code Field Contents to CALL, leaving the PFA on the hardware stack.
And then
* Change ENTER to use this stored PFA.

That's certainly one way to fix things.
But what if we left the JMP, NEXT, and ENTER alone, and modified EXECUTE something like this:

 EXECUTE:
    PSHS IP ; save the old IP
    STD [fake_parameter_field] ; store TOS (D) into the fake parameter field
    LDY #fake_parameter_field ; point the IP (Y) register at the fake parameter field.
    PULU TOS ; pop new TOS
    NEXT

 fake_parameter_field:
    DW 0x0000 ; will be replaced by the actual address we want to execute
    DW EXIT

This seems to me to be a good tradeoff -- it makes EXECUTE much slower, in return for making the heavily-used ENTER a little faster.

Or is there some /other/ gotcha that this will trip over?
