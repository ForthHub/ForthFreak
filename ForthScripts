working:  JonahThomas

The goal is to make a good bytecode-system generator.

Easy to make bytecode systems.

The code to generate and execute bytecodes should itself be easily portable.

It should be relatively easy to classify bytecode systems and Forth systems to determine what's needed to get a given bytecode system to run on a given Forth system.

There are various Forth bytecode systems already.  Each bytecode system involves a specialized application that includes a tokenizer and a token compiler, and the application gets loaded onto a particular Forth, and gets used as an application. They tend to be one-off.

* WhyByteCode?
* WhyMultipleBytecodes?

* ByteCodeDesignDetails

What's done so far is:

A sample TokenizeR and a matching sample TokenCompiler that should be easy to modify for specialized needs.

A sample DeTokenizer that matches the tokenizer and token compiler.

The start of a decentralised ForthscriptID method.  Scripts could have a short ByteCodeHeader that says what token-compiler is needed to interpret/compile them.  If you have the right token-compiler, and it runs correctly on your system, and the byte-code compiles to something that runs correctly on your system, then you're set -- you can import byte-code and run it.

Building a new TokenizerTokencompilerPair

TheVirtualMachine

Undone:

It would be good to have one byte-code system that was optimised for PortingTokenCompilers.  The current sample conspicuously lacks ' ['] and DOES> . TheDoesIssue needs some choices made.

Ideally, we would get a method to ClassifyForthSystems.  In the ultimate ideal we would have an automated way to estimate which Forth systems any body of code would port to.  The claim isn't that there would be no bugs, but that there should be no bugs introduced by the particular known differences between the system it was designed for and the system it is sent to.  Work on this is just beginning.

There should be some provision to deal with UntrustedByteCode.  

The intention is to provide tools to aid people in getting their own work done.  Add no limitations except those imposed by the difficulties of the medium.
          
----

/I fail to see why a byte-coded Forth is needed for sending over a network. Most Forth source I encounter is already in ascii text format, so it can be sent easily enough. The big challenge - in my view - is embeddeding a Forth environment into a web browser similar to how java/javascript is done. That said, I do see bytecode as a useful tool, especially for a native compiler. It makes it easier to optomize code./ -- CharlesChilders
----
Clearly, you *can* send Forth in text mode.  Bytecode is not necessary.

The advantages I see are (in the order I think of them, not of importance)

*   size.  Bytecode can automatically remove comments and whitespace and surplus names etc, and reduce each call to a byte or two.

*   portability.  You can't do bytecode *without* working out precisely which words you need, and some of the things that tend to be incompatible in text source get smoothed out to be compatible.  

*   small footprint.  A Forth on a minimal system could run only bytecode and not text, and it could interpret/compile bytecode as it came in, a byte at a time, provided the bytes came in the right order.  This one is likely to be a small advantage because once it's on a network the network software will gobble up far more space than you would use or save either one on application software.  And if you don't mind using a tethered system you could send execution tokens etc and muck around with the internals of the system that way -- replace the whole Forth system provided you leave the communications alone along with a very few commands that lay down code at addresses and execute the code at an address.  But it could have some value, and if you have very minimal hardware that mostly sends its data as it collects it, you could wind up with something where a few K of names and such would matter, and yet you still wanted to have a Forth running.

I believe that for most of the existing Forth bytecode applications size is the important thing.  Open Firmware, where bytecode sits in ROM in various peripherals and plug-in devices.  OTA where large numbers of code snippets get sent over the phone lines and get stored in smartcards, by banks.  Etc.  They define precisely how the virtual machine works and all bytecode for that system must be designed for that particular VM.  It's harder to take existing code and tell whether it will run, and maybe that usually isn't worth doing.  

Still, if it becomes *easy* to make Forth bytecode systems, we might find ourselves doing it more often.


I think there could be an important place for a Forth embedded in a web browser, especially if that Forth had some special abilities that make it particularly useful there.  It probably wouldn't be too hard to make a Forth plugin for, say, Netscape.  A bit harder to do it for IE since they've switched to their own separate approach to plugins, but if you do that one it might be more generally useful for recent M$ software.  People would have to download the plugin before they could use it, of course.  A Forth in Javascript would be easier for them to deal with -- with the only problem that you would inherit all of the Javascript problems that you didn't work hard to avoid.  Let's each do what we think is most useful and see where it goes.

"If anybody else thought what you were doing was more fascinating than what they're doing, they'd be doing your stuff instead of their stuff."   JonahThomas
