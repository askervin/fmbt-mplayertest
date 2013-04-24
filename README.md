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

$ fmbt smoke.conf

$ fmbt rigorous.conf


Generate different tests
------------------------

Test 20 different ways to get from input "pause" to input "continue",
or from "continue" to "pause". Edit rigorous.conf, replace lines

coverage  = perm(3)
pass      = no_progress(3)

with

coverage  = sum(uinputs(from 'i:pause' to 'i:continue'), uinputs(from 'i:continue' to 'i:pause'))
pass      = coverage(20)

and increasing step limit (pass = steps(...)).

Finally run

$ fmbt rigorous.conf


Simulate test runs
------------------

You can only generate a test instead of generating and running it by
commenting out adapter=aal in the configuration file. ("#" starts a
comment line.) Then run

$ fmbt rigorous.conf | fmbt-log

to see the list of actions that would be tested.
