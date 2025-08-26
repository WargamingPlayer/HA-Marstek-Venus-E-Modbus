# HA Marstek Venus E Modbus
Home Assistant Modbus Interface for Marstek Venus E 

## Version information

### Version 2025.8.4  
Changed Battery load values to device_type: energy_storage.  
Created (liniear) based sensors: Marstek_1_battery_soc_in_Wh.   
Removed bug from marstek_venus_totals.yaml where 3rd Marstek is not calculated correct in totals.  
Rebuid the Effeciency Sensors. Now based on total from the Venus C/E.  
Added a total efficiency sensor.  
Reformatted the yaml files.  

### Version 2025.8.3  
Registers 33000 - 33010 added.  

### Version 2025.8.2  
Sensors min/max Cell temperature now correct.  
Efficency percentage is all over the place. Need to find out how to make this working.  

### Version 2025.8.1  
Added Sensors, fixed some bugs.  
MAC now displayed as string.  
Software version added.  
EMS version added.  
BMS version added.  
Adjusted temp sensors to BMS 215, 213 had scale issue.  
Inverter state 6 added.  
Grid standard added.  
Power restriction switch removed, added value only.   
Efficiency added.  
WiFi strength is now -dBm.  

### Version 0.0.5  
Added sensors, fixed some scale bugs.

### Version 0.0.4
This version contains now 3 files for the Marstek E Venus Modbus integration of 3 Marsteks. 
This version also contains a couple of termplates for consolidating values when using the "Power Flow Card Plus card".  

### Version 0.0.3  
Added automations.  
  
### Version 0.0.2  
Bug fixes
  
### Version 0.0.1  
First version, fork of https://github.com/Superduper1969/MarstekVenus-ElfinEW11  

## Folders:
  [root]\
    EW11B   - Elfin EW11B\
      packages - Home Assistant packages\

## More information:
More information: https://gathering.tweakers.net/forum/list_messages/2282240  
Pascallj Modbus: https://docs.google.com/spreadsheets/d/e/2PACX-1vSyu0LKoSrQQzvrosMH-sOcSKT7pgHSXEwAcIJe0cy3NCrmwiLH6VDGjh0_2HOKhL0nZmnI3Mk5Fb_d/pubhtml?gid=319238506&single=true  


## Disclaimer:
  The Home Assistant files from the packages folder is based on from @github/Superduper1969  
  https://github.com/Superduper1969/MarstekVenus-ElfinEW11  


# Installation: 
  ## Marstek V2 Modbus cable to Elfin EW11B
  | Pin | Color  | EW11 Pin | Signal |
  |-----|--------|----------|--------|
  | 1   | Yellow | 1        | A      |
  | 2   | Red    | 4        | B      |
  | 3   | Black  | 3        | GND    |
  | 4   | -      | -        | -      |
  | 5   | Black  | 2        | VCC    |
  | 6   | Red    | -        | -      |
  
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
    14. Copy the marstek_venus_totals.yaml also to the packages folder.
    15. Restart HA.

  ## Configure the yaml files:
    1.  Open the file in Home Assistant with file editor.
    2.  Find [YourIPGoesHere] in the top of the file.
    3.  Replace it with the IP address of the Elfin.

  ## Help I have 4 or more Marsteks:
    1.  Make a copy of the file marstek_venus_battery_1_control.yaml
    2.  Rename the copy to marstek_venus_battery_n_control.yaml where n= The Marstek you want to add (4, 5, 6)
    3.  Open the new file in an editor.
    4.  Replace the Text "Marstek 1" (including space) to "Marstek n" where n is same as in line 2.
    5.  Replace the text "marstek_1" to "marstek_n" where n is the same as in line 2.
    6.  Replace the _1 at the bottom of the files at daily_charge and daily_discharge.

# Marstek Modbus reference
## Individual Marstek Venus
### Sensors per Marstek
| Name                                | id                                    | type                | data           |
|-------------------------------------|---------------------------------------|---------------------|----------------|
| Marstek x Com Module version        | marstek_x_com_module_version          | string              | 12 characters  |
| Marstek x Name                      | marstek_x_name                        | custom(10)          | 20 characters  |
| Marstek x Software version          | marstek_x_software version            | unint(16)           | xx.y           |
| Marstek x EMS version               | marstek_x_software version            | unint(16)           | xxx            |
| Marstek x BMS version               | marstek_x_software version            | unint(16)           | xxx            |
| Marstek x Wifi SSID                 | marstek_x_wifi_ssid                   | custom(16)          | 32 characters  |
| Marstek x MAC                       | marstek_x_mac                         | custom(6)           | 12 bytes       |
| Marstek x Wifi Status               | marstek_x_wifi_status                 | unint(16)           |                |
| Marstek x BT Status                 | marstek_x_bt_status                   | unint(16)           |                |
| Marstek x Cloud Status              | marstek_x_cloud_status                | unint(16)           |                |
| Marstek x Wifi Signal Strength      | marstek_x_wifi_signal_strength        | unint(16)           | -dBm           |
| Marstek x Battery Voltage           | marstek_x_battery_voltage             | unint(16)           | V              |
| Marstek x Battery Current           | marstek_x_battery_current             | int(16)             | W              | 
| Marstek x Battery Power             | marstek_x_battery_power               | int(32)             | W              | 
| Marstek x Battery SOC               | marstek_x_battery_soc                 | unint(16)           | % (battery)    |
| Marstek x Battery Energy            | marstek_x_battery_energy              | unint(16)           | kWh            |
| Marstek x AC Voltage                | marstek_x_ac_voltage                  | unint(16)           | V              |
| Marstek x AC Current                | marstek_x_ac_current                  | unint(16)           | A              |
| Marstek x AC Power                  | marstek_x_ac_power                    | int(32)             | W              |
| Marstek x AC Frequency              | marstek_x_ac_frequency                | unint(16)           | Hz             |
| Marstek x AC Offgrid Voltage        | marstek_x_ac_offgrid_voltage          | unint(16)           | V              |
| Marstek x AC Offgrid Current        | marstek_x_ac_offgrid_current          | int(16)             | A              |
| Marstek x AC Offgrid Power          | marstek_x_ac_offgrid_power            | int(32)             | W              |
| Marstek x Total Charging Energy     | marstek_x_total_charging_energy       | unint(32)           | kWh            |
| Marstek x Total Discharging Energy  | marstek_x_total_discharging_energy    | unint(32)           | kWh            |
| Marstek x Daily Charging Energy     | marstek_x_daily_charging_energy       | unint(32)           | kWh            |
| Marstek x Daily Discharging Energy  | marstek_x_daily_discharging_energy    | unint(32)           | kWh            |
| Marstek x Monthly Charging Energy   | marstek_x_monthly_charging_energy     | unint(32)           | kWh            |
| Marstek x Monthly Discharging Energy| marstek_x_monthly_discharging_energy  | unint(32)           | kWh            |
| Marstek x Internal Temperature      | marstek_x_internal_temperature        | int(16)             | °C             |
| Marstek x Internal MOS1 Temperature | marstek_x_internal_mos1_temperature   | int(16)             | °C             |
| Marstek x Internal MOS2 Temperature | marstek_x_internal_mos2_temperature   | int(16)             | °C             |
| Marstek x Max Cell Temperature      | marstek_x_max_cell_temperature        | int(16)             | °C             |
| Marstek x Min Cell Temperature      | marstek_x_min_cell_temperature        | int(16)             | °C             |
| Marstek x Inverter State            | marstek_x_inverter_state              | int(16)             |                |
| Marstek x Battery Charge Limits     | marstek_x_battery_charge_limits       | custom(3) uint(16)  | array          |
| Marstek x Battery Maximum Cell V... | marstek_x_battery_maximum_cell_vol..  | float               | x.yyyV         |
| Marstek x Battery Minimum Cell V... | marstek_x_battery_minimum_cell_vol..  | float               | x.yyyV         |
| Marstek x RS485 Control Mode        | marstek_x_rs485_control_mode          | uint(16)            |                |
| Marstek x Force Charge/Discharge M  | marstek_x_force_charge_discharge_mode | uint(16)            |                |
| Marstek x Charge to SOC             | marstek_x_charge_to_soc               | uint(16)            | %              |
| Marstek x Forcible Charge Power     | marstek_x_forcible_charge_power       | uint(16)            | W              |
| Marstek x Forcible Discharge Power  | marstek_3_forcible_discharge_power    | uint(16)            | W              |
| Marstek x User Work Mode            | marstek_x_user_work_mode              | uint(16)            |                |
| Marstek x Capacity and Power reg..  | marstek_x_capacity_and_power_registers| custom(4) uint(16)  | array          |
| Marstek x Alarm State               | marstek_x_alarm_state                 | custom(2) uint(16)  | array          |
| Marstek x Fault State               | marstek_x_fault_state                 | custom(4) uint(16)  | array          |
| Marstek x Discharging in kWh        | marstek_x_discharging_in_kwh          | uint                | kWh            |
| Marstek x Charging in kWh           | marstek_x_charging_in_kwh             | uint                | kWh            |
| Marstek x Power Limit 800W          | marstek_x_power_limit_800w            | uint                | 0=yes, 1=no    |
| Marstek x Grid standard             | marstek_x_grid_standard               | uint                | x              | 


### Switches
| Name                                | id                                    | on                  | off            |
|-------------------------------------|---------------------------------------|---------------------|----------------|
| Marstek x Device Reset**            | marstek_x_device_reset                | 0x55AA              | 0              |
| Marstek x Factory Reset**           | marstek_x_factory_reset               | 0x55AA              | 0              |
| Marstek x Backup Enabled***         | marstek_x_backup_enabled              | 0                   | 1              |
** Experimental  
*** This switch reverses the modbus reading  
  
### Input numbers & Input select
These numbers are adjusted by the state of the Venus. And also adjust the state of the Venus when changed. This is done  
by the automations inside the yaml.  
| Name                                | id                                    | min    | max    | step   | mode      |
|-------------------------------------|---------------------------------------|--------|--------|--------|-----------|
| Marstek x (dis)charging power**     | marstek_x_discharging_charging_power  | -2500  | 2500   | 50     | slider    |
| Marstek x Set maximum discharging.. | marstek_x_set_max_discharging_power   | 50     | 2500   | 10     | box       |
| Marstek x Set maximum charging po.. | marstek_x_set_max_charging_power      | 50     | 2500   | 50     | box       |
| Marstek x Set Battery minimum SOC.. | marstek_x_set_battery_min_soc         | 11     | 25     | 0.1    | box       |
| Marstek x Set Battery maximum SOC.. | marstek_x_set_battery_max_soc         | 75     | 100    | 0.1    | box       |
| Marstek x User Work Mode            | marstek_x_user_work_mode_input_select | -      | -      | -      | select    |
  
** Avoid using, might be removed and then will break your dashboard.  
### Scripts
| id                                  | Description                                                                  |
|-------------------------------------|------------------------------------------------------------------------------|
| marstek_x_set_forcible_charge       | Executed this script will set the Marstek to the action defined by           |
|                                     | marstek_x_discharging_charging_power                                         |

### Automations
| id                                     | Alias                                    | Description                    |
|----------------------------------------|------------------------------------------|--------------------------------|
| marstek_x_sync_modbus_and_input_select | Marstek x Sync Modbus and Input Select   | Synchronizes User Mode with    |
|                                        |                                          | input_select. Beware that it   |
|                                        |                                          | just sets Trade or Manual      |
| marstek_x_sync_modbus_and_max_charge   | Marstek x Sync Modbus and Maximum Charge | syncs max with Venus           |
| marstek_x_sync_modbus_and_max_discha.. | Marstek x Sync Modbus and Maximum Dis..  | syncs max with Venus           |
| marstek_x_sync_modbus_and_ba.._min_soc | Marstek x Sync Modbus and Min SOC        | syncs min with Venus           |
| marstek_x_sync_modbus_and_ba.._max_soc | Marstek x Sync Modbus and Max SOC"       | syncs max with Venus           |
The automations sync the input fields.  

### Template sensors
| Name                                                    | id                                           | value     |
|---------------------------------------------------------|----------------------------------------------|-----------|
| Marstek x Charging in W                                 | marstek_x_charging_in_w                      | W         |
| Marstek x Discharging in W                              | marstek_x_discharging_in_w                   | W         |
| Marstek x Force Charge/Discharge Mode Status            | marstek_x_force_charge_discharge_mode_status | string    |
| Marstek x RS485 Control Mode Status                     | marstek_x_rs485_control_mode_status          | string    |
| Marstek x State                                         | marstek_x_state                              | string    |
| Marstek x Operational mode                              | marstek_x_operational mode                   | string    |
| Marstek x Alarm PLL Abnormal Restart                    | marstek_x_alarm_PLL_abnormal_restart         | 0,1       |
| Marstek x Alarm Fan Abnormal Warning                    | marstek_x_alarm_fan_abnormal_warning         | 0,1       |
| Marstek x Alarm Low Battery SOC Warning                 | marstek_x_alarm_low_battery_SOC_warning      | 0,1       |
| Marstek x Alarm Output Overcurrent Warning              | marstek_x_alarm_output_overcurrent_warning   | 0,1       |
| Marstek x Alarm Abnormal Line Sequence Detection        | marstek_x_alarm_abnormal_line_sequence_..    | 0,1       |
| Marstek x Alarm WIFI abnormal                           | marstek_x_alarm_wifi_abnormal                | 0,1       |
| Marstek x Alarm Blutooth abnormal                       | marstek_x_alarm_blutooth_abnormal            | 0,1       |
| Marstek x Alarm Network abnormal                        | marstek_x_alarm_network_abnormal             | 0,1       |
| Marstek x Alarm CT connection abnormal                  | marstek_x_alarm_ct_connection_abnormal       | 0,1       |
| Marstek x Battery maximum SOC (Charge)                  | marstek_x_battery_maximum_soc                | %         |
| Marstek x Battery minimum SOC (Discharge)               | marstek_x_battery_minimum_soc                | %         |
| Marstek x Maximum Charge Power                          | marstek_x_max_charge_power                   | W         |
| Marstek x Maximum Discharge Power                       | marstek_x_max_discharge_power                | W         |
| Marstek x Battery Cell Voltage Delta                    | marstek_x_battery_cell_voltage_delta         | V         |
| Marstek x Efficiency Percentage                         | marstek_x_efficiency_percentage              | %         |
| Marstek x Battery SOC in Wh                             | marstek_x_battery_soc_in_Wh                  | Wh        |

### Utility meters
| Name                                                    | id                                           | Interval  |
|---------------------------------------------------------|----------------------------------------------|-----------|
| Marstek x Daily Discharging in kWh                      | marstek_x_daily_discharging_in_kwh           | daily     |
| Marstek x Daily Charging in kWh                         | marstek_x_daily_charging_in_kwh              | daily     |

## Overall Sensors
Overall sensiors are consolidating the three seperate Marsteks. Beware that this is not just a simple add. Values are  
calculated.
  
### Sensors
| Name                                | id                                    | type                | data           |
|-------------------------------------|---------------------------------------|---------------------|----------------|
| Marstek Discharging in kWh          | marstek_discharging_in_kwh            | unint               | kWh            |
| Marstek Charging in kWh             | marstek_charging_in_kwh               | unint               | kWh            |
  
### Template Sensors
| Name                                                    | id                                           | value     |
|---------------------------------------------------------|----------------------------------------------|-----------|
| Marstek Charging in W                                   | marstek_charging_in_w                        | W         |
| Marstek Discharging in W                                | marstek_discharging_in_w                     | W         |
| Marstek Batteries Energy                                | marstek_batteries_energy                     | Wh        |
| Marstek Batteries Charge                                | marstek_batteries_charge                     | Wh        |
| Marstek Batteries SOC                                   | marstek_batteries_soc                        | %         |
  
### Utility meters
| Name                                                    | id                                           | Interval  |
|---------------------------------------------------------|----------------------------------------------|-----------|
| Marstek Daily Discharging in kWh                        | marstek_daily_discharging_in_kwh             | daily     |
| Marstek Daily Charging in kWh                           | marstek_daily_charging_in_kwh                | daily     |
