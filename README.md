# ID3.NET for .NET Core

ID3-DotNetCore is an effort to port the [ID3.NET library](https://id3.codeplex.com/) to .NET Core.

ID3.NET is a set of libraries for reading, modifying and writing ID3 and Lyrics3 tags in MP3 audio files.

This version of the core library currently supports .NET Core 1.1 and 2.0.

## Extension Support

The original version of ID3.NET supported multiple extensions, but as of right now, only the ID3.File extension has been ported.

Since the original library was written back in 2002, I assumed the metadata library was heavily out of date, and would need some serious refactoring.

Also, .NET Core's binary serialization support is significantly different from the full framework, so I didn't port the Serialization extension.  When/If I have the time, I'll look at porting the code to use [MessagePack](https://github.com/neuecc/MessagePack-CSharp), but if anyone feels ambitious, I'll accept a pull request.  :-)

## Example
```
var musicFiles = Directory.GetFiles(@"C:\Music", "*.mp3");
foreach (string musicFile in musicFiles)
{
    using (var mp3 = new Mp3File(musicFile))
    {
        Id3Tag tag = mp3.GetTag(Id3TagFamily.FileStartTag);
        Console.WriteLine("Title: {0}", tag.Title.Value);
        Console.WriteLine("Artist: {0}", tag.Artists.Value);
        Console.WriteLine("Album: {0}", tag.Album.Value);
    }
}
```
