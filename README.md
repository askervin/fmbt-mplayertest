fmbt-mplayertest
================

An example of testing MPlayer's slave mode with fMBT.


Prerequisites
-------------

Install fMBT and MPlayer. Requires pexpect library for Python and
pulseaudio.

$ sudo apt-get install mplayer python-pexpect pulseaudio


Take a look at the model
------------------------

$ fmbt-editor mplayertest.aal smoke.conf


Run tests
---------

$ fmbt smoke-realrun.conf

$ fmbt rigorous-realrun.conf


Generate different tests
------------------------

Test 20 different ways to get from iPause to iContinue or from
iContinue to iPause. Edit rigorous-realrun.conf, replace lines

coverage  = "perm(3)"
pass      = "no_progress(3)"

with

coverage  = "sum(uwalks(from 'iPause' to 'iContinue'),
                 uwalks(from 'iContinue' to 'iPause'))"
pass      = "coverage(20)"

and run

$ fmbt rigorous-realrun.conf
