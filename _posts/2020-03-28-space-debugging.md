---
title: "LED Debugging in Space"
subtitle: "Why documentation is key"
date: 2020-03-28
layout: post
category: misc
tags: [long-form,debugging,Space, documentation]
modified_date: 2024-02-28
---

There are to my knowledge, few languages and frameworks, that provide the documentation detail that Microsoft provides for the <a href="https://docs.microsoft.com/en-us/dotnet/standard/" rel="noopener noreferrer" target="_blank">.Net Standard</a>. and its languages.
However, it is far more important in the hardware domain to have adequate documentation.
An example for such a datasheet is Ambiq Micro's Documentation for the <a href="https://www.ambiqmicro.com/static/mcu/files/Apollo_MCU_Data_Sheet_DS-A1-1p00.pdf" rel="noopener noreferrer" target="_blank">Apollo MCU</a>.


One might think, that good documentation is a given with rising complexities and big company names behind the product.
A more recent counter example is AMD Developer Guidlines for their 17th generation CPU, or lack thereof.
There are several discussions, even on AMD's own community forum: <a href="https://community.amd.com/thread/213584" rel="noopener noreferrer" target="_blank">Need BIOS and Kernel Developer’s Guide Family 17h</a>.
Furthermore, AMD stopped releasing their <a href="https://developer.amd.com/resources/developer-guides-manuals/" rel="noopener noreferrer" target="_blank">Kernel Development Guides</a> after their <a href="https://en.wikipedia.org/wiki/Zen_(microarchitecture)" rel="noopener noreferrer" target="_blank">Zen microarchitecture</a>.


Although vexing, the lack of proper Kernel Guidelines is not the same as bad documentation.
Bad documentation is badly written, or worse, incomplete. NASA appearantly lost one of their research satellites, <a href="https://en.wikipedia.org/wiki/IMAGE_(spacecraft)" rel="noopener noreferrer" target="_blank">IMAGE</a>(Imager for Magnetopause-to-Aurora Global Exploration), to such a bad documentation (page 35 of the report).

<figure>
<img src="https://upload.wikimedia.org/wikipedia/commons/0/07/Image-spacecraft-iso-view.gif" alt="Isometric view of the IMAGE spacecraft"/>
<figcaption>
Isometric view of the IMAGE spacecraft, <a href="https://en.wikipedia.org/wiki/IMAGE_(spacecraft)#/media/File:Image-spacecraft-iso-view.gif" rel="noopener noreferrer" target="_blank">wikpedia</a>
</figcaption>
</figure>

<a href="https://image.gsfc.nasa.gov/publication/document/IMAGE_FRB_Final_Report.pdf" rel="noopener noreferrer" target="_blank">Link to the official inquery report.</a>
The used powersupply for the communication equipment has a high-current protection. The state of this protection however is not availabe in the telemtry of the power supply.
It is theorized, that the protection was tripped due to the ambient radiation flipping a bit. Since a short-circuit would have damaged IMAGE far more, then was observable.

To determine if the satellite could still recive commands, it was tried to shutdown the cooling equipment on one side, and introduce a spin.
This should have resulted in a detectable heat blip. Basically a very expensive LED debug, common in embedded development.

I call on you, if you decide to document something, please be thourogh. Either be one of the people that answer all inqueries with "the code is the documentation" or take the time to write a good documentation.
If there are parts where you think your prose is not good enough, add an example. But never ever leave out important details or let the documentation get out of sync with the thing you document.
Sadly, IMAGE was unrecoverable, altough several attempts were made over the years.
