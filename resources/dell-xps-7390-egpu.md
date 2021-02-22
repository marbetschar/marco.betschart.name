---
description: ""
---

# Dell XPS 7390 eGPU

## Windows 10 with AMD Radeon RX570

 1. Install the latest Windows 10 Pro
 2. Install potentially missing Drivers using the Optional Packages in Windows Update
 3. Add "Link State Power Management" to the Windows Power options and set it to Off while plugged in
 4. Reboot
 5. Download the AMD Radeon Drivers v19.12.2, because in the Adrenalin 2020 version of the driver does not work correctly due to an issue in Windows 10 not correctly identifying the eGPU as switchable graphics
 6. Plug Razor Core X with RX570 into the Thunderbolt 3 port which is also used for power delivery
 7. Wait until Windows correctly identifies and installed all drivers for the RX570
 8. Install the previously downloaded AMD Radeon Drivers v19.12.2
 9. Reboot
10. Theres probably an error 43 in the Device Manager, claiming the GPU does not work correctly. If this is the case, download and execute the atikmdag-patcher-1.4.8 (use Google, its download link is provided in several Cryptocoin boards)
11. Reboot again
12. Now you should be all set. Check by opening the Windows "Graphic Settings" - it should allow you to set the Radeon RX570 for an application as "High Performance GPU"

## Sources

* https://www.tenforums.com/tutorials/100629-remove-link-state-power-management-power-options-windows-10-a.html
* https://community.amd.com/t5/graphics/missing-switchable-graphics-option/td-p/134775
* https://community.amd.com/t5/drivers-software/rx570-code-43-windows-10/td-p/165079