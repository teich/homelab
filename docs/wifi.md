## Controller config

* Channel selection. Write some words here. It's annoying.
* IOT devices seem to often have terrible issues. Create a IOT device only network. 
    * I don't bother VLAN/isolating, but you do you.
    * I made the IOT SSID 2ghz only. Idea is pollute the 5ghz band less, no idea if it's helpful.
    * Turn off any new features for the IOT SSID. In Unifi Wifi -> WiFi Networks -> Settings -> Advanced Settings I literally have _everything off_ 
* 'Wi-Fi AI' sometimes makes everythig much worse, and there is no way to tell why. It also will sometimes disconnect IOT devices if it's on. My Ecobee for example get angry if this feature is on and require pulling from the wall. I'll leave the WiFi AI feature running for a few days or weeks, pick a setting that looks reasonble and turn it off.
* 'Network Settings -> Optimizations -> Auto-Optimize Network' seems to be a trap. I keep it off. Turning it on has only had negative results for my network so far.
* 'Network Settings -> Advanced -> Advanced Features' I have on. Haven't seen any benefit or negative.
* 'Gateway -> mDNS -> Enable Multicast DNS' is on since I've got devices on different networks.
* My 5GHZ good device network I turn on many fatures including 'Fast Roaming', 'Multicast Enhacement', 'UAPSD', and 2G Data Rate Control (@ 6Mbps)

## Device Config
* I go into each device and disable wireless meshing. Device -> Settings -> Gear Icon (config) -> Allow messhing from other acecss points -> off for both radios.
* I'll go into the WLANS for each device (there must be a better way, someone please tell me!) and turn off my IOT on 5GHZ by clicking the pencil and 'enabled on this AP'.