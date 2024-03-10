---
title: "Constants in Java"
subtitle: "public final static String HEADING = \"What about Typesafety?\""
date: 2024-03-05
layout: post
category: applied
tags: [java, longform, oop]
---

Behaviour depending on Constants is not something 'Object Oriented Programming' encourages, rather the opposite.
However, sometimes they are needed. A simple example, wrapping for example a 'C' library or communicating with another device via byte arrays.

### TLV Library
As a word of warning at the beginning, the following example is very constructed as well as simplified. It's meant to showcase what one could do in a brief and condensed manner.
Similar to the dog is an animal type of oop introduction slide.

Let's work as example with a communication protocol.
Lets further assume this protocol makes use of the TLV (tag, length, value) pattern, with 3 simple tags.

A simple solution for such a problem is to simply define the needed constants, maybe even package private and use them internally as needed.
```java
    final static int TAG_MESSAGE = 0;
    final static int TAG_SENDER = 1;
    final static int TAG_RECIPIENT = 2;
```

The library can use the tags as is and wrap them in multiply ways. One such approach could be to have a base class 'Tag' and extend for each different Tag, another possibility could be to make use of for example the builder pattern together with a simple Tag class.

The builder pattern would allow to reduce the amount classes significantly if more Tag types are necessary.

For example, something like this.
```java
    class TLV {
        public final int Tag;
        private final byte[] Data;
        public int getLength(){return Data.length();}
        public byte[] getValue(){return Data;}
        public Tag(int tag, byte[] data){...}
    }

    public class TagBuilder {
        TLV getSender(User sender){return new TLV(TAG_SENDER, sender.getBytes());}
        TLV getRecipient(User recipient){return new TLV(TAG_RECIPIENT, recipient.getBytes());
        ...
    }
```

This wraps the constants in a OOP fashion. Additionally we also provide some form of typesafety, as long as all necessary constant definitions and their usage remain tightly controlled.
The user of our toy-library only interacts with built objects.

### Introducing Enumerations.
However what happens if we need for whatever reason to pass the constants around?
Enumerations are quite useful for wrapping integer constants.
They provide type safety in most languages not only Java, not so in C.

In C they are simply (integer) constants with a nicer interface. See the C Standard 'Enumeration Specifiers', in this early draft [C17](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2346.pdf) its on page 87.

So our Tag Type enum could look something like this:
```java
enum Tag {
    Message,
    Sender,
    Recipient;
}
```

If you want to explicitly define the values and _not trust future maintainers_ to make sure the ordinals of these are equivalent to their intended constant, introducing a field is good practice.
The javadoc hints *very* subtly about **not** using the ordinal. [Java SE 21 Enum](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Enum.html#ordinal())

> It is designed for use by sophisticated enum-based data structures, such as EnumSet and EnumMap.

```java
enum Tag {
    Message(0),
    Sender(1),
    Recipient(2);
    
    public final int CONSTANT;
    public Tag(int constant){
        CONSTANT = constant;
    }
}
```
Requiring Objects of Class Tag provides strong type safety. However, introducing a new field creates the risk or possibility, however you like to look at this, to give the same constant value to different constant representations.

### Increased Complexity
What if you now would like to provide the ability to users of your library to define custom tags? The subclassing approach from earlier probably seems like the better approach in hindsight for you.
Users of the library could simply extend the base class with their own behaviour. This provides the greatest safety, as the public API could require final classes in places where no custom tag should be allowed.

Internally however, alot of new classes that need to be tested, maintained and documented are now necessitated.

#### Having your cake and eating it too! :cake:
Enumerations can't be subclassed in Java. However, they can implement interfaces.

```java
interface ITag{
    public byte getTagValue();
}

enum BasicTag implements ITag {
    Message((byte)  0),
    Sender((byte)   1),
    Recipient((byte)2);
    
    public final byte CONSTANT;
    public BasicTag(byte constant){
        CONSTANT = constant;
    }

    @Override
    public byte getTagValue(){
        return CONSTANT;
    }
}

public void someMethod(ITag tag, ...)
```
Now it is possible to require something that represents a Tag without directly coupling to an implementation while still having the type safety if BasicTag in other places. 
It also allows for neat enum operations such as operating on (sub) sets of your enums.
```java
final byte tag = buffer[index];
BasicTag t = BasicTag.fromValue(tag);
Set<BasicTag> allowedTags = EnumSet.allOf(BasicTag.class);
if(!allowedTags.contains(t)){
    //some error handling
}
...
```

It is of course also possible to extend the enum with additional values.
In case of our TLV library, it might be useful to know how to get the length.
If for example, we use a ByteBuffer we can make use of the get methods and extend our data container with some functionality.

```java
interface ITag{
    public byte getTagValue();
    public int getLengthSizeInByte();
}

enum BasicTag implements ITag {
    Message((byte)  0, 1),
    Sender((byte)   1, 2),
    Recipient((byte)2, 4);
    
    public final byte CONSTANT;
    public final int LengthInBytes;
    public BasicTag(byte constant, int lengthBytes){
        CONSTANT = constant;
        LengthInBytes = lengthBytes;
    }

    @Override
    public byte getTagValue(){
        return CONSTANT;
    }
}

//<snip>

long parseDataLength(ITag tag, ByteBuffer buffer){
        byte[] longBuffer = new byte[Long.BYTES]
        final int offset = Long.BYTES - tag.getLengthSizeInByte();
        //assumes big endian
        buffer.get(longBuffer, offset, tag.getLengthSizeInByte());
        
        long parsedLength = 0;
        for(byte b : longBuffer){
            long bAsLong = ((long)b) & 0xFF;
            parsedLength = (parsedLength << 8) + bAsLong;
        }
        return parsedLength;
    }
}
```

Of course it is possible to achive something similar with inheritance only.
However the enumeration approach provides a few benefits that are not that easily realised without.
- a 'class' of constants is neatly contained in a single file, (enumerations cant be extended)
- the usage of enumerations provides a lot of information inherently
- information about a constant, in our case the byte count of the length field, can be combined with a name
- alot of glue logic regarding the usage comes with the JRE, like getting the name as declared via name() or a list of all 'constants' in a class can be accessed via EnumSet.allOf().

[!WARNING]
This example is very constructed and in actual projects a mixture of multiple techniques and paradigms will give the best results.
