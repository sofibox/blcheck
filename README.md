This repo was forked from https://github.com/IntellexApps/blcheck and it contains up to the unmerge pulled request from @ogmueller here [#22](https://github.com/IntellexApps/blcheck/pull/22) and @ch604 here [#24](https://github.com/IntellexApps/blcheck/pull/24)

Up to the unmerged pull requests above, in this repo I have made the following improvement and features:

1) :new: It supports the IPv6 addresses checking as well as IPv6 domains.
   ipv6 scan example:

   ```
   # Scan a domain that only return an IPv6
   blcheck ipv6.google.com
   
   # Scan an IPv6 address with any format
   blcheck 2001:0db8:85a3:::8a2e:0370:7334
   blcheck ::1
   
   ```
2) :new: It has a nice scan output and the result is in a json format. Run `blcheck output` to show the scan output 

Sample output:

```
root@MAXIWORK:~# blcheck 107.170.243.13
Warning: list entry '#krn.korumail.com' is not valid and will be ignored
Notice: URIBL entry 'dbl.nordspam.com' will be ignore, because 107.170.243.13 is an IP address
Warning: list entry '#reputation-ip.rbl.scrolloutf1.com' is not valid and will be ignored
Notice: URIBL entry 'dbl.tiopan.com' will be ignore, because 107.170.243.13 is an IP address
Warning: list entry '#niprbl.mailcleaner.net' is not valid and will be ignored
Notice: URIBL entry 'dbl.suomispam.net' will be ignore, because 107.170.243.13 is an IP address
Notice: URIBL entry 'dbl.spamhaus.org' will be ignore, because 107.170.243.13 is an IP address
Warning: list entry '#work.drbl.gremlin.ru' is not valid and will be ignored
all.s5h.net : 127.0.0.2
bl.fmb.la : 127.0.1.27
dnsbl.isx.fr : 127.0.0.2
dnsbl.spfbl.net : 127.0.0.4
dnsbl-3.uceprotect.net : 127.0.0.2
dnsbl.beetjevreemd.nl : 127.0.0.2
dnsbl-2.uceprotect.net : 127.0.0.2
ip.v4bl.org : 127.0.0.2
free.v4bl.org : 127.0.0.2
dnsbl.rymsho.ru : 127.0.0.4
netblockbl.spamgrouper.to : 127.0.0.2

----------------------------------------------------------
Results for 107.170.243.13

Tested:        322
Passed:        310
Whitelisted:   0
Invalid:       1
Blacklisted:   11
Domains:       all.s5h.net,bl.fmb.la,dnsbl.isx.fr,dnsbl.spfbl.net,dnsbl-3.uceprotect.net,dnsbl.beetjevreemd.nl,dnsbl-2.uceprotect.net,ip.v4bl.org,free.v4bl.org,dnsbl.rymsho.ru,netblockbl.spamgrouper.to
Bad score:     3.55 %
----------------------------------------------------------
root@MAXIWORK:~# cat /mnt/c/Users/arafa/IdeaProjects/blcheck/bl_output.txt
{
  "data": [
    {
      "target": "blackhatworld.com",
      "ip": "104.20.155.34",
      "tested_count": 326,
      "passed_count": 323,
      "whitelisted_count": 0,
      "invalid_count": 1,
      "blacklisted_count": 2,
      "blacklisted_domains": "dnsbl.spfbl.net,netblockbl.spamgrouper.to",
      "target_bad_score": "0.62",
      "last_scan_date": 1673454706
    },
    {
      "target": "107.170.243.13",
      "ip": "107.170.243.13",
      "tested_count": 322,
      "passed_count": 310,
      "whitelisted_count": 0,
      "invalid_count": 1,
      "blacklisted_count": 11,
      "blacklisted_domains": "all.s5h.net,bl.fmb.la,dnsbl.isx.fr,dnsbl.spfbl.net,dnsbl-3.uceprotect.net,dnsbl.beetjevreemd.nl,dnsbl-2.uceprotect.net,ip.v4bl.org,free.v4bl.org,dnsbl.rymsho.ru,netblockbl.spamgrouper.to",
      "target_bad_score": "3.55",
      "last_scan_date": 1673454846
    }
  ]
}
```

3) :new: You can specify the scan output location with the option -o (eg: blcheck -o /tmp/output.json 1.2.3.4)

4) :new: It has an extra detail that will tell you about the IP bad score (eg: Bad score: 36.22%), it will show what domains the IP is blacklisted in.

Sample output:

```
root@MAXIWORK:~# blcheck 1.1.1.1
Warning: list entry '#krn.korumail.com' is not valid and will be ignored
Notice: URIBL entry 'dbl.nordspam.com' will be ignore, because 1.1.1.1 is an IP address
Warning: list entry '#reputation-ip.rbl.scrolloutf1.com' is not valid and will be ignored
Notice: URIBL entry 'dbl.tiopan.com' will be ignore, because 1.1.1.1 is an IP address
Warning: list entry '#niprbl.mailcleaner.net' is not valid and will be ignored
Notice: URIBL entry 'dbl.suomispam.net' will be ignore, because 1.1.1.1 is an IP address
Notice: URIBL entry 'dbl.spamhaus.org' will be ignore, because 1.1.1.1 is an IP address
Warning: list entry '#work.drbl.gremlin.ru' is not valid and will be ignored
v6.fullbogons.cymru.com : 127.0.0.2
hostkarma.junkemailfilter.com : 127.0.0.1
nobl.junkemailfilter.com : 127.0.0.1
blackholes.scconsult.com : 127.0.0.2
dunk.dnsbl.tuxad.de : 127.0.0.3
hartkore.dnsbl.tuxad.de : 127.0.0.2
all.spamrats.com : 127.0.0.36
dyna.spamrats.com : 127.0.0.36
list.dnswl.org : 127.0.10.3
dnsbl.justspam.org : 127.0.0.2

----------------------------------------------------------
Results for 1.1.1.1

Tested:        322
Passed:        309
Whitelisted:   1
Invalid:       3
Blacklisted:   9
Domains:       v6.fullbogons.cymru.com,nobl.junkemailfilter.com,hostkarma.junkemailfilter.com,blackholes.scconsult.com,dunk.dnsbl.tuxad.de,hartkore.dnsbl.tuxad.de,all.spamrats.com,dyna.spamrats.com,dnsbl.justspam.org
Bad score:     2.91 %
----------------------------------------------------------
root@MAXIWORK:~# blcheck 128.199.133.81
Warning: PTR lookup failed
Warning: list entry '#krn.korumail.com' is not valid and will be ignored
Notice: URIBL entry 'dbl.nordspam.com' will be ignore, because 128.199.133.81 is an IP address
Warning: list entry '#reputation-ip.rbl.scrolloutf1.com' is not valid and will be ignored
Notice: URIBL entry 'dbl.tiopan.com' will be ignore, because 128.199.133.81 is an IP address
Warning: list entry '#niprbl.mailcleaner.net' is not valid and will be ignored
Notice: URIBL entry 'dbl.suomispam.net' will be ignore, because 128.199.133.81 is an IP address
Notice: URIBL entry 'dbl.spamhaus.org' will be ignore, because 128.199.133.81 is an IP address
Warning: list entry '#work.drbl.gremlin.ru' is not valid and will be ignored
singular.ttk.pte.hu : 127.0.0.3
bl.blocklist.de : 127.0.0.14
bl.fmb.la : 127.0.0.2
all.s5h.net : 127.0.0.2
dnsbl.spfbl.net : 127.0.0.4
dnsbl-2.uceprotect.net : 127.0.0.2
dnsbl-3.uceprotect.net : 127.0.0.2
dwl.dnswl.org : 127.0.0.255
dnsbl.dronebl.org : 127.0.0.13
vote.drbl.gremlin.ru : 127.0.0.2

----------------------------------------------------------
Results for 128.199.133.81

Tested:        322
Passed:        311
Whitelisted:   1
Invalid:       1
Blacklisted:   9
Domains:       singular.ttk.pte.hu,bl.blocklist.de,bl.fmb.la,all.s5h.net,dnsbl.spfbl.net,dnsbl-2.uceprotect.net,dnsbl-3.uceprotect.net,dnsbl.dronebl.org,vote.drbl.gremlin.ru
Bad score:     2.89 %
----------------------------------------------------------

```

5) :new: You can specify the option -j to specify CPU parallel job or threads number (eg: blcheck -j 100% 1.2.3.4 or blcheck -j 2 1.2.3.4). The parallel feature was introduced by @ch604 (it has a known issue on scan percentage jumping randomly)
6) :new: You can specify the -k option to tell the script to use the latest scan result from an IP. So, next time you scan the same IP address, it will be faster as it will use the previous output as cache result instead of scanning it again.
   To cache a new data for the same IP, you can omit the -k option when you scan the same IP address again.
7) :new: You can specify the IP limit to be saved in output file by modifying the variable `MAX_OUTPUT_LINE`. It will delete the oldest scan output if it has reached the specified limit. 
   If you set this variable to 0 or less, you will only have the maximum 1 line in the output file.
8) :new: The code is more readable by following the bashism style guide
9) :new: The option -l <FILE> will accept URL as well that begins with http:// or https:// (eg blcheck -l https://sofibox.com/lists/uribl.txt 1.1.1.1)

10) Fixed bugs:
+ Fixed bug when supplying option -q not showing script result correctly
+ Fixed bug when scan is running, and the user press Ctrl+C, the script will still continue to run and show partial result
+ Fixed bug where sometimes the script did not manage to remove the temporary created files and cause the temp folder to be filled with a lot of files


# Extra package requirement for IPv6 and json support

	installation instruction for some distros:

	apt -y install ipv6calc jq (debian/ubuntu)
	dnf -y install ipv6calc jq (Almalinux/CentOS)

# blcheck

A powerful script for testing a domain or an IP against mailing black lists.
Script will use dig if it is found. If dig is not found script will use host.

Features
--------------------

* More then __100 black lists__ already included!
* Automatic distinction between __domain or IP__
* Performs __PTR validation__ (only if domain is supplied, does not work for IP)
* 3 verbose (-v) levels and a quiet (-q) mode
* The result of script is the number of servers which blacklisted the domain, so it can be used for any kind of __automated scripts or cronjobs__
* Informative and pleasant output


Requirements
--------------------

* Any Unix/Linux with POSIX shell.
* Either dig or host command available.


Usage
--------------------

blcheck [options] <domain\_or\_IP>

Supplied domain must be full qualified domain name.
If the IP is supplied, the PTR check cannot be executed and will be skipped.

-d dnshost  Use host as DNS server to make lookups
-l file     Load blacklists from file, separated by space or new line
-c          Warn if the top level domain of the blacklist has expired
-v          Verbose mode, can be used multiple times (up to -vvv)
-q          Quiet modem with absolutely no output (useful for scripts)
-p          Plain text output (no coloring, no interactive status)
-h          The help you are just reading

Result of the script is the number of blacklisted entries. So if the supplied
IP is not blacklisted on any of the servers the result is 0.


TODO
--------------------
1. Handle domains with multiple DNS entries.

Licence
--------------------
MIT License

Copyright (c) 2018 Intellex

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

Credits
--------------------
Script has been written by the [Intellex](http://intellex.rs/en) team.
Contributors:
	[Darko Poljak](https://github.com/darko-poljak)


