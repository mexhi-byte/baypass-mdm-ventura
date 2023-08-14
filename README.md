# baypass-mdm-ventura
baypass-mdm-ventura

IPSW: https://ipsw.me/product/Mac.

Apple Configurator 2: https://apps.apple.com/us/app/apple-configurator-2/id1037126344
__________________________________________________________________________________________________________________
I. RESET MACOS WITH IPSW
a. Power off MacBook, press and hold the power button to enter Recovery

b. Open Disk Utility, remove Macintosh HD

c. Reboot, connect to the network to Activate Mac.

d. Plug the C cord in the first port of the MacBook into the other Mac, then power off the MacBook

d. Hold down the Control (L) + Option (L) + Shift (R) + Power key combination for 10 seconds

e. Release the other keys, but keep holding the Power key for another 10 seconds

f. MacBook is returned to DFU, open Apple Configurator 2 on the other Mac and drag and drop the IPSW file in

g. After about 10 minutes, the installation is successful, MacBook will reboot into macOS
___________________________________________________________________________________________________________________
II. BYPASS CONNECTING NETWORK IN MACOS VENTURA's ASSISTANT SETUP
___________________________________________________________________________________________________________________
a. Power off MacBook, press and hold the power button to enter Recovery

b. Open the Terminal tool, type the following command to enable the root account and set a password for the root account:

_____________________________________________________________________________________________________________________________
                  dscl -f /Volumes/Data/private/var/db/dslocal/nodes/Default localhost -passwd /Local/Default/Users/root
(Depending on how macOS is installed, the Data partition path may be different. In the case of USB installation, the Data partition will be named "Macintosh HD - Data")

      Enter the password for the root account (need to meet the security criteria, different from the user account password).
c. Restart the MacBook, manipulate the steps to set the language, region... to the Wi-Fi connection, stop (do not enter the Wi-Fi password).

d. Press 4 keys Command + Option + Control + T at the same time to open Terminal

e. Select the Apple logo in the upper left corner of the screen, select System Settings -> User & Groups -> Add Account.

f. macOS will ask for user authentication, enter user as root and password as the password you created earlier.

g. Create a new user account for macOS, the New Account section should be Administrator.

H. After creating the account, power off the MacBook and then hold the power button to enter Recovery.

i. Open the Terminal tool, type the following command and press enter:
_________________________________________________________________________________________________________________________
        touch /Volumes/Data/private/var/db/.AppleSetupDone
(Depending on how macOS is installed, the Data partition path may be different. In the case of USB installation, the Data partition will be named "Macintosh HD - Data")
_____________________________________________________________________________________________________________________________________
k. Restart your MacBook, then log in to the user account you just created.

Note: After successful login, you should actively disable the root account by opening Terminal and typing the command:

      dsenableroot -d

____________________________________________________________________________________________________________________________________________
III. SELECT DEP NOTIFICATION FOR MACBOOK MDM

a. Complete initial setup, don't connect to Wi-Fi during setup

b. Open the Terminal software, then execute as root by typing:

         sudo -i
         
c. Continue typing the following commands to block the host:

         echo "0.0.0.0 iprofiles.apple.com" >> /etc/hosts
         echo "0.0.0.0 mdmenrollment.apple.com" >> /etc/hosts
         echo "0.0.0.0 deviceenrollment.apple.com" >> /etc/hosts

         
d. Check if the hosts file has changed or not:


        cat /etc/hosts
        
e. Restart the device, connect to Wi-Fi and use as usual
_________________________________________________________________________________________________________________________________________________
IV. UPDATE OTA CHO MACBOOK MDM
___________________________________________________________________________________________________________________________________________________
a. Go to System Preferences -> Software Update to check for updates

b. Download the update

c. Disconnect from the network (forget Wi-Fi, turn off AP, block MAC address on router...), then select Reboot

d. Once the update is complete, the MacBook will reboot to the Setup screen

e. Not connected to the network, if the device asks for the iCloud password, select Set Up Later

f. After entering the main macOS screen, open Terminal and type the following command to check the hosts file:

            cat /etc/hosts

g. If the hosts file is restored to default, block it with the command:

         echo "0.0.0.0 iprofiles.apple.com" >> /etc/hosts
         echo "0.0.0.0 mdmenrollment.apple.com" >> /etc/hosts
         echo "0.0.0.0 deviceenrollment.apple.com" >> /etc/hosts

H. Connect to Wi-Fi and use as usual
