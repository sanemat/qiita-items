```
$ dpkg -s git |grep Version
Version: 1:2.7.4-0ubuntu1.2
```
コレならCVE-2017-1000117はオッケー

changelogはコレで見える

```
$ apt changelog git
git (1:2.7.4-0ubuntu1.2) xenial-security; urgency=medium

  * SECURITY UPDATE: Arbitrary code execution on clients through
    malicious ssh URLs.
    - debian/patches/CVE-2017-1000117.patch: filter out hostnames that
      would interpreted as cli arguments to ssh
    - debian/diff/0002-transport-expose-git_tcp_connect-and-friends-in-new-t.diff:
      update to adjust for changes from CVE-2017-1000117.patch.
    - CVE-2017-1000117

 -- Steve Beattie <sbeattie@ubuntu.com>  Thu, 10 Aug 2017 14:15:28 -0700
```
