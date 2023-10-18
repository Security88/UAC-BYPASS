
```batch
@echo off
setlocal enabledelayedexpansion
call :definePaths
call :downloadFile
call :modifyRegistry
call :runFodHelper
goto :end

...

:end
endlocal
