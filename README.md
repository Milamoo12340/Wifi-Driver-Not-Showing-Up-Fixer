Choose 1 script to run, Powershell is the recommended as you can choose either 2.5Ghz or the Dual Band in the same script. 

*Use my scripts to auto add these values or follow the instructions below for the exact way to fix your wifi drivers not showing up on your computer, if you aren’t in Australia but still have this issue, just look up the values or ask your local browser embedded AI for the values that match your country or region and change them according to your location. 
Most will need the 2.5Ghz script, and using the Dual Band will still not show your drivers if your computer chip only has the ability to recognise 2.5Ghz networks so please, try that one FIRST to make sure your driver is easily found.
You can try the dual network if you check online that your exact make and model computer is a dual band recognising PC or Laptop. you can skip the rest of this README if you want to use the script, or read if you want to manually make the adjustments.*”

In Australia, routers use channels 1 to 13 on the 2.4GHz band. However, your Wi-Fi card's hardware or Windows defaults to the US locale, which strictly restricts it to channels 1 to 11. If your router has dynamically chosen Channel 12 or 13 to avoid local interference, your laptop or PC will be completely blind to it.
Since your current driver locks you out of the "Country/Region" or "Channel Plan" advanced properties, there are much easier ways to fix this permanently without having to manually trick Windows into loading broken drivers.
Not many Wifi Techs will even know this, because you change your Region on your computer and it still doesn’t show up, they don’t understand that the drivers will still be set in your registry to be wired to the US region regardless of your computer region settings, so this is the secret.

If you don’t want to use the script, here’s the manual fix.
Press the Windows Key + R, type "regedit", and hit Enter.
2. Navigate to this path on the left-side folder tree:
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}
3. Inside these folder, you will see a list of numbered folders like 0000, 0001, 0002. Click through them until you find the one that lists your wireless card (e.g., "Ralink", "Atheros", or "Realtek") under the DriverDesc string on the right side.

If you hit F3 you can just type your exact driver name EXACTLY AS ITS SHOWN in your Driver Manager (press the Windows Key (usually next to the fn key) and R at the same time to open Run, then type devmgmt and enter to open Drive Manager to navigate to the Network Adapters section to find the name of your driver, clicking view and then show hidden in the tabs up top to find any hidden or missing drivers) and search for that using the F3 search button in regedit (Registry) window, you can keep hitting F3 if the found result isn’t in the specific HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318} path, and it will keep searching through the folders as you’ll see on the left folder view until you find it, since this is the exact location where you need to edit the settings, you must be in this folder, you can just manually go down the list and find the correct one if you want, you may have many folders with this path. 

8. Step 1: How to Create the Keys Correctly
Once you are in the correct numbered folder, look at the right pane for keys like CountryRegion, Country, or ChannelPlan.
Double-click that key and change the value:
	• For Ralink/MediaTek cards: Change the value to 5 or 0 (this unlocks channels 1–14).
	• For Atheros cards: Look for CountryCode and change it to AUS or 61.
6. If the key isn't there, you can right-click an empty space in that folder, select New > String Value, name it CountryRegion (or whatever matches your card type), and give it the broader value
1. Right-click on any empty white space in the right-hand pane of your specific numbered folder (e.g., 0001).
2. Hover over New and select String Value.
3. Type the Value Name exactly as shown below (case-sensitive) and press Enter.
4. Double-click the newly created string to open its properties, type the number into the Value data box, and click OK.

Step 2: The Exact Settings to Create
Create using string values as the key value type
Create these four keys one by one:
1. CountryRegion
	• Type: String Value (REG_SZ)
	• Value Data: 5 (This unlocks the full range of Australian channels 1–13/14).
2. RecommendedBand
	• Type: String Value (REG_SZ)
	• Value Data: 1 (Forces the card to prioritize the 2.4GHz frequency your router uses).
3. RecommendedChannel
	• Type: String Value (REG_SZ)
	• Value Data: 0 (Tells the card to automatically scan all available channels instead of getting locked onto just one).
4. WirelessMode
	• Type: String Value (REG_SZ)
	• Value Data: 7 (Sets the card to a clean 802.11b/g/n mixed mode so it can talk to modern router signals).


Step 3: Refresh the Network Card

The registry will not load into your hardware until you reset the adapter.
1. Press the Windows Key + X and click Device Manager.
2. Expand Network adapters, right-click your wireless card, and select Disable device.
3. Wait about 5 seconds, right-click it again, and select Enable device.
Once it turns back on, click the network icon in your taskbar. The card will now use these newly built rules to scan past channel 11 and find your SSID.

