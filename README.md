# MyHTML — a pure C HTML parser

[![Build Status](https://travis-ci.org/lexborisov/myhtml.svg?branch=master)](https://travis-ci.org/lexborisov/myhtml)
[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=L59E49K2NVUHE)

MyHTML is a fast HTML Parser using Threads implemented as a pure C99 library with no outside dependencies.

* Mailing List: [https://groups.google.com/forum/#!forum/modest-engine](https://groups.google.com/forum/#!forum/modest-engine)
* IRC: [#modest-engine on `irc.freenode.net <http://freenode.net>`](http://webchat.freenode.net?channels=%23modest-engine)
* Or you can ask questions on [stackoverflow.com](https://stackoverflow.com/questions/ask?tags=myhtml) by myhtml tag

This is one of module of the [Modest] project.

## Now

The current version is 3.0.2. [Last stable version](https://github.com/lexborisov/myhtml/releases/latest) is 3.0.1

See [Releases](https://github.com/lexborisov/myhtml/releases)

## Features

- Asynchronous Parsing, Build Tree and Indexation
- Fully conformant with the [HTML5 specification]
- Two API - [high] and [low]-level
- Manipulation of elements: add, change, delete and other
- Manipulation of elements attributes: add, change, delete and other
- Support 39 character encoding by specification [encoding.spec.whatwg.org]
- Support detecting character encodings
- Support Single Mode parsing
- Support Build without POSIX Threads
- Support for fragment parsing
- Support for [parsing by chunks]
- No outside dependencies
- C99 support
- Passes all tree construction tests from [html5lib-tests]
- Tested by 1 billion HTML pages (by [commoncrawl.org], see [test file])

## Changes
Please, see [CHANGELOG.md] file

## Further developments

- [Modest] — Modest is a fast HTML Render implemented as a pure C99 library with no outside dependencies
- [MyCSS] — Fast C/C++ CSS Parser (Cascading Style Sheets Parser) 

## Support encodings for InputStream

```text
X_USER_DEFINED, UTF_8, UTF_16LE, UTF_16BE, BIG5, EUC_KR, GB18030,
IBM866, ISO_8859_10, ISO_8859_13, ISO_8859_14, ISO_8859_15, ISO_8859_16, ISO_8859_2, ISO_8859_3,
ISO_8859_4, ISO_8859_5, ISO_8859_6, ISO_8859_7, ISO_8859_8, KOI8_R, KOI8_U, MACINTOSH,
WINDOWS_1250, WINDOWS_1251, WINDOWS_1252, WINDOWS_1253, WINDOWS_1254, WINDOWS_1255, WINDOWS_1256,
WINDOWS_1257, WINDOWS_1258, WINDOWS_874, X_MAC_CYRILLIC, ISO_2022_JP, GBK, SHIFT_JIS, EUC_JP, ISO_8859_8_I
```

## Support encodings for output

**Program working in UTF-8 and returns all in UTF-8**

## Detecting character encodings

Now it UTF-8, UTF-16LE, UTF16BE and russian windows-1251,  koi8-r, iso-8859-5, x-mac-cyrillic, ibm866

## Introduction

[Introduction]

## Benchmark

- [Article with charts]
- [Benchmark code]
- [Images and CSV]

## Dependencies

None

## Installation

See [INSTALL.md](https://github.com/lexborisov/myhtml/blob/master/INSTALL.md)

## External Bindings and Wrappers

- [Perl 5] module
- [Perl 6] module
- [Crystal] binding

## Examples

See [examples] directory

**Simple example**

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include <myhtml/api.h>

int main(int argc, const char * argv[])
{
    char html[] = "<div><span>HTML</span></div>";
    
    // basic init
    myhtml_t* myhtml = myhtml_create();
    myhtml_init(myhtml, MyHTML_OPTIONS_DEFAULT, 1, 0);
    
    // first tree init 
    myhtml_tree_t* tree = myhtml_tree_create();
    myhtml_tree_init(tree, myhtml);
    
    // parse html
    myhtml_parse(tree, MyHTML_ENCODING_UTF_8, html, strlen(html));
    
    // release resources
    myhtml_tree_destroy(tree);
    myhtml_destroy(myhtml);
    
    return 0;
}
```

## AUTHOR

Alexander Borisov <lex.borisov@gmail.com>

## COPYRIGHT AND LICENSE

Copyright (C) 2015-2016 Alexander Borisov

This library is free software; you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation; either version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this library; if not, write to the Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301 USA

See the [LICENSE] file.


[HTML5 specification]: https://html.spec.whatwg.org/multipage/
[Modest]: https://github.com/lexborisov/Modest
[high]: https://github.com/lexborisov/myhtml/blob/master/include/myhtml/api.h
[low]: https://github.com/lexborisov/myhtml/tree/master/include/myhtml
[examples]: https://github.com/lexborisov/myhtml/tree/master/examples
[parsing by chunks]: https://github.com/lexborisov/myhtml/blob/master/examples/chunks_high_level.c
[encoding.spec.whatwg.org]: https://encoding.spec.whatwg.org/
[html5lib-tests]: https://github.com/html5lib/html5lib-tests
[commoncrawl.org]: http://commoncrawl.org/
[test file]: https://github.com/lexborisov/myhtml/blob/master/test/commoncrawl.c
[MyCSS]: https://github.com/lexborisov/mycss
[CHANGELOG.md]: https://github.com/lexborisov/myhtml/blob/master/CHANGELOG.md
[Perl 5]: https://metacpan.org/release/HTML-MyHTML
[Perl 6]: https://github.com/MadcapJake/p6-MyHTML
[Crystal]: https://github.com/kostya/myhtml
[Introduction]: http://lexborisov.github.io/myhtml/
[Article with charts]: http://lexborisov.github.io/benchmark-html-persers/
[Benchmark code]: https://github.com/lexborisov/benchmark-html-persers/tree/master
[Images and CSV]: https://github.com/lexborisov/benchmark-html-persers/tree/master/Results
[LICENSE]: https://github.com/lexborisov/myhtml/blob/master/LICENSE
