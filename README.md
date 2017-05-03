# ads_block
For block ADS **DD-WRT** open
Administration->Commands->Save Startup

*sleep 5; wget http://winhelp2002.mvps.org/hosts.txt -O - -q | grep 0.0.0.0 | sed 's/^\(.*\)#.*$/\1/' > /etc/hosts; killall -HUP dnsmasq*



For block ADS **OPENWRT** 
copy paste your roter ssh code:

cat << 'EOF' > /etc/init.d/ads_block
#!/bin/sh /etc/rc.common
START=99
STOP=99
boot(){
   sleep 10
   start
}
start() {
    echo "starting ADS block"
    wget http://winhelp2002.mvps.org/hosts.txt -O - -q | grep 0.0.0.0 | sed 's/^\(.*\)#.*$/\1/'  > /tmp/hosts_ads
    uci add_list dhcp.@dnsmasq[0].addnhosts='/tmp/hosts_ads'
    uci commit dhcp
    /etc/init.d/dnsmasq restart
    echo "started ADS" 
}
stop() {
    echo "stoping ADS block"
    rm /tmp/hosts_ads
    uci delete dhcp.@dnsmasq[0].addnhosts
    uci commit dhcp
    /etc/init.d/dnsmasq restart
    echo "stoped ADS"
}
EOF
chmod +x /etc/init.d/ads_block
/etc/init.d/ads_block enable
/etc/init.d/ads_block start
