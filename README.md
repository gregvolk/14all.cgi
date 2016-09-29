# 14all.cgi
Front end for MRTG in RRDtool mode

I am migrating this over from http://my14all.sourceforge.net/. The original author and maintainer is Rainer Bawidamann. Many thanks to him for creating and publshing 14all.cgi all those years ago. 
I have made some modifications to 14all.cgi over the years, the most useful one being the addition of CSV export links below each graph. 

-Greg Volk



The original readme file content, most of which is still relevant appears below...

README for 14all.cgi
====================

14all.cgi is a CGI script to create html pages and graphics for mrtg.
It's not another index.cgi for the mrtg-created html pages! Instead it
creates everything itself.

Features
--------

14all.cgi parses the mrtg config file (often called mrtg.cfg) and uses
most of the information to create
- main index page: one link for every "Directory[...]: adir"
- group index pages: one for every "Directory..." with small versions
  of the daily graphics
- statistic pages: one for every target with daily/weekly/monthly/yearly
  graphics according to "Suppress[...]: ..."

MRTG does not create any graphics/pictures if you set "UseRRDTool: Yes"
(mrtg 2.8) or "logformat: rrdtool" (mrtg 2.9)!

Installation
------------

14all.cgi exists in two different versions: v1.0 for mrtg-2.8 and v1.1 for
mrtg-2.9. v1.0 might work with a mrtg-2.9 config file, v1.1 won't work
with mrtg-2.8 as it needs a library from mrtg-2.9.

Installation is similar for both versions:

1. install rrdtool (install perl-shared with "make site-perl-inst" if possible
2. if you use mrtg version 2.8: convert every .log file to .rrd
   with log2rrd.pl (from rrdtool contrib)
3. with mrtg version 2.8: add the line "UseRRDTool: Yes" to your mrtg.cfg
   with mrtg version 2.9: add the line "logformat: rrdtool" to your mrtg.cfg
4. make 14all.cgi accessible via your web server. change the path to your
   mrtg.cfg file in the line beginning with "$cfgfile = ..."

14all.cgi runs under mod_perl. You might want to use mod_perl as it speeds
up the cgi significantly.

v1.1 of the cgi needs the file "MRTG_lib.pm" from mrtg. If the cgi dies with
the error "Can't locate MRTG_lib.pm in @INC" change the path in line 13 in
the cgi to point to the directory where this file is. If your mrtg in
installed in '/opt/mrtg29' this line should look like

  use lib qw(/opt/mrtg29);


Configuration cache
-------------------

Version 1.0 of 14all.cgi now contains code to generate and use a "cache" of
the config file for faster access. This is especially useful for big config
files. The cgi needs write access to the directory with the config file. IF
you don't want this you can run the cgi manually like this:

    /path/to/14all.cgi cfg=path/to/config/file.cfg

from the command line as a user who can write to the config directory. This
will create the config cache. You have to run this command every time you
change the config file (the cgi does not use the cache if it's older than
the config file).

v1.1 currently does not have this config cache.


Author: bawidama@users.sourceforge.net
Homepage: http://www.wh-hms.uni-ulm.de/~widi/14all/
License: Use freely, but: NO WARRANTY - USE AT YOUR OWN RISK!
