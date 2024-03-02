---
title: "The Demoscene"
subtitle: "Performance is key"
date: 2020-03-28
layout: post
category: misc
tags: [long-form,procedural,performance, art]
modified_date: 2024-02-28
---

### Introduction
Before we delve deeper into the matter, please watch the following video. 
Not only to set the scene, but also to emphesize the feats the demo scene routinley creates.
<center>
<figure>
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/sWblpsLZ-O8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
    <figcaption>
        A Mind Is Born, for the code, visit the author's site: <a href="https://linusakesson.net/scene/a-mind-is-born/" rel="noopener noreferrer" target="_blank">linusakesson.net</a>.
    </figcaption>
</figure>
</center>

The video you (hopefully) just watched, was a recording of a demo for the Commodore 64.
The size of the executable is 256 bytes. Almost all demos and intros are tiered according to their executable size.

To give you a frame of reference, ye olde 'Hello World' will help us out.


```c
#include stdio.h;
int main(void) {
  puts("hi");
  return;
}
```
An almost standard 'Hello World' in C; puts instead of printf.


If this is then compiled, for example with clang 7 for x86-64 with the '-Oz' flag, you'll get the following result:

```assembly
puts@plt:
 jmp    QWORD PTR [rip+0x200b92]        # 601018 <puts@GLIBC_2.2.5>
 push   0x0
 jmp    400470 <.plt>
main:
 push   rax
 mov    edi,0x400614
 call   400480 <puts@plt>
 xor    eax,eax
 pop    rcx
 ret    
 nop    WORD PTR cs:[rax+rax*1+0x0]
 nop    DWORD PTR [rax]</code>
```
Assembling this will give you about 45 bytes of actual opcode (without image meta data). 
If you'd like to fiddle around with diffrent compilers and optimisations, give <a href="https://godbolt.org/z/KxwUum" rel="noopener noreferrer" target="_blank">godbolt</a> a try.



The above code snippet, enters main, calls puts and returns from main.
We are already at one fifth of the demo's code size. All we have done is write 'Hello World' without actually doing the writing our self.

Keep this in mind if you have a look at all the amazing demos out there.

## How it all started
It all started with showing off: who could crack/remove the digital rights management, the newest game the fastest.
To this end, the binary of the games, were modified to play a short intro sequence, 'cracktro',
before the actual game started. 


As groups competed with one another, their intros became more and more elaborate.
To reduce the size of the executable as well as to show off what they could do, the intros where written as software, to be rendered on the user's machine.
As the hardware was more homogenous in the early 90's and before that, software could be much more optimized for a specific configuration,
compared to today.
Additionally it made the resulting renderings much more comparable.
These cracktros became so elaborate to <b>demo</b>nstrate, that over time they became the focus of attention, creating the demoscene.


If you compare demos and games of the same hardware and era, it is quite astoundig what these small groups 
managed to create.

<center>
<figure>
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/GqPtAsw7h_k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
    <figcaption>
        Showcase of demos and games of their era on a commodore 64. Games are around the 1:32 timestamp.
    </figcaption>
</figure>
</center>


### Procedural Generation
Over time, other subgenres developed, one of them being games.
Probably one of the most known demos in the mainstream, '.kkrieger' by .theprodukkt,  is such a game.

<center>
<figure>
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/2NBG-sKFaB0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
    <figcaption>
        Playthrough of .kkrieger
    </figcaption>
</figure>
</center>

Its use of procedural world generation, as well as graphics, made it possible to store the entire game of about 300mb in 
just 96kb.

The group released its tools used for development and the game itself on <a href="https://github.com/farbrausch/fr_public" rel="noopener noreferrer" target="_blank">their github</a> if you want to have a look yourself.
Two of the members also gave a talk about some of the techniques used, if you prefer to hear it from the horse's mouth:

<center>
<figure>
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/uUfV41HE_Dg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
    <figcaption>
        Talk on the creation of .kkrieger
    </figcaption>
</figure>
</center>


### Analog Peer to Peer Networks
If you are interested in the demoscene from a Hungarian view especially the differences to Western europe in the early days,
I´d recommend watching the documentary 'The Art of Algorithms'.

<center>
<figure>
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/5MexnBunH_g" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
    <figcaption>
        'The Art of Algorithms' Documentary on the Demoscene in the 80's and 90's.
    </figcaption>
</figure>
</center>

This documentary establishes a timeline of the early demo scene utill the early 2010s.
They do this with a non-technical target audience in mind,
resulting in several glossed over aspacts that propably need their own documentary.

For example, they briefly touch on how they kept up to date on current events and the newest demos without access to an internet connection.
They mailed floppy disks to each other, but not as in the creator sends it to all intrested parties.
There where networks in place, that copied the contents and sent them to their group of 	
acquaintances and those to theirs and so on. 
To keep up to date who is responsible for wich 'subnet' alone must have been a part time job.

Demos were not the only thing passed on with those envelopes of floppies.
Some also contained magazines, not as in the digital magazines we know today,
but programs that executed the demos on the floppy, as well as containing leaderboards and being a demo in and of themselvs, playing music and so on.
Keeping the leaderboards and news up to date with all the networking infrastructure briefly outlined above, must have been no small feat.

### Revision 2020

I'd like to end this entry, with an appeal.
Have a look at Revision. It's a multiday compo (the 'scene' expression for competition) in Germany every year around April.
Virtual Attendence is free, so have a lookout for this years livestream, or recordings of previous years.
The work that gets done there is truly amazing.



Most readers will read this post after Revision 2020 took place,
however their <a href="https://revision-party.net" rel="noopener noreferrer" target="_blank">url</a> should default to the current year's edition.

### DIY
If I have peaked your interest, you can of course, try to do it yourself without additional assistance/team members,
or try the framework of .kkrieger.


However there is a much simpler way to try it out yourself, although it is more restrictive.
An itegral part of demo work, is shading. 
At Revision, there is a live coding competition in shading aptly named Shader Showdown.
The software, <a href="https://github.com/Gargaj/Bonzomatic" rel="noopener noreferrer" target="_blank">Bonzomatic</a>, used for this competition is available for free as well as instruction how to set it up for a competition.

