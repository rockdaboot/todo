# todo
What to do next, ideas, facts, fun

wget2
=====

- take test suite from mget project (in work)
- fix the license text in each file
- maybe split tim/wget2 into libwget and wget2 as separate projects ? [1]
- docs - use gtk-docs or what ?
- document the libwget API
- add an FTP/S API into libwget
- add FTP/S support into wget2
- write test cases for FTP/S
- add HTTP/2 support
- write test cases for HTTP/2
- add WARC API into libwget
- add WARC support into wget2
- write test cases for WARC
- ********* add support for libwget to famous tools like e.g. mpg123/mpg321 *******
- Any possibility to grab code verbatim from wget 1.x to libwget (both are GPL)?
  - Interesting code branches:
    - Progress bar.
    - WARC
  - Potential improvements:
    - We avoid having to rewrite complex logic (eg. progress bar).
    - Taking code from wget 1.x doesn't mean we have to maintain current API. We can arrange the code into internal functions and call them from the public-facing API functions, adapting these as we want.
    - We take code out of current wget's hacky codebase and put it into easy-to-use, reusable public libraries.

[1] I guess this depends on how we're planning to release wget2. Because AFAIK wget2 will eventually be merged on top of current wget, right? So, will libwget be on the same codebase as wget (eg. in a directory called 'libwget'), or will it be a separate project (eg. gnu.org/software/libwget) wget will link against? I'd rather go for the first option because that's the approach many projects take. We can then ship two separate packages every time we make a release: one for wget and the other one for libwget alone. Thus, for me the current layout at tim/wget2 is OK.

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
