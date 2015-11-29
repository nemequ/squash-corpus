# Squash Compression Corpus

While I was working on the [Squash
Benchmark](https://quixdb.github.io/squash-benchmark/) I noticed
that the existing corpora for data compression are, in my
opinion, not an accurate representation of the types of things
people typically use compression for.

This project is an effort to compile a new corpus which is
targeted at modern mainstream use cases.  If you have a use case,
or would like to suggest data for one, please use [the issue
tracker](https://github.com/nemequ/squash-corpus/issues) to let
us know.

## Goals

### Designed for modern uses

Most people probably don't have many large plain text
files (things like books) that you need to compress.  On the
other hand, they probably do have things like office
documents (ODF/OOXML), PDFs, log files, data from games, JSON
data, etc.

Rather that just selecting data which is easy to get (and legally
redistribute), we should decide *what* to include then find an
appropriate source.

### Designed for the 99%

There are several groups who have massive data sets and are major
users of compression software.  For example, DNA, geological
data, medical images, etc.  These users can and should create
their own tests with their
data ([Squash](https://quixdb.github.io/squash/) even makes this
easy!)—this corpus is not for them.  [I'm willing to **help**
create something for
them](http://encode.ru/threads/2158-Compiling-a-new-corpus?p=43159&viewfull=1#post43159),
but this corpus is for the 99%.

Note that this doesn't mean it is targeted at the things most
people think they use compression for (e.g., zipping up a few
files so they are easier to e-mail).  Compression often occurs on
the user's behalf without them even being aware—for example, log
files on their computer, RPC messages, data files for games, etc.

### Reasonable overall size

It's easy to get carried away and try to include multiple
versions of lots of different types of data, and while that can
be great for people writing compression codecs, it can be a bit
overwhelming for people writing benchmarks as and the people
trying to interpret the results.  This corpus should contain no
more than 25 (preferably 15-20) pieces of data.

### Appropriate file sizes

Some pieces of data, such as database backups, can be quite large
but others, such as JSON used for RPC or PubSub, are small.  Data
should be as accurate to real-world uses as we can make it,
including how much of it there is.

### Community involvement

We should involve people from various communities early in the
process to make sure our data is relevant to their needs.
Examples include (but are not limited to):

* Mobile developers
* Game developers
* System administrators

### Non-goal: overall corpus design

Some people want to be able to create a tarball of the whole
corpus and compress that, then present a single number for the
result as representative of the entire dataset.  I don't believe
this is feasible, and it is in conflict with other goals.  This
corpus will not be designed to be used like that, and you should
view any attempts to do so with a great deal of skepticism.

## Data (WIP)

Data selection is currently in progress, everything here is subject to
change.

### jquery-2.1.4.min.js

Version 2.1.4 of jQuery, which is probably the most popular JavaScript
library.  This is minified, and should be pretty close to what most
JavaScript used on the web looks like these days.

#### Legal Status

jQuery is licensed under the MIT license; redistribution is not an
issue.

### vmlinux-4.2.6-300.fc23.x86_64

This is a kernel image based on the vmlinuz-4.2.6-300.fc23.x86_64
which I happen to be running right now.  I simply used the
`extract-vmlinux` script to extract the uncompressed kernel.

This should be a decent example of machine code.

#### Legal Status

This is a Linux kernel, licensed under the GPLv2.  Redistribition is
not an issue.

### raspbian-jessie-lite-20151121.tar

I started with Raspbian Jessie Lite (2015-11-21), and mounted the root
partition, deleted /var/cache/apt/archives/*.deb (Debian packages are
comperssed archives).  Then I created a tarball of the remaining files.

#### Legal Status

Raspbian is based on Debian, and contains components under many
different licenses, but it is freely redistributable.

### random

8 MiB of random data collected from /dev/urandom with a Linux 4.2.6
kernel on x86_64 (the same one from vmlinux-4.2.6-300.fc23.x86_64).

#### Legal Status

It's just the output from a PRNG, shouldn't be a problem
