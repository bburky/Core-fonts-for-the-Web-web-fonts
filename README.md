# Core fonts for the Web web fonts

The Microsoft [Core fonts for the Web](https://en.wikipedia.org/wiki/Core_fonts_for_the_Web) included Andale Mono, Arial, Arial Black, Comic Sans MS, Courier New, Georgia, Impact, Times New Roman, Trebuchet MS, Verdana and Webdings as TrueType fonts. Though Microsoft no longer distributes the fonts, they may still be redistributed. The [EULA](http://www.microsoft.com/typography/fontpack/eula.htm) specifies that the fonts may not be "included as part of your own product" or modified in any way.

But wouldn't it be fun to use them as `@font-face` web fonts? But sadly the original, redistributable, format is only either .exe or .sit.hqx files...

With sufficient usage of JavaScript, random HTML5 features ([blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) URLs in dynamically generated stylesheet rules) and [emscripten](http://emscripten.org)-compiled [cabextract](http://www.cabextract.org.uk/), anything is possible.

# Why?

Why not?

# Demo

http://bburky.com/Core-fonts-for-the-Web-web-fonts/demo.html

This downloads `comic32.exe` via XHR using CORS from a [Dropbox public folder](https://dl.dropboxusercontent.com/u/2950460/Core-fonts-for-the-Web/index.html) and then the emscripten-compiled cabextract extracts a TTF font. A CSS rule is inserted to use the font via `@font-face`.

# Compiling cabextract

You must have emscripten installed.

1.  Download cabextract 1.4.

    ```bash
    wget http://www.cabextract.org.uk/cabextract-1.4.tar.gz
    ```

2.  Compile cabextract using emscripten.

    ```bash
    emconfigure ./configure
    emmake make
    emcc cabextract.o md5.o libmspack.a  mktime.o fnmatch.o -o cabextract.js
    ```

TODO: Recompile cabextract with optimization. Use libmspack directly instead of cabextract.

# License

This project is GPL licensed because it incorporates a compiled copy of [cabextract](http://www.cabextract.org.uk/) which is also GPL licensed.

The fonts (not included) are licensed under Microsoft's [EULA](http://www.microsoft.com/typography/fontpack/eula.htm).
