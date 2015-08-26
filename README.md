# todo
What to do next, ideas, facts, fun

wget2
=====

- take test suite from mget project (in work)
- fix the license text in each file
- maybe split tim/wget2 into libwget and wget2 as seperate projects ?
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
