# Volatility Guide

## **CONTENTS**
* [**Introduction**](#introduction)
* [**Installation**](#installation)
* [**Options**](#options)
* [**Plugins**](#plugins)
* [**References**](#references)


## Introduction
Volatility is a free memory forensics tool developed and maintained by Volatility labs. Regarded as the gold standard for memory forensics in incident response, Volatility is wildly expandable via a plugins system and is an invaluable tool for any Blue Teamer. There is some file support to analyzed by volatility :  
* VMware      - .vmem file
* Hyper-V     - .bin file
* Parallels   - .mem file
* VirtualBox  - .sav file 

## Installation
First, download the file at https://www.volatilityfoundation.org/releases , in this tutorial I use Linux, **then rename the file to volatility** (your program is run depend on your name file)
```
./volatility.exe --help
```

## Options

## Plugins
* **imageinfo** : Identify information for the image  
```
./volatility.exe -f [file name.extension] imageinfo
```
```
┌──(root💀DESKTOP-VE2NGI6)-[/mnt/d]
└─# ./volatility.exe -f example.vmem imageinfo
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_23418
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (D:\example.vmem)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf80002c2f120L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff80002c31000L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2021-08-29 09:14:18 UTC+0000
     Image local date and time : 2021-08-29 16:14:18 +0700
```

* **pslist** : Print all running processes by following the EPROCESS lists  
```
./volatility.exe -f [nama file.format] --profile=[profil name] pslist
```
```
┌──(root💀DESKTOP-VE2NGI6)-[/mnt/d]
└─# ./volatility.exe -f example.vmem --profile=Win7SP1x64 pslist
Volatility Foundation Volatility Framework 2.6
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa8018dc3040 System                    4      0     71      508 ------      0 2021-08-29 09:12:31 UTC+0000
0xfffffa8024fb7610 smss.exe                220      4      2       29 ------      0 2021-08-29 09:12:31 UTC+0000
0xfffffa801aa29060 csrss.exe               288    280      8      427      0      0 2021-08-29 09:12:32 UTC+0000
0xfffffa8018dc9790 wininit.exe             336    280      3       76      0      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801a264b00 csrss.exe               348    328      9      585      1      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801aa77b00 winlogon.exe            388    328      5      113      1      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801aaa95c0 services.exe            432    336      9      182      0      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801aab26d0 lsass.exe               440    336      8      722      0      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801aaab500 lsm.exe                 448    336     10      142      0      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801ab678d0 svchost.exe             552    432     11      368      0      0 2021-08-29 09:12:33 UTC+0000
0xfffffa801aba7b00 svchost.exe             620    432      7      262      0      0 2021-08-29 09:12:34 UTC+0000
0xfffffa801abd3b00 svchost.exe             672    432     20      416      0      0 2021-08-29 09:12:34 UTC+0000
0xfffffa801ac56b00 svchost.exe             776    432     24      448      0      0 2021-08-29 09:12:34 UTC+0000
0xfffffa801ac8eb00 svchost.exe             828    432     93      498      0      0 2021-08-29 09:12:34 UTC+0000
0xfffffa801aca6b00 svchost.exe             872    432     36      765      0      0 2021-08-29 09:12:34 UTC+0000
0xfffffa801acea700 audiodg.exe             924    672      5      123      0      0 2021-08-29 09:12:35 UTC+0000
0xfffffa801ad0fb00 svchost.exe             296    432     39      479      0      0 2021-08-29 09:12:35 UTC+0000
0xfffffa801ab81060 spoolsv.exe             824    432     15      273      0      0 2021-08-29 09:12:36 UTC+0000
0xfffffa801ac95060 svchost.exe            1088    432     19      321      0      0 2021-08-29 09:12:36 UTC+0000
0xfffffa801ab83060 taskhost.exe           1128    432     11      216      1      0 2021-08-29 09:12:36 UTC+0000
0xfffffa801ae13060 svchost.exe            1360    432     10      147      0      0 2021-08-29 09:12:37 UTC+0000
0xfffffa801aef4b00 sppsvc.exe             1628    432      5      146      0      0 2021-08-29 09:12:39 UTC+0000
0xfffffa801af139d0 svchost.exe            1684    432      6       95      0      0 2021-08-29 09:12:39 UTC+0000
0xfffffa801adecb00 dwm.exe                1204    776      5       79      1      0 2021-08-29 09:12:48 UTC+0000
0xfffffa801afa7b00 explorer.exe           1292   1248     37      732      1      0 2021-08-29 09:12:48 UTC+0000
0xfffffa801af83b00 SearchIndexer.         2036    432     12      606      0      0 2021-08-29 09:12:55 UTC+0000
0xfffffa801b09a430 SearchProtocol         1896   2036      6      275      0      0 2021-08-29 09:12:56 UTC+0000
0xfffffa801afcdb00 SearchFilterHo         1200   2036      4       92      0      0 2021-08-29 09:12:56 UTC+0000
0xfffffa8019ee6670 firefox.exe            1060   1048     74      906      1      1 2021-08-29 09:13:16 UTC+0000
0xfffffa801b1f1490 firefox.exe            2144   1060     25      289      1      1 2021-08-29 09:13:18 UTC+0000
0xfffffa801b29f060 firefox.exe            2300   1060     23      310      1      1 2021-08-29 09:13:19 UTC+0000
0xfffffa8019ee4060 firefox.exe            2440   1060     23      307      1      1 2021-08-29 09:13:20 UTC+0000
0xfffffa801b248060 firefox.exe            2488   1060     22      309      1      1 2021-08-29 09:13:21 UTC+0000
0xfffffa801b3d05f0 firefox.exe            2820   1060     23      326      1      1 2021-08-29 09:13:24 UTC+0000
0xfffffa801b320060 firefox.exe            2828   1060      0 --------      1      0 2021-08-29 09:13:24 UTC+0000   2021-08-29 09:13:25 UTC+0000
0xfffffa801b32a060 firefox.exe            3020   1060     20      287      1      1 2021-08-29 09:13:26 UTC+0000
0xfffffa801afe3060 iexplore.exe           3048   1292     19      607      1      0 2021-08-29 09:13:29 UTC+0000
0xfffffa8018e41b00 iexplore.exe           2832   3048    102     1087      1      1 2021-08-29 09:13:31 UTC+0000
0xfffffa801a11c320 iexplore.exe           2508   3048     80      923      1      1 2021-08-29 09:13:37 UTC+0000
0xfffffa80255fab00 iexplore.exe           3080   3048     35      605      1      1 2021-08-29 09:13:37 UTC+0000
0xfffffa80271fd320 iexplore.exe           3088   3048     38      643      1      1 2021-08-29 09:13:37 UTC+0000
```

* **pstree** : Print process list as a tree
```
./volatility.exe -f [nama file.format] --profile=[profil name] pstree
```
```
┌──(root💀DESKTOP-VE2NGI6)-[/mnt/d]
└─# ./volatility.exe -f example.vmem --profile=Win7SP1x64 pstree
Volatility Foundation Volatility Framework 2.6
Name                                                  Pid   PPid   Thds   Hnds Time
-------------------------------------------------- ------ ------ ------ ------ ----
 0xfffffa801aa29060:csrss.exe                         288    280      8    427 2021-08-29 09:12:32 UTC+0000
 0xfffffa8018dc9790:wininit.exe                       336    280      3     76 2021-08-29 09:12:33 UTC+0000
. 0xfffffa801aaab500:lsm.exe                          448    336     10    142 2021-08-29 09:12:33 UTC+0000
. 0xfffffa801aaa95c0:services.exe                     432    336      9    182 2021-08-29 09:12:33 UTC+0000
.. 0xfffffa801ac56b00:svchost.exe                     776    432     24    448 2021-08-29 09:12:34 UTC+0000
... 0xfffffa801adecb00:dwm.exe                       1204    776      5     79 2021-08-29 09:12:48 UTC+0000
.. 0xfffffa801af139d0:svchost.exe                    1684    432      6     95 2021-08-29 09:12:39 UTC+0000
.. 0xfffffa801ab678d0:svchost.exe                     552    432     11    368 2021-08-29 09:12:33 UTC+0000
.. 0xfffffa801ab81060:spoolsv.exe                     824    432     15    273 2021-08-29 09:12:36 UTC+0000
.. 0xfffffa801ac8eb00:svchost.exe                     828    432     93    498 2021-08-29 09:12:34 UTC+0000
.. 0xfffffa801ad0fb00:svchost.exe                     296    432     39    479 2021-08-29 09:12:35 UTC+0000
.. 0xfffffa801ac95060:svchost.exe                    1088    432     19    321 2021-08-29 09:12:36 UTC+0000
.. 0xfffffa801abd3b00:svchost.exe                     672    432     20    416 2021-08-29 09:12:34 UTC+0000
... 0xfffffa801acea700:audiodg.exe                    924    672      5    123 2021-08-29 09:12:35 UTC+0000
.. 0xfffffa801aef4b00:sppsvc.exe                     1628    432      5    146 2021-08-29 09:12:39 UTC+0000
.. 0xfffffa801ae13060:svchost.exe                    1360    432     10    147 2021-08-29 09:12:37 UTC+0000
.. 0xfffffa801ab83060:taskhost.exe                   1128    432     11    216 2021-08-29 09:12:36 UTC+0000
.. 0xfffffa801aba7b00:svchost.exe                     620    432      7    262 2021-08-29 09:12:34 UTC+0000
.. 0xfffffa801aca6b00:svchost.exe                     872    432     36    765 2021-08-29 09:12:34 UTC+0000
.. 0xfffffa801af83b00:SearchIndexer.                 2036    432     12    606 2021-08-29 09:12:55 UTC+0000
... 0xfffffa801afcdb00:SearchFilterHo                1200   2036      4     92 2021-08-29 09:12:56 UTC+0000
... 0xfffffa801b09a430:SearchProtocol                1896   2036      6    275 2021-08-29 09:12:56 UTC+0000
. 0xfffffa801aab26d0:lsass.exe                        440    336      8    722 2021-08-29 09:12:33 UTC+0000
 0xfffffa801aa77b00:winlogon.exe                      388    328      5    113 2021-08-29 09:12:33 UTC+0000
 0xfffffa801a264b00:csrss.exe                         348    328      9    585 2021-08-29 09:12:33 UTC+0000
 0xfffffa801afa7b00:explorer.exe                     1292   1248     37    732 2021-08-29 09:12:48 UTC+0000
. 0xfffffa801afe3060:iexplore.exe                    3048   1292     19    607 2021-08-29 09:13:29 UTC+0000
.. 0xfffffa8018e41b00:iexplore.exe                   2832   3048    102   1087 2021-08-29 09:13:31 UTC+0000
.. 0xfffffa801a11c320:iexplore.exe                   2508   3048     80    923 2021-08-29 09:13:37 UTC+0000
.. 0xfffffa80255fab00:iexplore.exe                   3080   3048     35    605 2021-08-29 09:13:37 UTC+0000
.. 0xfffffa80271fd320:iexplore.exe                   3088   3048     38    643 2021-08-29 09:13:37 UTC+0000
 0xfffffa8018dc3040:System                              4      0     71    508 2021-08-29 09:12:31 UTC+0000
. 0xfffffa8024fb7610:smss.exe                         220      4      2     29 2021-08-29 09:12:31 UTC+0000
 0xfffffa8019ee6670:firefox.exe                      1060   1048     74    906 2021-08-29 09:13:16 UTC+0000
. 0xfffffa8019ee4060:firefox.exe                     2440   1060     23    307 2021-08-29 09:13:20 UTC+0000
. 0xfffffa801b320060:firefox.exe                     2828   1060      0 ------ 2021-08-29 09:13:24 UTC+0000
. 0xfffffa801b32a060:firefox.exe                     3020   1060     20    287 2021-08-29 09:13:26 UTC+0000
. 0xfffffa801b3d05f0:firefox.exe                     2820   1060     23    326 2021-08-29 09:13:24 UTC+0000
. 0xfffffa801b1f1490:firefox.exe                     2144   1060     25    289 2021-08-29 09:13:18 UTC+0000
. 0xfffffa801b248060:firefox.exe                     2488   1060     22    309 2021-08-29 09:13:21 UTC+0000
. 0xfffffa801b29f060:firefox.exe                     2300   1060     23    310 2021-08-29 09:13:19 UTC+0000
```
* **psscan** : Pool scanner for process objects
```
./volatility.exe -f [nama file.format] --profile=[profil name] psscan
```
```
┌──(root💀DESKTOP-VE2NGI6)-[/mnt/d]
└─# ./volatility.exe -f example.vmem --profile=Win7SP1x64 psscan
Volatility Foundation Volatility Framework 2.6
Offset(P)          Name                PID   PPID PDB                Time created                   Time exited
------------------ ---------------- ------ ------ ------------------ ------------------------------ ------------------------------

NULL (┬┬﹏┬┬)
It means that there are no processes that have previously been terminated (inactive) and no processes that have been hidden or unlinked by a rootkit.
```
* **psxview** : Find hidden processes with various process listings
```
./volatility.exe -f [nama file.format] --profile=[profil name] psxview
```
```
┌──(root💀DESKTOP-VE2NGI6)-[/mnt/d]
└─# ./volatility.exe -f example.vmem --profile=Win7SP1x64 psxview
Volatility Foundation Volatility Framework 2.6
Offset(P)          Name                    PID pslist psscan thrdproc pspcid csrss session deskthrd ExitTime
------------------ -------------------- ------ ------ ------ -------- ------ ----- ------- -------- --------
0x000000007e1d3b00 svchost.exe             672 True   False  False    True   True  True    True
0x000000007de8eb00 svchost.exe             828 True   False  False    True   True  True    True
0x000000007dfecb00 dwm.exe                1204 True   False  False    True   True  True    True
0x000000007dbf1490 firefox.exe            2144 True   False  False    True   True  True    True
0x000000007ddcdb00 SearchFilterHo         1200 True   False  False    True   True  True    True
0x000000007d848060 firefox.exe            2488 True   False  False    True   True  True    True
0x000000007fe46790 wininit.exe             336 True   False  False    True   True  True    True
0x000000007ece4060 firefox.exe            2440 True   False  False    True   True  True    True
0x000000007df0fb00 svchost.exe             296 True   False  False    True   True  True    True
0x000000007d92a060 firefox.exe            3020 True   False  False    True   True  True    True
0x000000007e0b26d0 lsass.exe               440 True   False  False    True   True  True    False
0x000000007eb1c320 iexplore.exe           2508 True   False  False    True   True  True    True
0x000000007d9d05f0 firefox.exe            2820 True   False  False    True   True  True    True
0x000000007dcf4b00 sppsvc.exe             1628 True   False  False    True   True  True    True
0x000000007e0ab500 lsm.exe                 448 True   False  False    True   True  True    False
0x000000007da9a430 SearchProtocol         1896 True   False  False    True   True  True    True
0x000000007de56b00 svchost.exe             776 True   False  False    True   True  True    True
0x000000007e077b00 winlogon.exe            388 True   False  False    True   True  True    True
0x000000007dc13060 svchost.exe            1360 True   False  False    True   True  True    True
0x000000007deea700 audiodg.exe             924 True   False  False    True   True  True    True
0x000000007e0a95c0 services.exe            432 True   False  False    True   True  True    False
0x000000007e181060 spoolsv.exe             824 True   False  False    True   True  True    True
0x000000007e183060 taskhost.exe           1128 True   False  False    True   True  True    True
0x000000007e1678d0 svchost.exe             552 True   False  False    True   True  True    True
0x000000007fc41b00 iexplore.exe           2832 True   False  False    True   True  True    True
0x000000007dea6b00 svchost.exe             872 True   False  False    True   True  True    True
0x00000000202ba320 iexplore.exe           3088 True   False  False    True   True  True    True
0x000000007de95060 svchost.exe            1088 True   False  False    True   True  True    True
0x000000007dd139d0 svchost.exe            1684 True   False  False    True   True  True    True
0x000000007dd83b00 SearchIndexer.         2036 True   False  False    True   True  True    True
0x000000007d89f060 firefox.exe            2300 True   False  False    True   True  True    True
0x000000007ece6670 firefox.exe            1060 True   False  False    True   True  True    True
0x000000007e1a7b00 svchost.exe             620 True   False  False    True   True  True    True
0x00000000221adb00 iexplore.exe           3080 True   False  False    True   True  True    True
0x000000007dde3060 iexplore.exe           3048 True   False  False    True   True  True    True
0x000000007dda7b00 explorer.exe           1292 True   False  False    True   True  True    True
0x000000007fe40040 System                    4 True   False  False    True   False False   False
0x000000007e029060 csrss.exe               288 True   False  False    True   False True    True
0x00000000226e3610 smss.exe                220 True   False  False    True   False False   False
0x000000007e864b00 csrss.exe               348 True   False  False    True   False True    True
0x000000007d920060 firefox.exe            2828 True   False  False    True   False True    False    2021-08-29 09:13:25 UTC+0000
```
* **dlllist** : Print list of loaded dlls for each process
```
./volatility.exe -f [nama file.format] --profile=[profil name] dlllist
```
```
┌──(root💀DESKTOP-VE2NGI6)-[/mnt/d]
└─# ./volatility.exe -f example.vmem --profile=Win7SP1x64 dlllist
Volatility Foundation Volatility Framework 2.6
************************************************************************
System pid:      4
Unable to read PEB for task.
************************************************************************
smss.exe pid:    220
Command line : \SystemRoot\System32\smss.exe


Base                             Size          LoadCount Path
------------------ ------------------ ------------------ ----
0x0000000047b40000            0x20000             0xffff \SystemRoot\System32\smss.exe
0x0000000076ee0000           0x19f000             0xffff C:\Windows\SYSTEM32\ntdll.dll
************************************************************************
csrss.exe pid:    288
Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,20480,768 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDl
l=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
Service Pack 1

Base                             Size          LoadCount Path
------------------ ------------------ ------------------ ----
0x0000000049720000             0x6000             0xffff C:\Windows\system32\csrss.exe
0x0000000076ee0000           0x19f000             0xffff C:\Windows\SYSTEM32\ntdll.dll
0x000007fefca60000            0x13000             0xffff C:\Windows\system32\CSRSRV.dll
0x000007fefca40000            0x11000                0x4 C:\Windows\system32\basesrv.DLL
0x000007fefca00000            0x39000                0x2 C:\Windows\system32\winsrv.DLL
0x0000000076de0000            0xfa000                0xb C:\Windows\system32\USER32.dll
0x000007fefec30000            0x67000                0xc C:\Windows\system32\GDI32.dll
0x0000000076cc0000           0x11f000               0x44 C:\Windows\SYSTEM32\kernel32.dll
0x000007fefcdd0000            0x6a000               0xdb C:\Windows\system32\KERNELBASE.dll
0x000007fefee80000             0xe000                0x3 C:\Windows\system32\LPK.dll
0x000007fefd0e0000            0xcb000                0x3 C:\Windows\system32\USP10.dll
0x000007feff0b0000            0x9f000                0x3 C:\Windows\system32\msvcrt.dll
0x000007fefc9f0000             0xc000                0x1 C:\Windows\system32\sxssrv.DLL
0x000007fefc8f0000            0x91000                0x1 C:\Windows\system32\sxs.dll
0x000007fefee90000           0x12d000                0x1 C:\Windows\system32\RPCRT4.dll
0x000007fefc8e0000             0xf000                0x1 C:\Windows\system32\CRYPTBASE.dll
************************************************************************
wininit.exe pid:    336
Command line : wininit.exe
Service Pack 1

...
```
## References
https://tryhackme.com/room/bpvolatility  
https://www.andreafortuna.org/2017/07/03/volatility-my-own-cheatsheet-part-2-processes-and-dlls/  
https://github.com/volatilityfoundation/volatility/wiki/Command-Reference  
