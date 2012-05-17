# asterisk-opencnam

The simplest way to add caller ID name information to your Asterisk-based PBX
system.

``asterisk-opencnam`` should work with Asterisk 1.2+.


## Install

To install ``asterisk-opencnam``, log into your Asterisk server(s) and run:

``` bash
$ mkdir -p /var/lib/asterisk/modules
$ cd /var/lib/asterisk/modules/
$ git clone git://github.com/rdegges/asterisk-opencnam.git
```

Then edit your ``/etc/asterisk/extensions.conf`` file, and append:

``` asterisk
#include </var/lib/asterisk/modules/*/src/*.conf>
```

To the bottom of the file. This tells Asterisk to dynamically load the
``asterisk-opencnam`` module each time Asterisk is started.

If you'd like to update ``asterisk-opencnam``, simply run:

``` bash
$ cd /var/lib/asterisk/modules/asterisk-opencnam
$ git pull
```

**NOTE**: These instructions assume you have Asterisk installed to the normal
system path (``/var/lib/asterisk``), and that you also have Git available on
the server(s).


## Usage

Now that you've got ``asterisk-opencnam`` installed, let's activate it! Since
we'll (most likely) want to get each caller's name information as soon as their
call comes in, you'll most likely want to modify your Asterisk system's
``from-pstn`` context to do the lookup.

Below is an example:

``` asterisk
;; /etc/asterisk/extensions.conf

[from-pstn]
exten => _NXXNXXXXXX,1,Gosub(opencnam-set-callerid,${EXTEN})
exten => _NXXNXXXXXX,n,NoOp(This caller's name is: ${CALLERID(name)})
exten => _NXXNXXXXXX,n,Answer()
exten => _NXXNXXXXXX,n,...
```

The code above will take the incoming caller's 10-digit US phone number, and
call the ``opencnam-set-callerid`` subroutine which will update the caller ID
name information for the call.


## Reference

If you've got no idea what I'm talking about, the following links may be
helpful:

- [Asterisk PBX](http://www.asterisk.org/)
- [OpenCNAM](http://www.opencnam.com/)

If you'd like more information on Asterisk, read
[Asterisk: The Definitive Guide](http://www.amazon.com/gp/product/0596517343/ref=as_li_ss_tl?ie=UTF8&tag=rdegges-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0596517343).


## Changelog

- No releases yet!
