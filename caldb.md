---
title: How to download and install CALDB
abbrlink: 7c4f43c4
date: 2022-09-01 12:13:59
tags:
  - HEASoft
  - HEASARC
  - CALDB
categories:
  - Linux
  - Bash
  - HEASARC
  - HEASoft
cover: https://s2.loli.net/2022/09/16/fp4ObzMH6qjU2k8.jpg
---
# 1  Introduction
CALDB is the High Energy Astrophysics Science Archive Research Center (HEASARC) Calibration Database. The CALDB is integrated with the [HEAsoft](https://heasarc.gsfc.nasa.gov/docs/software/lheasoft/) software package in that the HEAsoft tasks can access appropriate calibration data from the CALDB with little input from the user.There are two installation methods,Local access, remote access! 

# 2 Setting up the `CALDB` Environment
Define the environment variable $CALDB to point to the directory where the calibration data will be located (we'll call this the top-level CALDB directory). For example, if the CALDB is being installed under the directory /path/to/install/caldb you need to define the $CALDB environment variable as:
```bash
export CALDB=/path/to/install/caldb
export CALDB
```
## 2.1  Downloading and Installing CALDB setup files
Change your current working directory to $CALDB and download the file https://heasarc.gsfc.nasa.gov/FTP/caldb/software/tools/caldb_setup_files.tar.Z
either using your web browser or using a download utility like [wget](http://wget.sunsite.dk/) or [curl](https://curl.se/). Then uncompress and untar the file in your $CALDB directory. For example:
```bash
$ cd $CALDB
$ wget https://heasarc.gsfc.nasa.gov/FTP/caldb/software/tools/caldb_setup_files.tar.Z
--2022-09-16 13:11:40--  https://heasarc.gsfc.nasa.gov/FTP/caldb/software/tools/caldb_setup_files.tar.Z
Resolving heasarc.gsfc.nasa.gov (heasarc.gsfc.nasa.gov)... 129.164.179.23, 2001:4d0:2310:150::23
Connecting to heasarc.gsfc.nasa.gov (heasarc.gsfc.nasa.gov)|129.164.179.23|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7974 (7.8K) [application/x-tar]
Saving to: ‘caldb_setup_files.tar.Z’

caldb_setup_files.tar.Z       100%[=================================================>]   7.79K  --.-KB/s    in 0.001s

2022-09-16 13:11:42 (5.88 MB/s) - ‘caldb_setup_files.tar.Z’ saved [7974/7974]

$ tar -zxvf caldb_setup_files.tar.Z 
```
This will create two $CALDB configuration files, which are:
```bash
$CALDB/software/tools/alias_config.fits
$CALDB/software/tools/caldb.config
```
# 3 Setup CALDB
Open the initialization file `caldbinit.sh` in an editor (`vim` for example). Edit the definition of the `$CALDB` environment variable to your `CALDB` directory like text below.
```bash
CALDBCONFIG=$CALDB/software/tools/caldb.config
export CALDBCONFIG
CALDBALIAS=$CALDB/software/tools/alias_config.fits
export CALDBALIAS
```
# Download Calibration Data from the HEASARC
You should download the caldb for any instrument in the $CALDB directory – for example
```bash
$ cd $CALDB

$ pwd

/path/to/caldb

$ wget https://heasarc.gsfc.nasa.gov/FTP/caldb/data/nicer/xti/goodfiles_nicer_xti_20210707.tar.gz

$ tar -zxvf goodfiles_nicer_xti_20210707.tar.gz
```
 to install the nicer caldb in your $CALDB directory
```bash
$ caldbinfo INST nustar fpm

 ...  using gpcaldbinfo 1.0.0
 ** caldbinfo 1.0.2
 ...  using infocaldb   1.0.1
 ...... environ-var/logical CALDB defined
 .........   CALDB path = /home/Jisans/workspace/caldb
 ... environ-var/logical CALDBCONFIG defined
 ...   CALDBCONFIG file = /home/Jisans/workspace/caldb/software/tools/caldb.config
 ...... environ-var/logical CALDBALIAS defined
 .........   CALDBALIAS file = /home/Jisans/workspace/caldb/software/tools/alias_c
           onfig.fits
 ...... CALDB is configured for the FPM instrument onboard NUSTAR
 ......... Cal Index File: /home/Jisans/workspace/caldb/data/nustar/fpm/caldb.indx
 ......... Instrument directory: /home/Jisans/workspace/caldb/data/nustar/fpm
 ... CALDB appears to be set-up & accessible
 ** caldbinfo 1.0.2 completed successfully

```

# 4 Accessing the HEASARC CALDB Remotely
To enable Remote Access:
1.download the file
https://heasarc.gsfc.nasa.gov/FTP/caldb/software/tools/caldb.config

and set the environment $CALDBCONFIG to point to that file. For example if you download the file to /path/to/caldb.config, then
,if you're using the bash shell:
```bash
$ CALDBCONFIG=/path/to/caldb.config
  export CALDBCONFIG
```

download the file https://heasarc.gsfc.nasa.gov/FTP/caldb/software/tools/alias_config.fits and set the environment variable $CALDBALIAS to point to that file. For example, if you download the file to /local/user/alias_config.fits, then
,for bash shell users:
```bash
$ CALDBALIAS=/path/to/alias_config.fits
  export CALDBALIAS
```
set the environment variable $CALDB to https://heasarc.gsfc.nasa.gov/FTP/caldb
,for bash shell users:
```bash
$ CALDB=https://heasarc.gsfc.nasa.gov/FTP/caldb
  export CALDB
```
The installation is successful!