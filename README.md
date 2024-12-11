# lenovo-wwan-unlock
Modified version of the FCC and DPR unlock for Lenovo PCs, specifically tested as below

Instructions to perform FCC unlock and SAR config:

-----------------------------------------------------------------
List of Supported WWAN Modules and Systems:

1) WWAN module : Fibocom L860R+  
   Supported systems:
   - ThinkPad T15p Gen 3
     
   **Environment**:
   - Kernel version: 5.15 although it *should* work with all later kernels
   - ModemManager version: 1.20.0 or higher

Enablement is done on a Module + System basis. **Systems not listed 
are currently not supported.**

------------------------------------------------------------------------
Tested Operating Systems:
- Linux Mint 21.3 : OK

------------------------------------------------------------------------
**Please follow the procedure below step by step to enable WWAN**

1) Run the `fcc_unlock_setup.sh` script to
   install SAR config package and FCC unlock:
   ```
   chmod ugo+x fcc_unlock_setup.sh
   ./fcc_unlock_setup.sh
   ```
2) Reboot machine (Only needed once)

------------------------------------------------------------------------
**Please follow the procedure for uninstalling this package**

1) Run the `fcc_unlock_uninstall.sh` script to
   uninstall SAR config package and FCC unlock:
   ```
   chmod ugo+x fcc_unlock_uninstall.sh
   ./fcc_unlock_uninstall.sh
   ```
------------------------------------------------------------------------
Logs can be checked using **one** of the commands below:
- For FCC Unlock: `cat /var/log/syslog | grep -i DPR_Fcc_unlock_service`
- For SAR Config: `cat /var/log/syslog | grep -i configservice_lenovo`
- `journalctl`
- Please follow below steps to enable **Verbose** logging:
  1) **For FCC Unlock**:
  Add "-v" in FCC unlock scripts updated in "fcc-unlock.d.tar.gz", for example:

      FileName - fcc-unlock.d/8086:7560
  
      Modification- "./opt/fcc_lenovo/DPR_Fcc_unlock_service **-v**"

  2) **For SAR Config**:
      Add "-v" in systemd service file, for example:

      FileName - lenovo-cfgservice.service
  
  Modification- "ExecStart=/opt/fcc_lenovo/configservice_lenovo **-v**"    

------------------------------------------------------------------------
Additional Notes:
- If the Modem disappears after the machine reboots, please
restart it with the `systemctl restart ModemManager` command.
------------------------------------------------------------------------
