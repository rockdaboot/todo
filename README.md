# todo
What to do next, ideas, facts, fun

wget2
=====

The code has been taken from [Mget](https://github.com/rockdaboot/mget).<br>
It has been written from scratch, so I can move that code to another licence at will.<br>
The code is C99 + POSIX to keep it modern and clean (no gnulib dependency).<br>
(BTW, I already compiled Mget on Solaris 10 and CygWin - some tests fail yet)

The code is pretty much Coverity clean. Just two low pri warnings about weak
randomness. Hard to fix since all standard random functions seem to suffer from this.

Wget2 is incomplete and in some points not backwards compatible (e.g. IRI file naming),
also code-wise not mergeable with wget1.x. Wget2 cuts some ropes, e.g. not supporting ancient
web server bugs, ancient compilers, ancient operating systems.<br>
Also, multi-threaded file retrieval has some side effects (e.g. order of downloads).<br>
This means, we will have two tools for the next years - wget and wget2. In most use
cases interchangeable, but in some cases incompatible.<br>

Libwget is just a 'all what is needed for wget2' library. But see the 'examples' directory for
some stand-alone tools (e.g. printing URLs from a HTML or CSS file, downloading SHOUTCAST streams while 
printing embedded title strings).

- take test suite from mget project (in work)
- fix the license text in each file
- maybe split tim/wget2 into libwget and wget2 as separate projects ? [1]
- docs - use gtk-docs or what ?
- document the libwget API
- add an FTP/S API into libwget
- add FTP/S support into wget2
- **** at this point: introduce wget on mailing list
- write test cases for FTP/S
- add HTTP/2 support
- write test cases for HTTP/2
- add WARC API into libwget
- add WARC support into wget2
- write test cases for WARC
- ********* add support for libwget to famous tools like e.g. mpg123/mpg321 *******
- Any possibility to grab code verbatim from wget 1.x to libwget (both are GPL)?
  - Interesting code branches:
    - Progress bar. Wget2 already has a rudimentary multi-line progress bar using an API.
    - WARC. I would like to an WARC API (in libwget) that allows for stand-alone WARC tools.
  - Potential improvements:
    - We avoid having to rewrite complex logic (eg. progress bar).
    - Taking code from wget 1.x doesn't mean we have to maintain current API.
      We can arrange the code into internal functions and call them from the
      public-facing API functions, adapting these as we want.
    - We take code out of current wget's hacky codebase and put it into easy-to-use, reusable public libraries.

[1] I guess this depends on how we're planning to release wget2. Because AFAIK wget2 will eventually
    be merged on top of current wget, right? So, will libwget be on the same codebase as wget
   (eg. in a directory called 'libwget'), or will it be a separate project (eg. gnu.org/software/libwget)
   wget will link against? I'd rather go for the first option because that's the approach many projects take.
   We can then ship two separate packages every time we make a release: one for wget and the other one for libwget
   alone. Thus, for me the current layout at tim/wget2 is OK.

[Answer] wget1.x and wget2 will maybe never merge (or the earliest in a few years). They can both exist in parallel.
         Once wget2 is stable, we could rename it to wget and rename wget to wget1.x.<br>
         For the early development phase (now), I'll leave the branch tim/wget2 as it is, eventually taking out
         wget1.x and gnulib later. But libwget/wget2 will stick together.

GnuTLS
======

- add OCSP multi-stapling by simply merging the OCSP answers into one ASN.1 file.
  gnutls-cli has to extended for that, the low-level stuff should be done in 3.4 branch.
- add OCSP multi-stapling to gnutls-serv, so we can test gnutls-cli with gnutls-serv.
- add support for this file in modgnutls of Apache, it should be straight forward.
  the GNUTLS API should be ready for doing that.
- add OCSP multi-stapling to wget2. We can test with modgnutls or gnutls-serv.


libpsl
======

- add support for libpsl to curl and other web clients

VTLS (low priority)
===================

- let's call it libmtls (m for 'meta') - one TLS API wrapper for many TLS libraries
