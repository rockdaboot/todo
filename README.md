# todo
What to do next, ideas, facts, fun

wget2
=====

The code is now stored in branch 'wget2', with libwget and wget2 together.
HTTP/2 support has just been added.

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

- create a MarkDown document to explain wget2 [pri 1], something we can publish on the mailing list
and/or social networks to attract more people (testers, developers, maintainers).

- support HTTP pipelining, at least for HTTP/2 to get full speed when recursively downloading
- docs - use gtk-docs or what ?
- document the libwget API
- set up a second tool (wget2-ftp) to handle ftp only ? (One tool for one task). Communication between
wget2 and wget2-ftp needed for recursive downloads with included ftp URIs !?
- add an FTP/S API into libwget
- add FTP/S support into wget2
- **** at this point: introduce wget on mailing list
- write test cases for FTP/S
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
- create a 'wget2-debian' git repo for Debian packaging, so we can get it easier into Debian


[1] I guess this depends on how we're planning to release wget2. Because AFAIK wget2 will eventually
    be merged on top of current wget, right? So, will libwget be on the same codebase as wget
   (eg. in a directory called 'libwget'), or will it be a separate project (eg. gnu.org/software/libwget)
   wget will link against? I'd rather go for the first option because that's the approach many projects take.
   We can then ship two separate packages every time we make a release: one for wget and the other one for libwget
   alone. Thus, for me the current layout at tim/wget2 is OK.

[Answer] wget1.x and wget2 will maybe never merge (or the earliest in a few years). They can both exist in parallel.
         Once wget2 is stable, we could rename it to wget and rename wget to wget1.x.<br>

GnuTLS
======

- OpenSSL avoids certificate preloading by using hashes (utility c_rehash, have a look at /etc/ssl/certs).
  That allows a very fast startup. I would like to see something similar for GnuTLS. 
  Example for https://www.google.de
```
$ openssl x509 -subject_hash -fingerprint -noout -in /etc/ssl/certs/Equifax_Secure_CA.pem
578d5c04
SHA1 Fingerprint=D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A
$ ls -la /etc/ssl/certs/578d5c04*
lrwxrwxrwx 1 root root 21 Mai 29 21:12 /etc/ssl/certs/578d5c04.0 -> Equifax_Secure_CA.pem
```
  GnuTLS' certtool has no option to generate subject hashes.
  Use 'certtool -i --infile /etc/ssl/certs/Equifax_Secure_CA.pem' to print cert infos

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

curl
====

- When linked with GnuTLS, curl loads each certificate 4 times ! at startup (e.g .on Debian).
  We had the same issue a while ago with Wget - and I fixed it. curl needs a similar fix.
