Building an installation file, MSI, can simplify deployment of Sysmon to a network. The following instructions aim to achieve this, but testing and any required modifications should be done before a domain-wide deployment.

Prerequisites:
    This folder, events/sysmon/msi contains the WiX configuration file (Sysmon.wxs).
    Download and install the WIX Toolset from http://wixtoolset.org/. (instructions have been tested with WiX 3.11).
    Download Sysmon from https://technet.microsoft.com/en-au/sysinternals/sysmon (Instructions have been tested for 6.03), and place Sysmon.exe and Eula.txt in the existing msi directory.
    Read and accept terms of the Sysmon end user license agreement (EULA) - contained in Eula.txt.
    The configuration file sysmon_config.xml is placed in the msi folder (from events/sysmon/sysmon_config.xml). This file can optionally be edited to tweak which events are captured. Also, instructions are contained at the top of this file to reduce the event volume while still capturing most of the valuable events.

Building the MSI

To build the MSI, follow these steps:
    Ensure the MSI folder, contains, Sysmon.wxs, sysmon_config.xml, Eula.txt, and Sysmon.exe.
    Open command prompt (click start menu, type cmd, press enter)
    cd to the msi directory
    Build the intermediate file by typing C:\Program Files (x86)\WiX Toolset v3.11\bin\candle.exe Sysmon.wxs (Version number may need to be updated).
    Build the MSI file by typing C:\Program Files (x86)\WiX Toolset v3.11\bin\light.exe Sysmon.wixobj (Version number may need to be updated).
    On a test machine, double click on the created MSI file to verify it installs correctly.
    On the same test machine, check logs are being generated by Sysmon, open Event Viewer (eventvwr.msc), and navigate to Applications and Services Logs / Microsoft / Windows / Sysmon / Operational. There should be a number of log events generated already.

To update the configuration or Sysmon version, repeat the same instructions with an updated config file or Sysmon version. The installation file should remove the old version and install the updated version automatically.
