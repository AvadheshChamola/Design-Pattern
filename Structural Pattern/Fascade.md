# Fascade Structural Design Pattern

- Facade is a structural design pattern that provides a simplified interface to a library, a framework, or any other complex set of classes.
- A facade is a class that provides a simple interface to a complex subsystem which contains lots of moving parts. A facade might provide limited functionality in comparison to working with the subsystem directly. However, it includes only those features that clients really care about.

![image](https://github.com/AvadheshChamola/Design-Pattern/assets/43910109/21506efd-d720-4da8-a6bf-69985a194b3d)

# PseudoCode
![image](https://github.com/AvadheshChamola/Design-Pattern/assets/43910109/684db017-a7f6-4545-9942-d75c9707095f)

# Code
```java

// These are some of the classes of a complex 3rd-party video
// conversion framework. We don't control that code, therefore
// can't simplify it.

class VideoFile
// ...

class OggCompressionCodec
// ...

class MPEG4CompressionCodec
// ...

class CodecFactory
// ...

class BitrateReader
// ...

class AudioMixer
// ...


// We create a facade class to hide the framework's complexity
// behind a simple interface. It's a trade-off between
// functionality and simplicity.
class VideoConverter is
    method convert(filename, format):File is
        file = new VideoFile(filename)
        sourceCodec = (new CodecFactory).extract(file)
        if (format == "mp4")
            destinationCodec = new MPEG4CompressionCodec()
        else
            destinationCodec = new OggCompressionCodec()
        buffer = BitrateReader.read(filename, sourceCodec)
        result = BitrateReader.convert(buffer, destinationCodec)
        result = (new AudioMixer()).fix(result)
        return new File(result)

// Application classes don't depend on a billion classes
// provided by the complex framework. Also, if you decide to
// switch frameworks, you only need to rewrite the facade class.
class Application is
    method main() is
        convertor = new VideoConverter()
        mp4 = convertor.convert("funny-cats-video.ogg", "mp4")
        mp4.save()

```

# Pros
- You can isolate your code from the complexity of a subsystem.

# Cons
-  A facade can become a god object coupled to all classes of an app.
God Object - In object-oriented programming, a god object (sometimes also called an omniscient or all-knowing object) is an object that references a large number of distinct types, has too many unrelated or uncategorized methods, or some combination of both. The god object is an example of an anti-pattern and a code smell.
