# PLEASE READ!

Honestly I didn't want to write this at the time because of the brick risks involved but nowadays can be fixed really easily.

## Notes
- You lose eshop access but game updates do still work.
- If you are not that experienced with Wii U Homebrew, do not follow this. It's not as easy as region changing, say the 3DS.
- Unblock updates with UFDiine before following this guide (if you dont re-create the update folder it will bite you in the ass later in the guide).
- That being said, be careful and have a NAND Backup just in case. I am not responsible if you fuck up your system.

## What you need:
- A Brain, a large one at that.
- A way to run [UDPIH](https://github.com/GaryOderNichts/udpih) to be able to run the recovery_menu. You *might* be able to do this without it but dont take your chances.
- A modified [recovery_menu](https://raw.githubusercontent.com/Lazr1026/regionchange/main/files/recovery_menu). ([Source](https://github.com/Lazr1026/recovery_menu))
- [Python](https://www.python.org/downloads/)
- [wupclient.py](https://github.com/Lazr1026/regionchange/raw/main/files/wupclient.py) (right-click -> Save link as… -> Click Save)
- A text editor. Notepad will be fine
- If you need help, join [my server](https://discord.gg/HNDcTEkcR3) and ask in `#help`.

## Region Changing
1. Create a file on the root of your sd named `network.cfg` and insert the following into it:
	- If using a wifi connection (obviously replace `ssid` and `key` with what they should be):
```
type=wifi
ssid=ssidhere
key=wifikeyhere
key_type=WPA2_PSK_AES
```
	- If using an ethernet connection:
```
type=eth
```
1. Format your console. Yes this is required. I'll explain why later (scroll down).
1. Pair a gamepad and then shut down.
1. Load the recovery_menu with UDPIH.
1. Navigate to "Load Network Configuration" and press a button to exit back to the main menu.
1. Start wupserver in the recovery_menu.
1. Edit the `wupclient.py` file in a text editor and change the IP on line 140 with the one for your console. Do not change the port.
1. Open the command line/terminal where you saved `wupclient.py`.
1. Windows: `py -3 -i wupclient.py` macOS/Linux: `python3 -i wupclient.py`.
1. Insert `w.dl("/vol/system/config/sys_prod.xml")` into the CLI.
1. Open `sys_prod.xml` in a text editor.
	- Replace the `product_area` value with the desired region. 1 = JPN, 2 = USA, 4 = EUR. Also replace the `game_region` value with `119` (RegionHax).
	- Make sure you save your changes!
1. Insert `w.up("sys_prod.xml", "/vol/system/config/sys_prod.xml")` into the CLI.
1. Exit wupclient with `exit()`.
1. Press a button on the wiiu to shut down wupserver and go to `Set Coldboot Title`.
1. Set the System Settings for your current region as the default title.
1. Reboot.
1. Set an internet connection.
1. Start a System Update. It should start to "Update".
1. Wait for the update to finish. When its done you should be taken to the desired regions Wii U Menu.
   - If you get an error about the gamepad region, ignore it. This is to be expected.
1. Complete initial setup.
   - You will see duplicate titles. This is normal as the titles from the original region are still installed.
1. Get back into recovery_menu and start wupserver again.
1. Insert `remove_system_titles('REGION')` into the CLI. 
   - Replace `REGION` with the consoles original region (USA, EUR, or JPN).
1. Wait for the old titles to be removed.
1. Exit wupclient (`exit()`).
1. Press a button on the wiiu to shut down wupserver and go to `Shutdown`.

### Removing the Gamepad Update Nag
1. Get back into recovery_menu and start wupserver again.
1. Insert `w.dl("/vol/system/proc/prefs/DRCCfg.xml")` into the CLI.
1. Open `DRCCfg.xml` in text editor.
	- Change `versionCheckFlag` to 0.
	- Save the file.
1. Insert `w.up("DRCCfg.xml", "/vol/system/proc/prefs/DRCCfg.xml")` into the CLI.
1. Exit wupclient (`exit()`).
1. Press a button on the wiiu to shut down wupserver and go to `Shutdown`.
1. The console should no longer try to update the gamepad.

### WTF? WHY DO I HAVE TO FORMAT?
You have to format the system or else you will not boot after changing the `product_area` value. I dont know why especially since I have changed it in the past and I was still able to boot fine.

## Credits
- Lazr - Figured out how to do it. The writeup is [here](/docs/writeup.md).
- GaryOderNichts - UDPIH and the recovery_menu. (kinda) urged me to make this.
- Nightkingale- Helping figure out it out. In fact, he was writing [The Downgrade of Doom](https://nightkingale.github.io/posts/the-downgrade-of-doom) while I wrote this if you want to check it out.
- Maschell - Created [Tiramisu](https://tiramisu.foryour.cafe) and [Aroma](https://https://aroma.foryour.cafe) (these *really* helped with me gaining interest).
- Nonsocial for the wupclient mods (because I am too stupid for it).
