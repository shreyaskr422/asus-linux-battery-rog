# asus_laptop_arch_linux
packages and settings for asus laptops on arch linux


**1. tlp and tlp-rdw** - *for power settings*
As for config for tlp you find in /etc/tlp.conf

START_CHARGE_THRESH_BAT0=75     --*at this point, battery will start charging*

STOP_CHARGE_THRESH_BAT0=80      --*at this point, battery will stop charging*

*Then*
**sudo tlp start**

**sudo systemctl restart tlp**

**sudo tlp-stat -s**

**2. asusctl  & supergfxctl**   *allows ROG & TUF laptop owners to control their laptops from a CLI*

 
 **sudo systemctl enable --now asusd.service**

 **sudo systemctl enable --now supergfxd.service**
 
 **sudo systemctl enable --now asusd.service**

 
 
 **lsmod | grep asus**                        --for checking asus_nb_wmi and asus-wmi is enabled or not
 
 **sudo modprobe asus_nb_wmi**         --if Not then enable it                                         
 
 **sudo modprobe asus_wmi**
 
 
 
 **echo "asus_nb_wmi" | sudo tee -a /etc/modules-load.d/asus.conf**   --recheck it          
 
 **echo "asus_wmi" | sudo tee -a /etc/modules-load.d/asus.conf**



#for setting up the asusctl and supergfxctl 
 
 **asusctl**
 
 **asusctl -k auto**


 
 **supergfxctl**
 
 **supergfxctl -m Hybrid**

 
 
 #For checking the the services are working or not if not then reload daemon 
 
 **lsusb**
 
 **Bus 001 Device 002: ID 0b05:1866 ASUSTek Computer, Inc. N-KEY Device**
 
 **sudo  systemctl daemon-reload && systemctl restart asusd**





NOW COMES THE GOOD PART 

 **asusctl**                   *use this for modes and help*
 
 **asusctl aura static**       *this command is for the aura static settings you have in windows 11 or 10 whatever*




AND FOR SUPERGFXCTL 

**supergfxctl**               *use this command for also modes and options*


common used modes  -->


**supergfxctl -m Integrated**       *only igpu(amd or intel) and not dedicated gpu (nvidia or amd) mostly for battery*

**supergfxctl -m Hybrid**           *both igpu and dedicated gpu it gonna select according to use*


**supergfxctl -m VFIO**             *For bypass for vm mostly used for qmeu and virt-manager for tuning for vm*


**supergfxctl -m Dedicated**        *only dedicated gpu (nvidia or amd) and not igpu (amd or intel)*





*********FOR GUI CONTROL FROM ASUS CONTROL INSTALL ( rog-control-center ) FROM AUR MULTI REPO*********






 
