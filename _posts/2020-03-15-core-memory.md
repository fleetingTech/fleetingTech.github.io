---
title: "The Cores behind the core-dump"
subtitle: "Why we core dump and the beginning of SRAM"
date: 2020-03-15
layout: post
category: fleeting
tags: [long-form,memory,space]
modified_date: 2024-02-28
---

<center>
    <figure>
        <img src="http://ed-thelen.org/comp-hist/navy-core-memory-fig-6-03.gif" alt="core schema" style="width:45%"/>
            This schema was taken from <a href="http://ed-thelen.org/comp-hist/navy-core-memory-desc.html" rel="noopener noreferrer" target="_blank">ed-thelen.org</a>.
            Thelen also gives a more detailed description including the hysteresis of the cores.
    </figure>
</center>


The term dates back to an old type of memory, based on transformer cores.
Saving the complete state of the system, "dumping", the contents of these cores to e.g. a file; hence "core dump".



### Working principle:
The cores are ferite rings (toroids), similar to those used for transformers.
Depending on their usage the rings are magnetisable to enable read and write operations for random access memory (RAM), read only memory (ROM) used the same rings.
Although the technique to do a readout of the two memory systems differ, both systems use a magnetised ring as a binary 1.
Both systems arrange their cores in a lattice, that use for each row and column a wire. 
To activate a core, on both corresponding wires, half the activation voltage is applied,
so the needed magnetic field is generated at the position both wires intersect.

### Usage as RAM:

<center>
    <figure>
        <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/paQ3zIsz1-8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
        <figcaption>EEVblog showcases a memory core module, supposedly from Siemens, with 400 words of storage from the 1970s.
                Also giving an overview of the working principles. The mentioned old video, is the NASA moonlanding documentary linked below.
        </figcaption>
    </figure>
</center>

This type of memory was used as RAM in the period 1955 till the late 70s.
For a small graphical simulator visit the <a href="https://nationalmaglab.org/education/magnet-academy/watch-play/interactive/magnetic-core-memory-tutorial" rel="noopener noreferrer" target="_blank">national mag lab</a>, for another description have a look at the <a href="https://en.wikipedia.org/wiki/Magnetic-core_memory#Description">wiki page</a>,
which sadly has not that many sources. 
Although the contents of the memory are persistent, (non-volatile, static, static random access memory (SRAM)),
the read was destructive. To read, a write signal was applied.
If the core was already set, the output of the read signal will look differently then if the core had state binary 0.
Core memory was more reliable and more radiation hardy compared to the early transistor RAM,
so much so, that the <a href="http://cpushack.com/space-craft-cpu.html" rel="noopener noreferrer" target="_blank">flight computer memory of the space shuttles</a>,
was still implemented in core memory!


There was another system that worked on a similar principle,
<em>BIAX memory</em>
short for <i>biaxial ferrite core</i>.
    <center>
        <figure>
            <img src="https://images.computerhistory.org/revonline/images/x242.83cp-03-01.jpg?w=600" alt="biax cores" style="width:45%"/>
            Taken from <a href="https://www.computerhistory.org/revolution/memory-storage/8/253/984" rel="noopener noreferrer" target="_blank">computerhistory.org</a>
        </figure>
     </center>
Sadly, there is not that much information available.
However there are a few pay-walled articles describing its properties.
<a href="https://www.sciencedirect.com/science/article/abs/pii/0032063361903002" rel="noopener noreferrer" target="_blank"> One is hosted on science direct.</a>
Another one can be found on the <a href="https://dl.acm.org/doi/10.1145/1464052.1464060" rel="noopener noreferrer" target="_blank"> ACM</a>.



Using 2 holes perpendicular to each other, a non-destructive readout is possible,
with lower energy and faster response times, keeping its static property.
According to <a href="https://encyclopedia2.thefreedictionary.com/Biax" rel="noopener noreferrer" target="_blank">The Free Dictionary</a> which cites in turn
the 'Great Soviet Encyclopedia, 3. Edition' - <i>(Vizun, Iu. I. O primenenii elementov tipa “Biaks” ν operativnoi pamiati. Moscow, 1965)</i>, they were cheap to produce in scale.
This however contradicts <a href="https://www.computerhistory.org/revolution/memory-storage/8/253/984" rel="noopener noreferrer" target="_blank">Computer History</a>.
They state that, although superior to the standard toroids in terms of their characteristics, the prohibitive price made them only practical in military applications.



### Usage as ROM:
There are two configurations of the ROM.
They both share the way for encoding 1s and zeroes, passing trough a core was high, not passing through a core meant low.
Both ROMs where word adressable. This means that for each bit, a sense line was active and for each word a read line.

- Active reset - The same way as the RAM. This can be seen in the Apollo documentary below. 
Altough with a much higher data rate per core. As several sense lines are passed through each core. Also, the cores need to be reset after a read.
    <center>
        <figure>
            <img src="https://upload.wikimedia.org/wikipedia/commons/f/fb/Agc_rope.jpg" alt="active reset memory block" style="width:45%"/>
Apollo´s active reset memory, taken from wikipedia.

        </figure>
     </center>

- Passive reset, also named rope memory - Instead of a lattice, the cores are aranged in a line. And the each core has an individual sense line.
This method uses much weaker currents, so the cores reset them selfes after the selection current was shut off. The name comes from the rope assembly of cores and wires.
        <center>
        <figure>
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Apollo_guidiance_computer_ferrit_core_memory.jpg/800px-Apollo_guidiance_computer_ferrit_core_memory.jpg" alt="passive reset memory block" style="width:45%"/>
Rope memory prototype of the apollo memory. (according to <a ref="http://www.righto.com/2019/07/software-woven-into-wire-core-rope-and.html" rel="noopener noreferrer" target="_blank"> Ken Shirriff's blog</a>)
        </figure>
     </center>
    <center>
        <figure>
            <img src="http://www.robotrontechnik.de/bilder/Komponenten/Faedelspeicher_10_k.jpg" alt="passive reset memory block" style="width:45%"/>
            Rope memory of an <a href="https://en.wikipedia.org/wiki/ES_EVM"> ES EVM computer</a>. 
            Picture from <a href="http://www.robotrontechnik.de/index.htm?/html/komponenten/datentraeger.htm" rel="noopener noreferrer" target="_blank"> robotrontechnik.de<a/>
            a german language site dedicated to the history of the GDR's biggest computer company, Robotron.
            The line in green shows how the rope is placed on the pcb.

        </figure>
     </center>


For unknown reasons, NASA moved away from the traditional way and used for the apollo guidance computer the active reset configuration.
You can read about the core memory of an apollo guidance computer and its restoration at 
<a ref="http://www.righto.com/2019/07/software-woven-into-wire-core-rope-and.html" rel="noopener noreferrer" target="_blank"> Ken Shirriff's blog</a>.
Nasa used the passive configuration for prototyping and testing, according to Ken.

<center>
<figure>
    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/ndvmFlg1WmE?start=1245" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen='true'></iframe>
    <figcaption>This documentary of the apollo program shows among other things, the assembly of a ROM core memory,
        also known as <a href="https://en.wikipedia.org/wiki/Core_rope_memory" rel="noopener noreferrer" target="_blank">core rope memory</a>.
    </figcaption>
</figure>
</center>
The east germanan company "Robotron" used for their ROM the traditional passive configuration.
    <center>
        <figure>
            <img src="http://www.robotrontechnik.de/bilder/Komponenten/Faedelspeicher_11_k.jpg" alt="core rope memory schema " style="width:45%"/>
            Core rope memory schema, taken from <a href="http://www.robotrontechnik.de/" rel="noopener noreferrer" target="_blank"> robotrontechnik.de</a>
        </figure>
     </center>

Intrested in tinkering with the concepts yourself? There are several sites that give a step by step guide:
- <a href="https://sites.google.com/site/wayneholder/one-bit-ferrite-core-memory" rel="noopener noreferrer" target="_blank">Wayne's Tinkering Page</a>
- <a href="https://hackaday.io/project/163976-interactive-core-memory-shield-using-led-matrix" rel="noopener noreferrer" target="_blank">Arduino Shield Project</a>



I think it is not proper to end this post without giving the clichéd size comparision:
<center>
    <figure>
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c0/8_bytes_vs._8Gbytes.jpg/1280px-8_bytes_vs._8Gbytes.jpg" alt="comparison" style="width:45%"/>
        <figcaption>Picture taken from <a href="https://www.flickr.com/people/17884028@N00" rel="noopener noreferrer" target="_blank">Daniel Sancho</a>, published as <a href="https://www.flickr.com/photos/17884028@N00/2852716477">cc 2.0</a>. 8 Bytes vs 8 GB.
            However, as you can see in the EEVBlog video, memory cores where in the 70's much smaller already as the shown array.
        </figcaption>
    </figure>
</center>