@echo off
echo AFHS cyberpatriot A team Batch script
pause
echo disclamer: This script is in alpha stages please go through and mannualy check the changes mannualy to make sure everything is fine and working
pause
echo if you didnt run this script with admin privleges please close and restart the program elevated
pause
echo if a error appears and the script doesn't work abandon the script close it and continue mannualy
pause
echo again this script has never been fully tested use at your own risk
pause
echo the script will now execute are you ready?
pause

echo executing cyber patriot script...

::enables automatic updates
echo setting windows update to download automatically...
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update" /v AUOptions /t REG_DWORD /d 3 /f
echo remember you need to install any updates mannualy (do that near the end) 
pause

::disables guest account
echo disabling guest account...
net user guest /active:no
echo guest account disabled
pause

REM ::removing unauthorized users 
REM echo below are all the users currently on the machine
REM net localgroup Users
REM echo take note of users and compare to list of authorized users
REM pause
REM echo you will asked how many users you wold like to delete then thosse users will be entered in
REM set /p loopcount="Enter amount of users you would like to delete (if there is none enter 0): "
REM pause
REM set /a loopcount=loopcount-1
REM if %loopcount%==-1 goto exitloop
REM :loop
REM set /p deaduser="what user would you like to delete: "
REM net localgroup Users %deaduser% /delete
REM if errorlevel 1 echo Unsuccessful
REM goto loop
REM :exitloop
REM pause

REM ::remove unauthorized administrators
REM net localgroup administrators
REM echo compare list of administrators to authorized administrators on the readme
REM et /p loopcount1="Enter amount of admins you would like to remove (if there is none enter 0): "
REM pause
REM set /a loopcount1=loopcount1-1
REM if %loopcount1%==-1 goto exitloop
REM :loop1
REM set /p deadadmin="what admin would you like to remove: "
REM net localgroup Administrators %deadadmin% /delete
REM if errorlevel 1 echo Unsuccessful
REM goto loop1
REM :exitloop1
REM pause

REM echo make sure to remove any users from groups explicitly stated in the readme
REM pause

:: changes password policies
echo changing password policy...
::this will change the minimum length of the password
net accounts /minpwlen:10
if errorlevel 1 echo Unsuccessful
::this will change the maximum age of the password
net accounts /maxpwage:30
if errorlevel 1 echo Unsuccessful
::this will change the minimum age of the password
net accounts /minpwage:5
if errorlevel 1 echo Unsuccessful
::this will change the number of passwords stored
net accounts /uniquepw:5
if errorlevel 1 echo Unsuccessful
echo secpol.msc (local security policy) must be started to change complexity requirements, disable reversible encryption, and set account lockout threshold
start secpol.msc /wait
pause

:: finding and deleting media files
echo finding and deleting media files from users...
cd C:\Users
DEL /S *.3g2 
if errorlevel 1 echo Unsuccessful
DEL /S *.3gp 
if errorlevel 1 echo Unsuccessful
DEL /S *.asf 
if errorlevel 1 echo Unsuccessful
DEL /S *.avi 
if errorlevel 1 echo Unsuccessful
DEL /S *.flv 
if errorlevel 1 echo Unsuccessful
DEL /S *.m4v 
if errorlevel 1 echo Unsuccessful
DEL /S *.mov 
if errorlevel 1 echo Unsuccessful
DEL /S *.mp4 
if errorlevel 1 echo Unsuccessful
DEL /S *.mpg 
if errorlevel 1 echo Unsuccessful
DEL /S *.rm 
if errorlevel 1 echo Unsuccessful
DEL /S *.srt 
if errorlevel 1 echo Unsuccessful
DEL /S *.swf 
if errorlevel 1 echo Unsuccessful
DEL /S *.vob 
if errorlevel 1 echo Unsuccessful
DEL /S *.wmv 
if errorlevel 1 echo Unsuccessful
DEL /S *.aif 
if errorlevel 1 echo Unsuccessful
DEL /S *.iff 
if errorlevel 1 echo Unsuccessful
DEL /S *.m3u 
if errorlevel 1 echo Unsuccessful
DEL /S *.m4a 
if errorlevel 1 echo Unsuccessful
DEL /S *.mid 
if errorlevel 1 echo Unsuccessful
DEL /S *.mp3 
if errorlevel 1 echo Unsuccessful
DEL /S *.mpa 
if errorlevel 1 echo Unsuccessful
DEL /S *.wav 
if errorlevel 1 echo Unsuccessful
DEL /S *.wma 
if errorlevel 1 echo Unsuccessful
pause

:: sets auditing on everything.
echo Setting auditing success and failure for all categories...
auditpol /set /category:* /success:enable
if errorlevel 1 echo Unsuccessful
auditpol /set /category:* /failure:enable
if errorlevel 1 echo Unsuccessful
echo Set auditing success and failure
pause

:: patch applications
:: installs patch my pc to find outdated applications and update them
echo downloading patch my pc...
powershell -Command "Invoke-WebRequest https://patchmypc.com/freeupdater/PatchMyPC.exe -OutFile PatchMyPC.exe"
if errorlevel 1 echo file download Unsuccessful
echo installing patch my pc...
PatchMyPC.exe
if errorlevel 1 echo patch my pc install unsuccessful
echo running patch my pc... 
echo you will need to scan and install updates mannualy
REM PatchMyPC.exe
REM if errorlevel 1 echo patch my pc did not execute successfully (try running PatchMyPC mannualy)
pause

:: installs bitdefender antivirus and executes it
echo downloading bitdefender free antivirus...
powershell -Command "Invoke-WebRequest https://www.bitdefender.com/solutions/free/thank-you.html -OutFile bitdefender_online.exe"
if errorlevel 1 echo file download Unsuccessful
echo installing bitdefender...
bitdefender_online.exe
if errorlevel 1 echo bitdefender install unsuccessful
REM echo running bitdefender... 
REM echo you will need to scan and delete malicous programs mannualy
REM bitdefender_online.exe
REM if errorlevel 1 echo bitdefender not execute successfully (try running bitdefender mannualy)
pause

echo the program is complete the following things should be checked of your checklist
echo 1.Automatic updates turned on (remember you will still have to mannualy install updates)
echo 2.Guest account is disabled
echo 3.Password policies should be successfully set
echo 4.media files should be successfully removed
echo 5.PatchMyPC is installed and updated
echo 6.Bitdefender AntiMalware is installed and viruses are removed
echo remember to check all the changes and fix any errors caused by the program
echo would you like to exit the program?
pause
echo the script is exiting now...

EXIT


