# Core fonts for the Web web fonts

The Microsoft [Core fonts for the Web](https://en.wikipedia.org/wiki/Core_fonts_for_the_Web) included Andale Mono, Arial, Arial Black, Comic Sans MS, Courier New, Georgia, Impact, Times New Roman, Trebuchet MS, Verdana and Webdings as TrueType fonts. Microsoft no longer distributes the fonts, but they may still be redistributed. However, the [EULA](http://www.microsoft.com/typography/fontpack/eula.htm) specifies that the fonts may not be "included as part of your own product" or modified in any way.

But wouldn't it be fun to use them as `@font-face` web fonts? But sadly the original, redistributable, format is only either .exe or .sit.hqx files...

With sufficient usage of JavaScript, random HTML5 features ([Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) URLs in dynamically generated stylesheet rules) and [emscripten](http://emscripten.org)-compiled [cabextract](http://www.cabextract.org.uk/), anything is possible.

# Why?

Why not?

# Usage

1.  First get the fonts.

    Currently you must download the fonts yourself. If the fonts are available from a public HTTP server supporting CORS, this step could be removed and this project becomes almost useful.

    ```bash
    wget http://prdownloads.sourceforge.net/corefonts/comic32.exe
    ```

    All the fonts may be found online in [various](http://web.nickshanks.com/fonts/microsoft-core-web-fonts) [places](http://sourceforge.net/projects/corefonts/files/the%20fonts/final/).

2.  Serve the directory as HTTP. This is needed for XHR access to the fonts.

    ```bash
    python -m SimpleHTTPServer 8080
    ```

3. Open http://localhost:8080/demo.html

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

TODO: recompile cabextract with optimization.

# License

This project is GPL licensed because it incorporates a compiled copy of [cabextract](http://www.cabextract.org.uk/) which is also GPL licensed.

The fonts are licensed under Microsoft's [EULA](http://www.microsoft.com/typography/fontpack/eula.htm).
