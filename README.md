# ads_block
For block ADS DD-WRT open
Administration->Commands->Save Startup

content:  dd-wrt-administration-commands-startup.txt
*sleep 5; wget http://winhelp2002.mvps.org/hosts.txt -O - -q | grep 0.0.0.0 | sed 's/^\(.*\)#.*$/\1/' > /etc/hosts; killall -HUP dnsmasq*

