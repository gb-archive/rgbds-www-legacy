---
layout: default
name: Windows
title: Windows install instructions
---

# Installing RGBDS on Windows

The install instructions change a bit depending on the environment you wish to use RGBDS with.

## Windows (CMD, PowerShell)

These instructions may also work for some environments listed further below, since most of them pick up Windows' PATH.
If you have such an environment, we recommend you follow its specific install instructions.

1. First, [pick the version you want to install]({{ site.baseurl }}/docs). If you want to [use `master`]({{ site.baseurl }}/docs/master/#what) instead of a release, [go here](master).
2. Follow the "release page" link below "GitHub links", and grab either of the `win32` (for 32-bit Windows) or `win64` (for 64-bit Windows) `.zip` files, near the bottom of the page.
3. Unzip that file, you should get the `.exe` files alongside a couple of `.dll`s.
4. Either:
   - Put all of the files in a directory, then add it to the `PATH`, using one of the following methods:
     - Graphically:
       1. Open Control Panel
       2. Click "User Accounts"
       3. Click "User Accounts" again
       4. Click "Change my environment variables"
       5. Select the "Path" line in the **top** panel
       6. Click "Edit..."
       7. Click "Browse...", select the folder the files are in, and click OK
       8. Make sure that the new entry (which should be highlighted) is at the bottom of the list; if not, click on "Move Down" until it is
       9. Click "OK"
       10. Click "OK"
     - Using a command line:
       1. Use Explorer to go into the folder the files are in (you should see `rgbasm.exe` etc.), and click a blank part of the address bar near the top. Copy this path, and **use this instead of `<rgbds_path>` in step 3!**
       2. Open `cmd` or PowerShell
       3. Type `setx PATH "%PATH%<rgbds_path>;"` for `cmd.exe`, or `setx PATH ${Env:PATH}<rgbds_path>;` for PowerShell
       4. Close the window for the changes to take effect
       
       This will permanently allow you to use RGBDS. If you only want to modify the PATH temporarily, instead of the permanent [`setx` command](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/setx), you can use  the **temporary** [`set` one](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/set_1): `set PATH="%PATH%<rgbds_path>` for `cmd.exe`.
   - Put all of the files in your project's directory
   - Put all of the files in a directory already in the `PATH`
5. Profit! RGBDS can now be used from your favorite command line (`cmd.exe` or PowerShell, most likely). You can test it by running `rgbasm --version`.

## [Cygwin](https://cygwin.com/), [MSYS2](https://github.com/msys2/msys2)

Follow steps 1 to 3 of the instructions above to get the release's files; then, copy all of the `.exe` and `.dll` files to the `/usr/local/bin` directory of Cygwin/MSYS2's installation.
(You can get its equivalent Windows path by running `cygpath -w /usr/local/bin`.)
**Do not put them in a subdirectory** (e.g. `/usr/local/bin/rgbds`)**!**
This would not work.

After that, you should be able to use RGBDS from within the Cygwin/MSYS2 terminal, which you can confirm by running `rgbasm -V`.
If this doesn't work, check that `/usr/local/bin` is within the PATH there (`echo $PATH`); if it isn't, you must add it (e.g. `export PATH="/usr/local/bin:$PATH"` in the `~/.bashrc`).

Note: if you can choose between using Cygwin or MSYS2, be advised that Cygwin is slower and has been reported to cause a bit of trouble to some.

## [WSL](https://docs.microsoft.com/en-us/windows/wsl/), and all other Linux-like environments

For these, you have to [build from source](source). On WSL, you should install any prereqs using `apt-get` (example: `sudo apt-get install libpng-dev`).
