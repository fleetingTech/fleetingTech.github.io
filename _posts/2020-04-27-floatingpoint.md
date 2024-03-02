---
title: "The trouble with the floats"
subtitle: "Why float in a sea of uncertainty if you could decimal?"
date: 2020-04-27
layout: post
category: theory
tags: [long-form, floating-point]
modified_date: 2024-02-28
---
Floating point variables are weird.

- Their representation is not intuitve.
- You need to take special care if you want to compare them.
- Their exactness reduces with every step away from 0.
- Most of the time we use them although, we actually do not need them.

But what is a float?
On most machines, we have IEEE single and double precission floating point operation support, so 32 and 64 bit datums.
However, there are many more bitsizes in the annals of history; Zuse's Z1 for example had 24-bit floats. Many relay based machines had 69 bits for float representation.
Whatever size and exact rounding behaviour defined in a standard, the basic system holds true.
Each float consists of 3 parts:
<center>
    <figure>
    s &middot; b <sup>e</sup> 
    </figure>
    <figcaption>s...significand, b...base, e... exponent</figcaption>
</center>
Depending on the defined format, significand, base and exponent have different lengths.
For example, IEEE single precision uses 1 bit for the sign, 8bit for the exponent and 23bit for the significand.
As the base is always 2 for single and double precision, it does not need to be stored.

This however locks the IEEE single and double precision floating point into a specific exactness.
Only fractions that are base-2 representable, can be stored exact in these data formats.
To compare them with other values one needs to actually compare the float &plusmn; epsilon with another value.
Epsilon is an arbitrary value, that the user can choose, as a good enough treshold.
However, in most cases, using the format specific epsilon, the smallest resolvable value of the format, is most sensible.



Also, as already stated, with each step away from 0, the possible resultion of 'base = 2' floats reduces.
These and other mathematical properties of floats have been shown in much more detail with an <a href="https://www.volkerschatz.com/science/float.html" rel="noopener noreferrer" target="_blank">8-bit example</a> by Volker Schatz.
As well as, why floats, still remain exact if used properly.

However, in my opinion, if one discusses the problems of a solution, one should also discuss possible mitigations, if there are any of course.
I sorted the workarounds known to me by usecase. If you know other usecases, please create an issue, so I can update this list.


### Usecase: Currency and other base-10 Values
If your intended use-case is currency, or in other words, fractions with base 10, eg.: <sup>3</sup>&frasl;<sub>10</sub> = 0.3, as fractions that are not base 2, are not always representable.
If you do not know why floating point variables should not be used for currency, you can try <a href="https://github.com/fleetingTech/floating-point-test/blob/master/main.c" rel="noopener noreferrer" target="_blank">this snippet</a> either on your machine or <a href="https://www.onlinegdb.com/online_c_compiler" rel="noopener noreferrer" target="_blank">this online compiler</a>.

The easiest workaroung is using decimals instead. This solution is however a lot slower, as it relies on software, instead of hardware with traditional single or double floating point arithmetic.
But keep in mind, that in most usecases, this decrease in speed, will not be an issue.



### Developing your own fractional representation
Since most languages dont have decimal support out of the box, one could develop their own system.
Especially, if the target plattform does not have floating point support.
This is even easier if the used language supports operator overloading, this way, the fraction can still be used like any other number.
Keep in mind, that if your design is a straightforward implementation of the fractional system, calculating the least common multiple is a very expensive operation, that will be used frequently.


### Usecase: Scaling a value
If your intended goal, is to scale a value, simply scale your source value up until your desired count of decimal places are before the decimal.
Then apply your scaling factor. This is especially useful, if your source value is in a higher unit (eg. volts) then needed (eg. millivolts).
If the resulting value is not in the correct dimension, one needs to reduce with the value that was used to scale, after applying the factor.

<center>
<figure>
$$\frac{1}{3.14}\cdot x = \frac{\frac{1\cdot 100}{3.14}\cdot x}{100}$$
</figure>
</center>



### Usecase: Mapping a range to another
To map a range to another, a conversion factor is needed.
However, the exactness of this factor is susceptible to rounding errors, even more so, if this factor is just calculated as a float without proper care.
If the the target range is not a integer multiple of the source range, rounding errors will happen.
To avoid this, shift your fraction counter.


```c
int scaling = 4;
int convFactor = ((target_max - target_min) << scaling)
                / (source_max - source_min);
int offset = source - source_min;
int result = target_min + ((convFactor * offset) >> scaling);
```
C style snippet, that maps a range to another. If combined with some prescaling, (for the conversion factor), one can get finetuned results, even if no floating point unit is available.



<center>
<figure>
$$\frac{target_{max} - target_{min}}{source_{max} - source_{min}}\cdot offset =\frac{\frac{(target_{max}-target_{min})\cdot scaling}{source_{max}-source_{min}}\cdot offset}{scaling}$$
<figcaption>The right side of the equation is what the code above does. If we ignore the scaling, we get the left side.</figcaption>
</figure>
</center>