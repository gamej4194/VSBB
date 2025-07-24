@echo off
setlocal enabledelayedexpansion

rem NAME OF THE WORLD YOU WICH TO BACKUP
set savename=SAVE-NAME

rem WHERE TO SAVE
set backupFolder=C:\vsbackup

rem HOW MANY BACKUPS
set BackupNumber=5

set "sourceFile=%appdata%\VintagestoryData\Saves\%savename%.vcdbs"
set "lastBackup=%backupFolder%\%savename%.bak1"
fc %sourceFile% %lastBackup% >nul
if errorlevel 1 (
    echo Files are different.
) else (
	exit /b
)
tasklist /FI "IMAGENAME eq Vintagestory.exe" 2>NUL | find /I "Vintagestory.exe" >NUL
if "%ERRORLEVEL%"=="0" (
    echo Vintagestory.exe is running
) else (
	set baseName=%savename%
	if exist "%backupFolder%\%savename%.bak%BackupNumber%" del "%backupFolder%\%savename%.bak%BackupNumber%"	
	for /l %%i in (%BackupNumber%,-1,1) do (
		set /a o=%%i+1
		if exist "%backupFolder%\%savename%.bak%%i" ren "%backupFolder%\%savename%.bak%%i" "%savename%.bak!o!"
	)
copy /Y "%sourceFile%" "%backupFolder%\%savename%.bak1"
)
