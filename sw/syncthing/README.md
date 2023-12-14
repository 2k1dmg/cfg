### Windows batch

`start_syncthing.bat`  
For automatic start you need to create a shortcut and place it in **Win+R** for current user **shell:startup** for all **shell:common startup** <a href=https://docs.syncthing.net/users/autostart.html#windows>other methods</a>

```batch
@echo off

if not exist "%~dp0syncthing.exe" (
	echo File syncthing.exe doesn't exist.
	pause
	goto :EOF
)

if not exist "%~dp0config\" mkdir "%~dp0config"

start /d "%~dp0" syncthing.exe -no-console -no-browser -no-default-folder -home="%~dp0config"
IF ERRORLEVEL 1 (
	pause	
	goto :EOF
)
```

`*-no-default-folder`
```
		Set default folder.

http://localhost:8384

Actions - Settings - General - Edit Folder Defaults - Folder Path
	
	*path for example

D:\Sync\Syncthing

	Save
```

`stop_syncthing.bat`
```batch
@echo off

taskkill /IM syncthing.exe /T /F

pause
```

You need to stop Syncthing before starting to copy or move the config and start it again.

`copy_config.bat`
```batch
@echo off

if not exist "%~dp0config\" (
mkdir "%~dp0config"
xcopy "%localAppData%\Syncting" "%~dp0config"
)

pause
```

`move_config.bat`
```batch
@echo off

if not exist "%~dp0config\" (
mkdir "%~dp0config"
xcopy "%localAppData%\Syncting" "%~dp0config"
IF ERRORLEVEL 1 (
	pause	
	goto :EOF
)
del /S "%localAppData%\Syncting\*"
)

pause
```

### .stignore Patterns

```
	DCIM/Camera
.*
(?i)!/*.{mp4,jpg}
*

	Pictures/Screenshots (or DCIM/Screenshots)
.*
(?i)!/*.{mp4,jpg}
*
```

other
```
	DCIM/Camera
.*
(?i)!/*.{3gp,mp4,mkv,webm,ts,bmp,gif,jpg,png,webp,heic,heif,avif}
*

	Pictures
.*
(?i)!/Screenshots/*.{bmp,gif,jpg,png,webp,heic,heif,avif}
*

	DCIM/Camera
.*
// (?i)*.{tmp,temp}
!/*.*
*

	DCIM
.*
// (?i)*.{tmp,temp}
!/Camera/*.*
!/Screenshots/*.*
*

	DCIM/Camera
.*
(?i)!/*.{3gp,mp4,mkv,webm,ts,bmp,gif,jpg,png,webp,heic,heif,avif}
*

	DCIM
.*
(?i)!/Camera/*.{3gp,mp4,mkv,webm,ts,bmp,gif,jpg,png,webp,heic,heif,avif}
(?i)!/Screenshots/*.{bmp,gif,jpg,png,webp,heic,heif,avif}
*
```
