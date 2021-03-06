# Squash Compression Corpus

While I was working on the
[Squash Benchmark](https://quixdb.github.io/squash-benchmark/) I
noticed that the existing corpora for data compression are, in my
opinion, not an accurate representation of the types of things people
typically use compression for.  This means that codecs are developed
and benchmarked using data which is very different from what we see
used in practice.

This project is an effort to compile a new corpus which is targeted at
modern mainstream use cases.  If you have a use case, or would like to
suggest data for one, please use
[the issue tracker](https://github.com/nemequ/squash-corpus/issues) to
let us know.

## Goals

### Designed for modern uses

Most people probably don't have many large plain text files (things
like books) that they need to compress, but most existing corpora are
rife with them.  On the other hand, they probably do have things like
office documents (ODF/OOXML), PDFs, log files, data from games, JSON
data, etc., which are woefully underrepresented.

Rather that just selecting data which is easy to acquire (and legally
redistribute), we should decide *what* to include then find an
appropriate source.

### Designed for the 99%

There are several groups who have massive data sets and are major
users of compression software.  For example, DNA, geological data,
medical images, etc.  These users can and should create their own
tests with their data ([Squash](https://quixdb.github.io/squash/) even
makes this easy!)—this corpus is not for them.
[I'm willing to **help** create something for them](http://encode.ru/threads/2158-Compiling-a-new-corpus?p=43159&viewfull=1#post43159),
but *this* corpus is for the 99%.

Note that this doesn't mean it is targeted at the things most people
think of when they think of compression (e.g., zipping up a few files
so they are easier to e-mail).  Compression often occurs on the user's
behalf without them even being aware—for example: browsing the web,
log files, RPC messages, data files for games, etc.

### Reasonable overall size

It's easy to get carried away and try to include multiple versions of
lots of different types of data, and while that can be great for
people writing compression codecs, it can be a bit overwhelming for
people writing benchmarks as and the people trying to interpret the
results.  This corpus should contain no more than 25 (preferably
15-20) pieces of data.

That said, it would be reasonable to put together a large corpus from
which to select the final corpus.  This larger corpus could still be
made available to people who would benefit from it (such as those
developing compression codecs).

### Appropriate file sizes

Some pieces of data, such as database backups, can be quite large but
others, such as JSON used for RPC or PubSub, are small.  Data should
be as accurate to real-world uses as we can make it, including how
much of it there is.

### Community involvement

We should involve people from various communities early in the process
to make sure our data is relevant to their needs.  Examples include
(but are not limited to):

* Mobile developers
* Game developers
* System administrators

### Non-goal: overall corpus design

Some people want to be able to create a tarball of the whole corpus
and compress that, then present a single number for the result as
representative of the entire dataset.  I don't believe this is
feasible, and it is in conflict with other goals.  This corpus will
not be designed to be used like that, and you should view any attempts
to do so with a great deal of skepticism.

## Getting Involved

Currently, the
[issue tracker](https://github.com/nemequ/squash-corpus/issues) is the
preferred location for public discussion.  If you prefer, you can also
use the #squash IRC channel on freenode.  If there is demand I can
create a mailing list.

I'm also willing to discuss issues privately
[via e-mail](mailto:evan@nemerson.com), but please keep in mind that
all data for the corpus needs to be public.

## Data (WIP)

Data selection is currently in progress, everything here is subject to
change.

| Name                              | Type                      | Size    |
| --------------------------------- | ------------------------- | ------- |
| jquery-2.1.4.min.js               | JavaScript                | 84 KiB  |
| vmlinux-4.2.6-300.fc23.x86_64     | x86_64 machine code       | 15 MiB  |
| raspbian-jessie-lite-20151121.tar | Mixed; Linux distribution | 723 MiB |
| random                            | Random                    | 8 MiB   |
| girl-brunette.blend               | 3D model                  | 1.7 MiB |
| eff.html                          | HTML                      | 44 KiB  |
| MG44-MathGuide.tar                | Open Document Format      | 11 MiB  |
| bootstrap-3.3.6.min.css           | CSS                       | 120 KiB |
| Total                             |                           | 756 MiB |

### jquery-2.1.4.min.js

Version 2.1.4 of jQuery, which is probably the most popular JavaScript
library.  This is minified, and should be pretty close to what most
JavaScript used on the web looks like these days.

![jquery-2.1.4.min.js](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/jquery-2.1.4.min.js.png)

#### Legal Status

jQuery is licensed under the MIT license; redistribution is not an
issue.

### vmlinux-4.2.6-300.fc23.x86_64

This is a kernel image based on the vmlinuz-4.2.6-300.fc23.x86_64
which I happen to be running right now.  I simply used the
`extract-vmlinux` script to extract the uncompressed kernel.

This should be a decent example of machine code.

![vmlinux-4.2.6-300.fc23.x86_64](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/vmlinux-4.2.6-300.fc23.x86_64.png)

#### Legal Status

This is a Linux kernel, licensed under the GPLv2.  Redistribition is
not an issue.

### raspbian-jessie-lite-20151121.tar

I started with Raspbian Jessie Lite (2015-11-21), and mounted the root
partition, deleted /var/cache/apt/archives/*.deb (Debian packages are
comperssed archives).  Then I created a tarball of the remaining files.

![raspbian-jessie-lite-20151121.tar](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/raspbian-jessie-lite-20151121.tar.png)

#### Legal Status

Raspbian is based on Debian, and contains components under many
different licenses, but it is freely redistributable.

### random

8 MiB of random data collected from /dev/urandom with a Linux 4.2.6
kernel on x86_64 (the same one from vmlinux-4.2.6-300.fc23.x86_64).

![random](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/random.png)

#### Legal Status

It's just the output from a PRNG, shouldn't be a problem

### girl-brunette.blend

[Blender](https://www.blender.org/) 3D model of a young woman,
downloaded from
[Clara.io](https://clara.io/view/500eaba8-395c-46ff-abfd-b7e1b3f5807f).

![girl-brunette.blend](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/girl-brunette.blend.png)

#### Legal Status

©2014-2015 Jason Shoumar.  Licensed under the
[Creative Commons BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license.

### eff.html

The [Electronic Frontier Foundation](https://www.eff.org/)'s index
page, as retrieved on 2015-12-03.

![eff.html](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/eff.html.png)

#### Legal Status

Licensed under the
[Creative Commons BY 3.0 US](https://creativecommons.org/licenses/by/3.0/us/).

### MG44-MathGuide.tar

[LibreOffice Math 4.4 User Guide](https://wiki.documentfoundation.org/images/b/bc/MG44-MathGuide.odt)
in [ODF](https://en.wikipedia.org/wiki/OpenDocument), unzipped then
added to a tarball.

![MG44-MathGuide.tar](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/MG44-MathGuide.tar.png)

#### Legal Status

© 2012–2015, dual-licensed under GPLv3+ / CC-BY 4.0.

### bootstrap-3.3.6.min.css

The CSS from version 3.3.6 of the extremely popular bootstrap project.

![bootstrap-3.3.6.min.css](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/bootstrap-3.3.6.min.css.png)

#### Legal Status

© 2011-2015 Twitter, Inc.,
[MIT](https://github.com/twbs/bootstrap/blob/master/LICENSE)-licensed.

### zlib.wasm

zlib compiled to WebAssembly's binary format.

![zlib.wasm](https://raw.githubusercontent.com/nemequ/squash-corpus/master/fv/zlib.wasm.png)

#### Legal Status

Licensed under the [zlib license](http://www.zlib.net/zlib_license.html).

## Other Corpora

Existing corpora, which this project aims to largerly replace,
includes:

 * [Large Text Compression Benchmark](http://mattmahoney.net/dc/textdata.html) (2006)
 * [Silesa Compression Corpus](http://sun.aei.polsl.pl/~sdeor/index.php?page=silesia) (2003)
 * [Canterbury Corpus](http://corpus.canterbury.ac.nz/descriptions/#cantrbry) (1997)
 * [Calgary Corpus](http://corpus.canterbury.ac.nz/descriptions/#calgary) (1987)
