# Progress Report 10/3/2023
[Go back to home page](https://wib-wob.github.io/site/)

heya :) welcome to our second progress report! it sure has been a while since the last one!

We are super excited to share a big update with you, so hang tight!

I also wanna thank all of YOU for supporting us! Our Discord server has been through an "identity crisis" recenetly, but everyone is still so supportive! We love you so much and appreciate your support.

**And without further-a-do, let's get progress-reporting (???)**

## a bit of background
recently, we opened 2 more projects in our Discord server: Yo-Kai Exercise Translation And PTE. PTE is just a LTS version of the discontinued Puni Translation Project, and Yo-Kai Exercise Translation is a translation of the niche mobile game Yo-Kai Taiso. This means that we've been splitting our attention among multiple projects recently, but now we development is back in full swing!
it's also worth mentioning that Woganog and I are people with a life that do other things other than mod stupid children's games, so that's why the progress reports have been taking so long.

## some facts about wibwob's internals
As some of you probably know, WibWob was a cross platform game, meaning it was on both iOS and Android. This meant that the developers couldn't have possibly written the game in either Java or Swift, which are each used on their respective platforms, because writing 2 codebases is just not that realistic. Instead, they opted into writing the game in C++ and compiling it into a shared object. A shared object is a compiled binary that can be used by external code. here is a goofy chart I drew that explains how they wrote the code in C++ and compiled it to android:

![image](https://github.com/wib-wob/site/assets/111663937/ff0155f2-da7b-48e9-9dbe-e8413b28a179)

So basically, they used 1 codebase for everything. Good for them! Not so good for us. Regular compiled Java code is just compiled into bytecode, so it can just be decompiled into Smali, which is a human readable representation of the bytecode Java is compiled into. Here is an example of what a smali function might look like:
```smali
.method public static myFunction()Ljava/lang/String;
    .registers 1

    # This function takes no arguments and returns a string.

    const-string v0, "Hello, world!"
    # Create a string constant in register v0.

    return-object v0
    # Return the string constant in register v0.
.end method
```
Shared Objects, on the other hand, are compiled to machine code. This means that we will have to directly edit the assembly code of the game. Assembly is like Smali, but instead of representing bytecode, it represents machine code (machine code like 01101101 01100101 01101110 00100000 01101000 01101111 01110100). To analyze and edit a compiled binary like WibWob's game code, we need a disassembler. A disassembler is a program that takes in a compiled binary and displays the program's Assmebly code and its symbols (function names and stuff like that). Luckily, WibWob's code has a lot of these symbols, which brings me to the next thing:

## login implementation (kinda ig)

sooo... I found a function called "LoginGuest". When you login as a guest, it means that you are logging into the game's servers without an account, therefore, a guest.  

I also found a function called "OnLoginGuestComplete".

your first thought is probably "man just edit LoginGuest to call OnLoginGuestComplete and see what happens".

well, I can't get the ARM64 assembler to work 😭

I am still trying, and unfortunately I was on time crunch with this progress report, because it was actually due yesterday.

but then I had a very bright idea. a very very bright one.

## restitching the game!1!1!!!

you probably know what stitching means, right? Good. so by "restitching", I mean that instead of reverse enginerring the server, we can just "restitch" the game together through shared object editing. here is what I mean: find which functions control everything and run them based off of our own server that doesn't even remotely resemble the original WibWob server! This will make everything so much easier for us and a lot more enjoyable for you! I will be back with another progress report in a few days when I get that fucking assembler working AAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

-SuperTavor

