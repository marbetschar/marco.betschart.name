---
description: ''
---

# Dell XPS 7390 eGPU

## Windows 10 with AMD Radeon RX580

1. Install the latest Windows 10 Pro
2. Install potentially missing Drivers using the Optional Packages in Windows Update
3. Add "Link State Power Management" to the Windows Power options and set it to Off while plugged in
4. Reboot
5. [Download the AMD Radeon Drivers v19.12.3](https://www.amd.com/en/support/kb/release-notes/rn-rad-win-19-12-3), because in the Adrenalin 2020 version of the driver does not work correctly due to an issue in Windows 10 not correctly identifying the eGPU as switchable graphics
6. Plug Razor Core X with RX580 into the Thunderbolt 3 port which is also used for power delivery
7. Wait until Windows correctly identifies and installed all drivers for the RX580
8. Install the previously downloaded AMD Radeon Drivers v19.12.3
9. Reboot

## Sources

* [https://www.tenforums.com/tutorials/100629-remove-link-state-power-management-power-options-windows-10-a.html](https://www.tenforums.com/tutorials/100629-remove-link-state-power-management-power-options-windows-10-a.html)
* [https://community.amd.com/t5/graphics/missing-switchable-graphics-option/td-p/134775](https://community.amd.com/t5/graphics/missing-switchable-graphics-option/td-p/134775)
* [https://community.amd.com/t5/drivers-software/rx570-code-43-windows-10/td-p/165079](https://community.amd.com/t5/drivers-software/rx570-code-43-windows-10/td-p/165079)

