==============================================
Dell Display Manager
===============================================

Automatic install/uninstall.

32/64-bit OS support:
Windows 11 (22H2 b25140.1000)
Windows 10
Windows 8
Windows 7
Windows Vista

Requires one or more Dell DDC/CI and asset management 
enabled monitors, and Windows Vista or a newer OS 
with a WHQL display driver that supports DDC/CI. 

Troubleshooting
-----------------------------------------------
If DDM is unable to detect and/or communicate with
a supported Dell monitor:
- check the monitor OSD to ensure DDC/CI is enabled
- make sure you have the correct and latest display
  driver from the graphics vendor (AMD, Intel, NVidia)
- remove any docking stations or cable extenders or
  converters between the monitor and the graphics port
- with first generation DP 1.2 monitors, it may be 
  necessary to disable MST/DP 1.2 in the monitor OSD
- wireless and gaming displays with NVidia G-Sync 
  scalers do not support DDC/CI and/or DDM

A diagnostic log can be generated from the DDM program
service menu: while holding down the SHIFT key, 
right-click on the DDM system tray icon and then select 
"Save diagnostic report" from the popup menu.

DisplayLink / e-Docks
-----------------------------------------------
USB DisplayLink-based graphics may require version 8.0 
or newer USB Graphics Software from DisplayLink. USB-C and
Thunderbolt docks may require updated Intel dock drivers. 

Virtual Machines / Windows on ARM
-----------------------------------------------
Virtual machine environments and WoA platforms lack 
DDC/CI support; in consequence only Easy Arrange and
associated features will be available.

Portability, Installation Privileges and UAC
-----------------------------------------------
Because DDM interacts directly with monitor firmware, the
program - by default and design - requires administrative
privileges to install. However, the ddm.exe program itself
is designed to be portable and requires no special 
privileges to run; and DDM can be installed and run from
a network server. In addition, a version of DDM is 
available in the Windows Store that requires no special 
privileges.

Silent Deployment
-----------------------------------------------
To silently deploy Dell Display Manager, start the setup 
program with the "/VerySilent" command-line parameter. To
install silently to a specific folder, add the parameter
"/Dir=FullPathName".

To silently run Dell Display Manager, with no user
interface, start the program itself with the "/VerySilent" 
command-line parameter.

Auto-rotation
-----------------------------------------------
Auto-rotation is only available on displays with 
supporting firmware, and only applies to changes in 
physical or OSD menu orientation made while Dell Display 
Manager is connected to the monitor.

Input management
-----------------------------------------------
Input management is only available on displays with 
supporting firmware.

Easy Arrange
-----------------------------------------------
Easy Arrange is now available on all display 
models, and while enabled may disable Microsoft Snap
window dragging to minimize feature overlap. To 
temporarily disable Easy Arrange while moving a 
window, hold down the Shift key until the move 
completes. A checkbox is provided to reverse 
this default logic, and leave Windows Snap enabled.

Easy Arrange is subject to Windows UAC policy, and can
only interact with applications that are running with 
equal or lower privileges.   

Auto Mode and Metro/Windows apps
-----------------------------------------------
To associate a Metro/Windows app with a Preset mode, 
open the app on the Windows 10 desktop and drag-and-drop 
the top-left corner of the app window into the Auto Mode 
application list. If Easy Arrange is enabled, it may be 
necessary to change the state of the Shift key to 
temporarily disable auto-positioning.

Preferrably, access the DDM application menu in/on the 
target app window, and simply select the desired Preset
mode for the popup menu; the choice will be registered 
and remembered in the Auto Mode application list. 

Note that if DDM Night Mode support is enabled Auto Mode 
is disabled while Windows Night Light (Mode) is active. 

Hotkeys
-----------------------------------------------
With the exception of the input switching hotkeys, which
are unique to each monitor, hotkeys are shared and - where
appropriate - targeted at the monitor the Windows mouse
pointer is on.

Command language
-----------------------------------------------
A rich and flexible command language is supported via the
command-line, and command-line arguments can be combined.
Where appropriate, a specific display can be targeted by
prefacing the command with the monitor EDID serial number 
or enumerated display number, e.g., "2:AutoSetup"; if a 
display serial or enumerated number is not specified the 
command will be applied to the current selected display 
or to all displays, as appropriate. Commands include:
 
SetActiveInput [DVI2/HDMI/DP2,etc] - switches active input
RestoreFactoryDefaults - restores factory defaults*
AutoSetup - executes an autosetup (analog only)*
RestoreLevelDefaults - restores level defaults*
RestoreColorDefaults - restores color defaults*
SetBrightnessLevel X - sets brightness to X% (0-100)*
SetContrastLevel X - sets contrast to X% (0-100)*
SetNamedPreset [Movie/CAL1,etc] - changes the Preset mode*
SetPowerMode [on/off] - sets the display power mode*
SetOptimalResolution - switches to optimal resolution
SaveProfile [Name] - save settings to named profile*
RestoreProfile [Name] - restore settings from named profile*
DeleteProfile [Name] - delete named profile
SetGridType [X] - changes Easy Arrange grid type to X
Rescan - rescans display hardware
ForceReset - reconnects and rescans display hardware
SetControl X Y - sets hex control X to hex value Y
IncControl X Y - increases the value of control X by Y
DecControl X Y - decreases the value of control X by Y
SetPxPMode [Off/PiP/PBP Main Sub1] - set PxP mode/inputs
Zoom - switches between PxP and fullscreen mode
Wait X - pause X milliseconds
Exit - terminates the program
 
Some of these commands require familiarity with the MCCS
standard. For example, on monitors that support it the 
command to switch the OSD language to Spanish would be 
"SetControl CC 0A"; to unlock an OSD that has been 
inadvertently locked "SetControl CA 02".

Instructions can be combined on the command-line, and
assigned to standard Windows shortcuts with optional 
hotkeys or coupled with the native Windows Task 
Scheduler to execute at certain times.

For example:
 
  "ddm.exe /RestoreLevelDefaults /2:SetContrastLevel 70"
 
would first restore level defaults on all monitors, and 
then set the contrast level on monitor #2 to 70%. 

  "ddm.exe /G606K4NP0:SetPxPMode Quad DP1 HDMI2 HDMI1 DP2"

would target the monitor with service tag/serial number 
"G606K4NP0", turn PBP-quad on, and set the main window 
input to DP1, and the three sub window inputs to HDMI2, 
HDMI1 and DP2 respectively.

Note also that the serial number or service tag is the one 
provided by the monitor EDID, and may be different from the 
one affixed to the back of the monitor. The EDID serial 
number can be found in the DDM About box, and in the 
shortcut created from the DDM monitor service menu: while 
holding down the SHIFT key, click on the DDM About button 
and then select "Create shortcut" from the popup menu.

NB: If not targeted to a specific monitor, commands listed
above that are tagged with an asterisk (*) apply to all
monitors to facilitate simple and uniform control over all
members of a multimonitor matrix. For instance, if executed
on a matrix of 16 similar monitors, the command-line:
 
  "ddm.exe /SetNamedPreset Warm /SetBrightnessLevel 75"
 
would set all 16 monitors to Warm preset mode, with a
brightness level of 75%.

A tiny DDM-dependent console app - ddmcmd.exe - is also 
available for placement in the environment path to facilitate 
speedier command execution and to view results.

===============================================
History
===============================================
08/25/2022 - 1.56.2109
- Added support for G3223Q FW ECR
- Qualified night mode support
06/22/2022 - 1.56.2107
- Added support for U4323 USB upstream assignments
- Redesigned PIP/PBP toolbar
- Disabled PBP controls/wizard when iMST is enabled
- Removed VE for AW2x23
05/26/2022 - 1.56.2103
- Augmented CLI
05/14/2022 - 1.56.2102
- Improved EA custom layouts on VM platforms
- Added preliminary support for U4323Q 
- Included ddmcmd.exe console app
- Added Ukrainian localization
- Implemented friendly monitor names
- Stretched pause after HPD event 
- Restored EA after internally generated PIP/PBP change 
- Implemented model exclusion support
- Improved trackbar behavior/sync with OSD
- Relaxed constraints on FW version decoding
01/30/2022 - 1.55.2090
- Fixed EA virtual desktop support under Win11
- Qualified UI display of FW string 
- Removed tag window option under Win11
- Improved handling of FY22+ PIP/PBP mode changes
- Changed discovery messaging
- Added constraints on DDM window size
- Implemented conditional DDM window position recall
- Redesigned low level kbd hooks
- Implemented VE preview
- Added Night support
- Fixed several UI anomolies
- Synced DDM to EAM v3.1
- Extended matrix control to mini-presets
- Increased DebugRead retries
- Removed preliminary DDM 2.0 feature set
- Excluded Win11 Start menu from auto-mode
09/28/2021 - 1.54.2068
- Revised low level kbd hook
- Reordered discovery logic
- Fixed matrix contrast control
- Improved VE hotkeys
09/01/2021 - 1.53.2065
- Added preliminary support for Windows 11
- Added support for Novatek scalers
- Added special support for IE and Chrome windows
- Enhanced z-order detection
- Automated followup to DDM resolution changes
- Added support for G-series VE feature set
- Improved support for UP27/UP32
- Revised FW string encoding on older models
- Optimized discovery
- Added auto mode support for Chromium-Edge
06/23/2021 - 1.52.2056
- Added workaround for broken mobile Intel/NV HDMI port
- Fixed FW string parsing error
06/10/2021 - 1.52.2054
- Localized Dell web help links based on LCID
05/26/2021 - 1.52.2052
- Added additional info to diagnostic report
- Added web link to model specific support
- Rationalized basic and advanced menus
- Implemented MRU Easy Arrange toolbar
- Improved UI for system enhanced GDI scaling
- Added easy switch between discrete and spanned EA
- Update UI to reflect current UX guidelines
- Changed Easy Arrange MRU hotkey behavior
- Further improved Japanese localization
04/09/2021 - 1.51.2034
- Fixed mouse wheel scrolling in listboxes
- Improved resume from PowerNAP
- Excluded Start/Cortana from auto mode
- Confined custom EA captures to current virtual desktop 
- Changed BEC rules
- Fixed potential problem with video swap hotkey
- Updated and optioned low level keyboard hook
- Worked around broken AMD MST support
04/09/2021 - 1.51.2028j
- Corrected Japanese localization
02/27/2021 - 1.51.2028
- Disabled constrain window to desktop option 
- Fixed image list default value
02/04/2021 - 1.51.2027
- Added Polish and simplified future localizations
- Fixed issue with restoring minimized windows
- Added Create shortcut option to monitor service menu
- Added monitor list (with serial numbers) to About box
- Optimized restoring window positions
- Improved tag window behavior on startup
12/28/2020 - 1.51.2021
- Fixed zoom hotkeys for P4317
12/05/2020 - 1.51.2020
- Fixed KVM wizard PIP settings
- Improved SetPxP/SetActiveInput/SetSubInput
- Added SetPxPMode combining PXP mode+main+subs
- Fixed custom grid string
- Qualified KVM support in the absence of PBP
- Fixed and abbreviated text strings where necessary
- Changed tag window behavior after loss of focus
- Changed MST validity test
- Fixed potential silent install loop
- Added support for FW based Multi-Monitor Sync
- Changed FW string rendering
- Fixed PxP toolbar button behavior
- Updated DisplayLink driver identification
- Fixed Custom preset numbering
- Added alert when image controls are not available
- Improved handling of zoomed/iconic windows
- Added exceptions for U2720Q/QM
10/06/2020 - 1.51.2015
- Fixed incompatibility between older and newer SmartHDR flags 
- Added support for complex filenames to command line arguments
- Optimized installer
- Added KVM wizard support for C24/C27 
09/11/2020 - 1.51.2013
- Fixed UI for 67/33 PBP modes
- Expanded diagnostic log to include custom EA layouts
- Revised MST validity checks
- Made VCPE2 restore last on importing settings
- Adjusted UI to support BEC and PIP hotkeys
08/16/2020 - 1.51.2010
- Added gfx driver MST validity checks
- Added view options to Diagnostic and AM reports
- Updated unsupported icon
- Rationalized EA predefined layouts
- Improved custom cell recording under Win10
- Added icons to default automode categories
- Improved diagnostic UI
- Added support for new color presets
- Added support for new PBP modes
- Updated command-line arguments
- Fixed DecControl bug
- Fixed trackbar tick artifacts under 20H1 
- Improved restoring window positions
- Added customization tips to the selected EA partition
- Improved KVM wizard USB selection
- Added option to allow any hotkey combination
- Renamed USB1 to USB-B where appropriate
- Added support for USB upsteam switch to P3421/U3421
- Added support for PIP position hotkey to P3421/U3421 
- Enhanced and exposed compatibility problem notifications
- Improved hotkey string definitions
- Improved multi-scaled caption bar issues with app menu button
- Removed contrast control for UP2720Q
- Added broadcast to customized EA layouts
- Added support for S2721Q/QS
- Added SHIFT cancel auto-rearrange when changing EA layouts
- Added GetFirmwareVersion to command list
01/21/2020 - 1.50.1996
- Added workaround for Apple iTunes bug
- Added feature disable switches
01/06/2020 - 1.50.1995
- Added qualification to restore from PowerNap
- Added EA support for Qualcomm WoA
- Restored child window exclusions for AVEVA 
- Added check and exception wrapper for EA MRU
- Removed redundant DDM window refreshes
- Added unusual Windows metrics behavior traps
- Fixed maximized window restore issue
- Added U2520 FW notification
- Added U2518 automode support
- Added import/export settings commands
- Improved resizing of console windows
11/07/2019 - 1.50.1986
- Exposed additional hotkeys
- Added application window controls
- Enhanced Easy Arrange customization options
- Added support for Thunderbolt inputs
- Added KVM wizard 
- Added support for FY20 models
- Improved level attachments to preset modes
- Added per-monitor MRU for EA layouts
- Added sync mechanism with ISP
- Differentiated Alienware models
- Fixed Unicode tool tips
- Fixed disappearing hotkey control borders
- Added AutoMode exclusions
- Supplemented PowerNAP restore
- Optimized Easy Arrange
- Fixed and enhanced command-line processor
- Improved VM auto-detection
- Added EA support for non-standard window wrappers
- Added support for Citrix distributed apps
10/21/2019 - 1.40.1943
- Changed Alienware naming convention
- Revised Easy Arrange recall 
- Added prerequisite installation check
- Fixed USB swap hotkey issue w. frozen kbd
01/20/2019 - 1.40.1942
- Circumvented VD identification issue 
- Fixed mouse wheel trackbar scrolling
- Added support for 19H1
06/10/2018 - 1.40.1937
- Changed virtual desktop detection routines
10/08/2018 - 1.40.1936
- Added custom row/column options to EA
- Added autoexec cfg admin support
- Added optional binding of image adjust to presets
- Added panel source detection
- Added support for MSM offset
- Improved EyeFinity and NV Surround support
09/07/2018 - 1.40.1930
- Added force discovery option w. helpers
- Improved matrix error reporting
- Fixed potential PowerNap resume error
- Added support for Multiscreen Match preset
21/06/2018 - 1.40.1928
- Modified USB upstream assignment UI
- Added Thunderbolt driver check
- Optimized discovery
- Improved EA desktop spanning 
- Added support for U4919DW
- Added support for Multiscreen Match preset
- Fixed max/restore automode issue
22/05/2018 - 1.40.1924
- Added support for U3219Q
- Added input switching hotkeys for each monitor
- Restored admin option to disable updates
- Enabled Easy Arrange on all supported models
- Updated UI and exposed FY19 feature set
- Added support for targeted serial numbers
- Fixed hotkey disable bug
14/02/2018 - 1.31.1903
- Fixed landscape rotation issue under RS3
27/01/2018 - 1.31.1902
- Improved dialog box dimissal
- Corrected DCR behavior
- Synced desktop and Store app
17/12/2017 - 1.31.1899
- Optimized startup and discovery
- Updated command language 
06/11/2017 - 1.31.1898
- Improved Edge handler
- Updated support for HDR
04/10/2017 - 1.31.1897
- Fixed manual mode disabled bug
28/09/2017 - 1.31.1896
- Corrected overlapped UI controls
- Refined FY19 features
- Added support for new HDR and PXP modes
- Increased number of custom layouts
- Removed DUT identification logo
16/08/2017 - 1.31.1895
- Fixed USB switch on U3818DW
- Added active input check to PowerNAP
- Added support for roaming users
- Added support for Win10S
05/07/2017 - 1.31.1892
- Added qualifications for Chrome_widgets
09/06/2017 - 1.31.1890
- Fixed persistent menus after closing
- Resolved conflict between old and new EA records
- Updated Dell font
- Restretched discovery to cover I2C errors
03/05/2017 - 1.31.1887
- Fixed auto/manual preset mode UI
- Revised manually triggered discovery
- Improved clone handling
- Redesigned USB upstream selection
25/03/2017 - 1.31.1880
- Added suppport for unrestricted USB association
- Rewrote window layout routines (disabled)
- Restored overlap glass border option
- Optimized move/size window qualifications
- Updated localized strings
- Adjusted auto-rotation to PIP/PBP metadata
- Added restrictions for Smart HDR
14/02/2017 - 1.31.1867
- Added inventory support for AM
- Improved RestoreWindowLayout conditionality 
25/01/2017 - 1.31.1860
- Refined HDR/SDR mode switching
- Added preliminary 8Kx4K support 
- Revised USB-C source coding
- Improved VM support
24/12/2016 - 1.31.1848
- Added workaround for NV/Novatek DPrx
- Fixed FY extraction
- Extended EA to Win10 virtual desktops
- Added polling disable switch
- Enhanced diagnostic report
- Extended drag & drop 
- Fixed EA issue with Chrome
- Fixed auto-mode issue with UWP
- Fixed CAI hotkeys
- Standardized installation options 
- Added HDR support
- Enhanced RestoreWindowLayout conditionality 
02/06/2016 - 1.30.1800
- Fixed Input Manager control labels
- Extended auto-mode fullscreen policy coverage
- Added BEC support for new game modes
- Adjusted UI to hide unsupported controls
- Added default preset auto-mode for D3D
- Implemented FW revision check
05/05/2016 - 1.27.1792
- Added new game presets
- Implemented FW busy and wireless display flags
- Fixed default auto-mode
- Enabled Input Manager on MStar based models
- Validated DisplayLink 8.0 software
- Added PowerNap check/reset
26/04/2016 - 1.27.1790
- Added conditional polling logic to qualify MStar scalers
- Removed MHL from input labels
- Added workaround for MR-series HDMI cap string
- Fixed default preset auto-mode for Metro/Windows apps
- Added support for up to 16 user programmable hotkeys
- Eliminated redundant discovery
- Added independent auto-mode support for Metro/Windows apps
- Extended PowerNap support to lock screen
- Added /NOUPDATE setup option to disable auto-updates
- Stretched HPD delay 
- Re-enabled matrix support
- Changed uninstall link in Start menu to an option
24/02/2016 - 1.26.1759
- Added conditional model logic to support FY17 UP/P-series
- Fixed trackbar arrow/pg key behavior
- Optimized notification tray behavior
- Improved XP style UI scaling
- Added selectable preset mode for UWP apps
08/02/2016 - 1.26.1754
- Improved exception handling
- Added Input Manager
- Added PIP/PBP mode hotkeys
- Added Game mode black enhancement hotkey
- Eliminated unnecessary threads
- Added auto-run delay 
- Improved CI link detection
- Optimized polling mechanism
- Added support for ComfortView preset
- Fixed Vista/Win7/Win8 high-DPI issues
- Added EA glass border overlap option for Win10
- Add USB switch hotkey
06/11/2015 - 1.25.1652
- Added PBP check to KVM switch
- Added PBP underscan hotkey
- Synced hotkey selection mechanism with Windows
- Disable PBP underscan if PBP zoom is not available
25/10/2015 - 1.25.1640
- Added Smart Visibility support
- Expanded hotkey support via ddmext.dll
16/10/2015 - 1.25.1630
- Rewrote commandline procedures
- Added Wait command
- Exposed softKVM and softPBP hotkeys
08/10/2015 - 1.25.1612
- Enabled RestoreWindowLayout by default
06/10/2015 - 1.25.1610
- Extended RestoreWindowLayout to hotplug events
- Abbreviated notifications for Win10
- Improved hotplug DDC/CI detection
- Added processlist to diagnostic report
- Enhanced Refresh command with ForceReset
- Updated exception handler
- Fixed EA high DPI-awareness under Win7
- Removed obsolete DPI menu command under Win10
07/08/2015 - 1.25.1595
- Added softKVM input selection
06/08/2015 - 1.25.1592
- Added optional away mode
- Removed tool windows from EA processing
- Added hotkeys for PBP and softKVM
- Added support for optimized wallpaper
- Added special support for medical models
- Added support for per-model default preset 
27/05/2015 - 1.24.1586
- Added support for Rec2020 preset mode
- Relocated DND registration
- Disabled Game mode switch when unsupported
01/05/2015 - 1.24.1582
- Updated exception handler
- Changed drag-and-drop routines
- Added EA positioning hotkeys
12/04/2015 - 1.23.1580
- Revised interaction with Win10 Snap
- Fixed redundant clone notifications
- Added recognition of Windows 10.0 (ex-6.4)
- Changed multimonitor identifying bitmap and incidence
26/03/2015 - 1.23.1572
- Revised EA interaction with notifications
- Improved EA per monitor DPI awareness
- Improved RestoreWindowLayout procedure
- Fixed SVE issue with MStar controllers
- Updated hooks
- Removed control update redundancies
16/03/2015 - 1.22.1560
- Improved synchronization with OSD
- Trapped floating point exception
26/02/2015 - 1.22.1554
- Linked icm swapping to auto preset modes
23/02/2015 - 1.22.1553
- Added multimonitor identifiers
- Added optional ability to restore window positions after resume
- Improved polling policy for FY17 models
- Added support for new preset modes
- Added optional integration with desktop context menu
- Enhanced and exposed command processor
- Improved optional remote management 
12/01/2015 - 1.21.1508
- Partial support for new AMD virtual display
- Improved Easy Arrange handling of MDI apps
- Initial rewrite of polling mechanism
- Added better ICM support for cloned displays
25/10/2014 - 1.21.1500
- Fixed potential custom grid metric error
17/10/2014 - 1.20.1498
- Added support for windowed Metro apps
- Improved text size support
- Updated power policies
- Revised hotplug detection
08/07/2014 - 1.20.1476
- Added minimized window qualifications
- Further refined DPI-awareness
20/06/2014 - 1.20.1470
- Optimized startup procedure
- Revised capabilities string parsing
- Updated error trapping/reporting
- Improved Easy Arrange DPI-awareness
- Adjusted Easy Arrange custom grid
- Fixed Snap handling
27/04/2014 - 1.20.1450
- Enabled autorotation on large format displays
17/03/2014 - 1.20.1445
- Added disable auto-update option to installer
- Added support for Win81 desktop scaling
18/01/2014 - 1.20.1437
- Excluded Guest accounts from auto-update
- Enabled drag and drop with admin privileges under Win81
25/12/2013 - 1.20.1432
- Added periodic DDC/CI check
- Suspended VCP threads if window is moving
- Reformatted string resources
- Disabled frozen thread check
- Corrected popup window size
- Fixed UHD recognition
- Adjusted PowerNap resume procedures
- Added color space limits
22/11/2013 - 1.20.1392
- Added initial support for P2815Q
- Enhanced verbose error reporting
- Rewrote preset switch box
- Streamlined error trapping
- Added multiple AutoMode policies
- Enhanced power restore routines
11/11/2013 - 1.20.1365
- Adjusted delays for different scalars
11/10/2013 - 1.20.1360
- Fine tuned handling of 4k displays
- Improved support for localizations
- Disabled auto-Game when AutoMode disabled 
04/10/2013 - 1.20.1355
- Enabled drag and drop with admin privileges
- Changed UI in accord with UX preferences
- Improved CEA input timing support on 4k displays
- Removed hard coded presets
- Added text size control for 4k displays
03/09/2013 - 1.11.1321
- Improved workspace change handling
21/07/2013 - 1.11.1315
- Changed behavior if Zonal Color is enabled
- Disabled image controls if CAL1/2 enabled 
09/07/2013 - 1.11.1306
- Added default preset option to AutoMode
- Added UPxxxx14Q Metro preset check
05/07/2013 - 1.11.1304
- Changed AutoPreset default to off
- Hardcoded UPxx14Q presets
27/06/2013 - 1.10.1295
- Added support for FY14 E-series displays
24/06/2013 - 1.10.1292
- Lengthened STm UPxx14Q preset delay
- Added RunAsAdmin option to installer
10/05/2013 - 1.10.1289
- Added special UP3214Q preset mode checks
25/03/2013 - 1.10.1285
- Enhanced exception handling
- Added elevation checks
- Added Windows version check/warning to installer
- Improved interaction with Microsoft Snap
- Added shift-disable feature to Easy Arrange
- Excluded Excel workbooks from Easy Arrange
31/12/2012 - 1.09.1266
- Included additional error trapping
19/09/2012 - 1.09.1265
- Increased STm preset delays again
18/09/2012 - 1.09.1264
- Increased STm preset delay
17/09/2012 - 1.09.1262
- Adjust behavior in clone mode
- Added special support for TApps
13/09/2012 - 1.09.1260
- Added delay after Preset change
- Fixed custom grid layout
- Implemented STm preset delay
12/08/2012 - 1.09.1256
- Added SVE support
05/06/2012 - 1.08.1245
- Fixed Outlook 2007 linkage issue
- Improved image level input control
25/05/2012 - 1.08.1240
- Added special Metro support
24/04/2012 - 1.08.1236
- Fixed unicode preset notifications
- Changed XP discovery
18/04/2012 - 1.08.1235
- Added support for MSI advertisements
17/04/2012 - 1.08.1234
- Auto-close preset list if changed via OSD
- Added qualified V3 firmware support
- Distinguish screen from monitor ID
- Changed grid feature name
- Recheck preset on assigned change
10/04/2012 - 1.08.1230
- Added support for VCP F2h
- Added qualified E-series support
- Added model to preset name in clone mode 
29/03/2012 - 1.08.1223
- Fixed V2 brightness value update issue 
28/03/2012 - 1.08.1222
- Fixed V1 brightness value update issue
- Adjusted V1 PowerNap timing
26/03/2012 - 1.08.1221
- Adjusted V2 PowerNap timing
25/03/2012 - 1.08.1220
- Exposed ScreenSnap
- Consolidated PowerNap and Rotation as Options
- Expanded Quick Setting controls
- Removed Shift-qualifier from Snap
- Exposed localizations
20/03/2012 - 1.07.1207
- Fixed trackbar thumb missing
- Manual-mode now always reverts to Standard preset
13/03/2012 - 1.07.1205
- Added support for VCP F1h bitfield
- Qualified auto-presets for both E and P series
- Fixed Intel/WinXP issue with powernap
07/03/2012 - 1.07.1203
- Additional checks for valid shortcuts 
06/03/2012 - 1.07.1202
- Disable brightness if preset mode is Movie or Game
05/03/2012 - 1.07.1201
- Fixed minimum contrast level to 25
04/03/2012 - 1.07.1200
- Improved auto-closing of image spinedit
- Improved window/monitor/preset tracking
- Auto-mode now always reverts to Standard preset
- Improved support for clone mode
- Extended delay before rediscovery
- Restore refresh rate on change in orientation
29/02/2012 - 1.07.1190
- Revised UI for UI-V2
29/02/2012 - 1.06.1188
- Added additional app filters 
- Hard coded initial manual mode preset
- Enforced preferred refresh rate on screen rotation
19/02/2012 - 1.06.1182
- Fixed relocation
- Implemented application sort
- Excluded LVDS from discovery
- Fixed Snap/mirroring issue
17/02/2012 - 1.06.1177
- Changed auto preset mechanism 
- Improved support for clone/duplicate displays 
14/02/2012 - 1.06.1170
- Fixed overlapping overlays
- Fixed preset sync error with multiple monitors
- Added capture for duplicate/extend transitions 
13/02/2012 - 1.06.1166
- Fixed PS/2 kbd issue
- Added alternate kbd hook
- Added mirroring workaround
12/02/2012 - 1.06.1161
- Rewrote hooks
- Fixed preset sync issues
10/02/2012 - 1.05.1126
- Patched around MCI issue with early FY13 firmware
07/02/2012 - 1.05.1125
- Fixed ansi-unicode conversion issue
- Reenabled drag and drop
- Added machine localizations (rename ddm.da_ to ddm.dat)
01/02/2012 - 1.05.1120
- Unicode version
- Adjusted polling frequencies
- Streamlined bug reporting, added screenshot
- Reduced size of notification font
- Added trap for app list errors
29/01/2012 - 1.04.1100
- Removed Dell Snap
- Fixed resolution label
22/01/2012 - 1.04.1098
- Added Win7 Snap disable if Dell Zone enabled
- Fixed image level spin controls
- Fixed DWM issue with overlays
- restricted zoning to windows with Min+Max buttons
- relativized custom zone coordinates
18/01/2012 - 1.04.1064
- Sorted application list
- Removed support for LVDS
- Added overlay preset notifications
16/01/2012 - 1.04.1060
- Posted to demonstrate live update
- Added 7 additional predefined screen layouts
15/01/2012 - 1.04.1047
- Revised in accordance with UXg again
- Added auto-Game mode option for D3D
- Added system scan for predefined apps
02/01/2012 - 1.04.993
- Revised in accordance with UXg
16/12/2011 - 1.03.974
- Internal release w. grids and virtual desktop
12/11/2011 - 1.03.952
- Reposted to illustrate live update
- Enabled localized strings
10/11/2011 - 1.03.950
- Initial descendant/preview
   