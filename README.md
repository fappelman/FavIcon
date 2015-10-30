# FavIcon [![License](https://img.shields.io/badge/license-Apache%202.0-lightgrey.svg)](https://raw.githubusercontent.com/bitserf/FavIcon/master/LICENSE) [![Build Status](https://travis-ci.org/bitserf/FavIcon.svg)](https://travis-ci.org/bitserf/FavIcon) 
FavIcon is a tiny Swift library for downloading the favicon representing a website.

Wait, why is a library needed to do this? Surely it's just a simple HTTP GET of
`/favicon.ico`, right? Right?  Well. Go have a read of [this StackOverflow
post](<http://stackoverflow.com/questions/19029342/favicons-best-practices), and
see how you feel afterwards.

## Quick Start
The project ships with a playground in which you can try it out for yourself.
Just be sure to build the `FavIcon-iOS` target before you try to use the
playground, or you will get an import error when it tries to import the FavIcon
framework.

## Features
- Detection of `/favicon.ico` if it exists
- Parsing of the HTML at a URL, and scanning for appropriate `<link>` or
  `<meta>` tags that refer to icons using Apple, Google or Microsoft
  conventions.
- Discovery of and parsing of Web Application manifest JSON files to obtain
  lists of icons.
- Discovery of and parsing of Microsoft browser configuration XML files for
  obtaining lists of icons.

Yup. These are all potential ways of indicating that your website has an icon
that can be used in user interfaces. Good work, fellow programmers. 👍

## Usage Example
Perhaps you have a 16x16 location in your user interface where you want to put
the icon of a website the user is currently visiting?

```swift
try FavIcons.downloadPreferred("https://apple.com", width: 16, height: 16) { result in
    switch result {
    case .Success(let image):
        // On iOS, this is a UIImage, do something with it here.
        break
    case .Failure(let error):
        // Ignore if you please!
        break
}
```

This will detect all of the available icons at the URL, and if it is able to determine their sizes, it will try to find the icon closest in size to your desired size, otherwise it will just take the first one it found.

Of course, if this approach is too opaque for you, you can download them all
using `downloadAll(_:completion:)`.

Or perhaps you’d like to take a stab at downloading them yourself at a later
time, in which case `scan(_:completion:)` will give you information about the
detected icons, which you can feed to `download(_:completion:)` for downloading
at your convenience.

## License
Apache 2.0
