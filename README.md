# WonderSwan TimingTest V0.2.0

This is a program to test the timing of the CPU in a Bandai WonderSwan.
These results are not an absolute definition of how long an opcode takes, the cpu has an instruction pipeline which is flushed when branching, it takes 1 extra clock when branching to an odd address, it also seems to take more cycles depending on what the destination instruction is. I have tried to make the tests of jump/branch/call avoid these situations but I'm not sure I did it correctly everywhere.
The test loop also takes 1 more cycle than it should, I'm not sure why this is yet, in my emulator I check for 3 nops and add 1 extra cycle, this is not correct but is a way to test all opcode timings.
You can also not compare the result value between opcodes, the result value is for the whole test loop, not the individual opcode. Some opcodes require more glue code than other, please check the source code to see what is happening.
The program test _all_ opcodes, even the undefined ones, on the WonderSwan these are almost allways one byte nops, including 0x0F.
Pop SP (0x5C) doesn't add 2 to the poped value from the stack as some documentation says.
Halt (0xF4) uses serial buffer empty interrupt, I also enable VBlank so that it can continue if serial interrupts are not suported.
All opcode names are in Intel notation and not in NEC notation.

## How to use:
	Use X4 (Left) & X2 (Right) to switch between pages.
	The result values are number of scanlines to run the test loop for each test, the tests are run 1000 times right now which means that the number of clock cycles x 4 almost should be the test result. Some result values can differ by 1 during certain circumstances this is not an error but happens on HW as well.
	I have run the test on my Pink WonderSwan Color to get the results.

## Credits:
	First version by Robert Peip. https://github.com/RobertPeip
	Additions and corrections by Fredrik Ahlström.

	Thanks to:
	Ed Mandy (Flavor) for WonderSwan info & flashcart. https://www.flashmasta.com
	Koyote for WonderSwan info.
	Alex Marshall (trap15) for WonderSwan info. http://daifukkat.su/docs/wsman/
	Guy Perfect for WonderSwan info http://perfectkiosk.net/stsws.html
	asie for info and inspiration.
	Godzil for boot rom stubs. https://github.com/Godzil/NewOswan
	lidnariq for RTC info.

Twitter @TheRealFluBBa

https://www.github.com/FluBBaOfWard
