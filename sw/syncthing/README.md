### Windows batch

start_syncthing.bat
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
stop_syncthing.bat
```batch
@echo off

taskkill /IM syncthing.exe /T /F

pause
```

copy_config.bat
```batch
@echo off

if not exist "%~dp0config\" (
mkdir "%~dp0config"
xcopy "%localAppData%\Syncting" "%~dp0config"
)

pause
```

move_config.bat
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
