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
![image](https://user-images.githubusercontent.com/55046884/134541253-f544899c-6e33-4ab2-8449-0693f4484e97.png)  

* **pslist** : Print all running processes by following the EPROCESS lists  
```
./volatility.exe -f [nama file.format] --profile=[profil name] pslist
```
![image](https://user-images.githubusercontent.com/55046884/134541810-cb67f13d-ebe5-414c-91a7-b2e948c1180c.png)

## References
https://tryhackme.com/room/bpvolatility
