------------------------------------------
  BIP Catalog Utility
------------------------------------------
Last Update: December 31, 2013

[BI Publisher Catalog Utility Download Link]

http://xmlp.us.oracle.com/syoshida/BIPCatalogUtil.zip

[Setup]

[Linux]
1) Login to your hosted linux env and unzip BIPCatalogUtil.zip in Home directory.

$ cd $HOME

$ unzip BIPCatalogUtil.zip

$ ls -F BIPCatalogUtil
Readme.txt bin/  config/  lib/

2) set environment variables for BIPCatalogUtil.
C-shell example:
% set path = ($HOME/BIPCatalogUtil/bin $path)
% setenv BIP_LIB_DIR $HOME/BIPCatalogUtil/lib
% setenv BIP_CLIENT_CONFIG $HOME/BIPCatalogUtil/config

% echo $BIP_LIB_DIR $BIP_CLIENT_CONFIG
/home/syoshida/BIPCatalogUtil/lib /home/syoshida/BIPCatalogUtil/config

% setenv JAVA_HOME $HOME/java/jdk1.6.0_18
% echo $JAVA_HOME
/home/syoshida/java/jdk1.6.0_18

Bash example:
$ export PATH=$HOME/BIPCatalogUtil/bin:$PATH
$ export BIP_LIB_DIR=$HOME/BIPCatalogUtil/lib
$ export BIP_CLIENT_CONFIG=$HOME/BIPCatalogUtil/config
$ export JAVA_HOME $HOME/java/jdk1.6.0_18


[Windows]
1) Unzip BIPCatalogUtil.zip
   The zip file will unzip to Readme.txt \bin \config \lib

2) set environment variables for BIPCatalogUtil.
set BIP_LIB_DIR={BIP_CATALOG_UTIL_DIR}\lib
set BIP_CLIENT_CONFIG={BIP_CATALOG_UTIL_DIR}\config


[Linux and Windows]

3) Edit BIP_CLIENT_CONFIG/xmlp-client-config.xml

set your bip instance URL, username and password.

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
        <comment>BIP Server Information</comment>
    <entry key="bipuri">http://sta00XXX.us.oracle.com:14001/xmlpserver/</entry>
        <entry key="username">OPERATIONS</entry>
    <entry key="password">welcome</entry>
</properties>

3) Run a BIPCatalogUtil command
   Note:  For Linux use BIPCatalogUtil.sh 
         For windows use BIPCatalogUtil.cmd

$ BIPCatalogUtil.sh  -listfolder catalogpath=/Samples subfolders=true

Connect to http://sta00XXX.us.oracle.com:14001/xmlpserver/ using OPERATIONS
Folder: /Samples/bursting
Report: /Samples/bursting/Bursting Example_Burst to Email.xdo
DataModel: /Samples/bursting/Employee Salary Report Datamodel.xdm
Folder: /Samples/Data Models
DataModel: /Samples/Data Models/Balance Letter Datamodel.xdm
DataModel: /Samples/Data Models/Check Printing Datamodel.xdm
DataModel: /Samples/Data Models/Customer Profile Datamodel.xdm
DataModel: /Samples/Data Models/Departmental Expenses Datamodel.xdm
DataModel: /Samples/Data Models/Discrete Job Data Report Datamodel.xdm
DataModel: /Samples/Data Models/Invoice Batch Report Datamodel.xdm
DataModel: /Samples/Data Models/North America Sales Datamodel  old.xdm
DataModel: /Samples/Data Models/North America Sales Datamodel.xdm
DataModel: /Samples/Data Models/Order Entry Data Model.xdm
DataModel: /Samples/Data Models/P11D Datamodel.xdm
DataModel: /Samples/Data Models/Price List Datamodel.xdm
DataModel: /Samples/Data Models/Purchase Order Datamodel.xdm
DataModel: /Samples/Data Models/Quarterly Income Statement Datamodel.xdm
......


[Command Samples]

Please use overwrite=true option for all commands if necessary. Existing files or BIP objects are overwritten with new files and objects by the tool with this mode.

1) Simple Download

Download a report from BIP server without extracting individual files

$ BIPCatalogUtil.sh -export catalogpath=/Samples/Financials/Balance+Letter.xdo target=/home/syoshida/bipub/reports/BalanceLetter.xdoz extract=false

2) Download with file extractions

Download a report from BIP server and extract individual files with name conversion for source control

$ BIPCatalogUtil.sh -export catalogpath=/Samples/Financials/Balance+Letter.xdo target=/home/syoshida/bipub/reports/BalanceLetter extract=true mode=fusionapps

3) Download Folder Contents

Download BIP contents in a selected catalog folder. Contents from subfolders are extracted, too
Data models are saved into {basedir}/datamodels. Reports are saved into {basedir}/reports. Style and Sub templates are saved into {basedir}/templates

$ BIPCatalogUtil.sh -exportfolder catalogpath=/Samples basedir=/Users/syoshida//home/syoshida/bipub/ subfolders=true extract=true mode=fusionapps

4) List Folder Contents

$ BIPCatalogUtil.sh -listfolder catalogpath=/Samples subfolders=true

5) Upload a report from directory 

Upload a report to a catalog path saved in meta file (original catalog path). Overwrite existing report if it exists.

$ BIPCatalogUtil.sh -import source=/home/syoshida/bipub/reports/BalanceLetter mode=fusionapps 


6) Upload a report with a new catalog path

$ BIPCatalogUtil.sh -import source=/home/syoshida/bipub/reports/BalanceLetter catalogpath=/Production/Financials/Balance+Letter+Report.xdo mode=fusionapps

7) Upload a report from xdoz/xdmz

Upload selected object to a catalog path saved in meta file in the zip. Add catalogpath option to upload to a different location.

$ BIPCatalogUtil.sh -import source=/home/syoshida/bipub/reports/BalanceLetter.xdoz  mode=fusionapps

8) Upload all bip objects from a selected local folder

$ BIPCatalogUtil.sh -import basedir=/Users/syoshidabipub subfolders=true  mode=fusionapps

9) Unzip .xdo/.xdm

$ BIPCatalogUtil.sh -unzip source=/home/syoshida/bipub/reports/Balance+Letter.xdoz target=/user/syoshida/bipub/reports/Balance+Letter catalogpath=/Samples/Financials/Balance+Letter mode=fusionapps

10) Zip exported BIP report files

$ BIPCatalogUtil.sh -zip source=/user/syoshida/bipub/reports/Balance+Letter/BalanceLetterTemplate.rtf target=/usr/syoshida/bipub/reports/BalanceLetter mode=fusionapps

11) Extract XLIFF from report definition file (.xdo). 

$ BIPCatalogUtil.sh -xliff source=/home/syoshida/bipub/reports/Balance+Letter/Balance+Letter.xdo target=/home/syoshida/bipub/reports/Balance+Letter/Balance+Letter.xlf

or 

$ BIPCatalogUtil.sh -xliff source=/home/syoshida/bipub/reports/Balance/Balance+Letter.xdo basedir=/home/syoshida/bipub/reports/Balance+Letter/


12) Extract XLIFF from rtf template

$ BIPCatalogUtil.sh -xliff source=/home/syoshida/bipub/reports/Balance+Letter/Balance+Letter+Template.rtf target=/home/syoshida/bipub/reports/Balance+Letter/Balance+Letter+Template.xlf

or 

$ BIPCatalogUtil.sh -xliff source=/home/syoshida/bipub/reports/Balance/Balance+Letter+Template.rtf basedir=/home/syoshida/bipub/reports/Balance+Letter/


You can also set bipuri, username, password in command line to overwrite values defined in xmlp-client-config.xml
