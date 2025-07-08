# HA Marstek Venus E Modbus
Home Assistant Modbus Interface for Marstek Venus E 

## Version information
Version 0.02  
This version is the base version for Marstek Venus E.  

## Folders:
  [root]\
    EW11B   - Elfin EW11B\
      packages - Home Assistant packages\

## More information:
More information: https://gathering.tweakers.net/forum/list_messages/2282240  

## Disclaimer:
  The Home Assistant files from the packages folder is based on from @github/Superduper1969  
  https://github.com/Superduper1969/MarstekVenus-ElfinEW11  


# Installation: 
  ## Elfin EW11B:
    https://nl.aliexpress.com/item/32916128353.html  
    Note: Use the Wide range Voltage version.  
  
    Serial Port parameters on Elfin EW11B:
        Baud Rate = 115200
        Data Bit = 8
        Stop Bit = 1
        Parity = None
        Buffer Size = 512
        Gap Time = 50
        Flow Control = Half Duplex
        Cli = Disable
        Protocol = Modbus
    Comunication Settings on Elfin EW11B:
        Protocol = Tcp Server
        Local Port = 502
        Buffer Size = 512
        Keep Alive(s) = 60
        Timeout(s) = 300
        Max Accept = 3
        Security = Disable
        Route = Uart

  ## Installation of Elfin EW11B packages for Home Assistant:
    1.  Create the connector for your Marstek Venus E.
        Note: Beware of the Wiring schema.
    2.  Connect the Elfin to the Marstek Venus E Modbus connector, it will power up.
    3.  Confiugure the network settings of the Elfin. Preferable a fixed IP address. http://www.hi-flying.com/elfin-ew10-elfin-ew11
        Note: Choose STA as settings  
        Note: The Public IP address is the address what is in your Wifi network.  
    4.  Configure Serial Port (see above)
    5.  Configure Communication settings (see above)
    6.  Reboot the Elfin.
    7.  Login into Home Assistant and open Studio Code Server or just the native editor.
    8.  Create a folder packages in the root (where your configuration.yaml is).
    9.  Now open configuration.yaml.
    10. Find the section "homeassistant:".
    11. Add the following text (without the quotes): "  packages !include_dir_named packages"  
        Note: Watch the two spaces before packages, these MUST be included.
    12. Now upload the neede files from Github EW11B/packages folder to the packages folder in Home Assistant. 
        Note: If you have 1 Venus, just use the marstek_venus_battery_1_control.yaml, if you have 2, use also the marstek_venus_battery_2_control.yaml  
    13. Update the yaml file(s) by editing the IP addresses (see below).
    14. Restart HA.

  ## Configure the yaml files:
    1.  Open the file in Home Assistant with file editor.
    2.  Find [YourIPGoesHere] in the top of the file.
    3.  Replace it with the IP address of the Elfin.

  ## Help I have 3 or more Marsteks:
    1.  Make a copy of the file marstek_venus_battery_1_control.yaml
    2.  Rename the copy to marstek_venus_battery_n_control.yaml where n= The Marstek you want to add (3, 4, 5)
    3.  Open the new file in an editor.
    4.  Replace the Text "Marstek 1" (including space) to "Marstek n" where n is same as in line 2.
    5.  Replace the text "marstek_1" to "marstek_n" where n is the same as in line 2.

