# Microsoft Visual C++ Build Tools

# Visual Studio Build Tools

# Standalone MSVC compiler

Version: `2022 LTSC 17.2`

**fully offline install** of the minimum required MSVC build tools

The files are signed by Microsoft and from their servers.

You can blacklist/firewall Microsoft completely and still compile what you need. Go ahead and blacklist all their ASNs. I assume you have at least access to GitHub somehow, since.. well.. GitHub. No choice there. Or use it offline-offline, actual unplug-it-offline, from before forced online abuse came up.

## install

- clone this repo
- unpack via 7-Zip
  ```powershell
  7z x .\VSLayout.7z.001
  ```
- run one of the included `cmd` files as admin
    + or push it manually `vs_BuildTools.exe --noWeb`, for unattended add: `--quiet --wait --norestart`
- Wait. It takes a long time. Enough time to download [MinGW](https://www.mingw-w64.org/) or install several [Debian](https://www.debian.org/) machines.
- Finally compile whatever you need to!

## size

If you only run this setup once (!), and delete the setup files after, about `1.6 GiB` will ultimately be used. (On a `21H2 LTSC` as of now.) Keep at least double available during install. This number may differ for you, I do not know how MS decides what to install. I've seen `6 GiB` for the same exact setup before.

If you ever let the ~~Visual Studio Installer~~ trojan dropper reign free in the future, prepare your disk for several dozens of GiBs.

About a dozen menu entries for things you do not want will be created. I tried more minimal configurations to no avail. If you know how to decrease size further, or how to rip the actual compiler/headers without breaking things randomly, send a message.

## components

Minimum viable build setup, no UWP. If you are forced to deal with UWP: I'm sorry, brother.

## N.B.

Microsoft is still as abusive as ever and simply ignores your *rights* (Does that word even bear any meaning in 2022?).

- Install an application firewall, like the excellent [simplewall](https://github.com/henrypp/simplewall), before you start, or it ***will*** **immediately**[^1] send tons of unwanted network requests without asking permission.
- Do not allow `svchost.exe` as that gives Microsoft free reign over your network and circumvents the firewall. Yes, it will break auto-updates, but you wouldn't be reading this, if you weren't capable of deploying them yourself.

## target audience

Developers and users forced to use the MSVC build tools.

Developers and users who aren't online 24/7 and want a reliable offline setup without huge efforts.

Developers and users who refuse to give Microsoft spyware unfettered network access.

As of today, the most common perp is probably Python's `distutils`, which refuses to cooperate with the user-respecting MinGW as it did in the past. Dozens upon dozens of threads/issues/SO posts later, nothing.

Hundreds of SO posts à la:

`error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/`

```
A: Install the <old-link-to-full-setup-that-is-gone-since-forever>.
R: That is not a full installer.
A: Indeed it is not, let me see.
A: Seems to redirect to some stub.
~confusion ensues
~hilarity ensues
A: Is Microsoft really trolling this hard?
A: Yes.

User left the building. 
```

After reading a few dozen you find out that in some mystical time called 2012 allegedly there was a (somewhat) reasonably sized offline installer. Not an archive like MinGW, allowing you to do as you please with some respect, and without blanket root permissions, but still, at least offline.

You try for yourself and find out it simply is not possible to install a primitive compiler and some headers without allowing Microsoft full access to everything.

You either give up, or give in. The oligarchy won.

## why this particular version

The 'LTS' brand no longer holds weight in the Microsoft world, as it has been degraded to ultra-short lifespans with the most recent iterations anyway (LTSB > LTSC > 10 > 5 > `aaS` > thin client > brain implant > ?), but it seemed prudent to choose it nonetheless.

You don't need the latest alpha to compile what you must.

LTSC versions might also trigger less auto-update-against-your-will nonsense, if you cannot get rid of that via GPs in your situation for whatever reason.

## how to create the files yourself

If you need a package that's not included, I strongly recommend doing this in a controlled environment, at least a VM, which you can monitor and wipe afterwards.

The only acceptable connection to Microsoft is **none**. If you give them even a fingertip, they will skin you alive. Good luck reverse engineering their infinite malware mechanisms. **Even [government agencies have tried and failed](https://www.bsi.bund.de/DE/Service-Navi/Publikationen/Studien/SiSyPHuS_Win10/SiSyPHuS_node.html)**, with their typical conclusion being: "Avoid if you can, you're not going to clean it up fully, ever." Who likes to maintain blacklists against a trillion dollar overlord? They can add more trash faster than you can get rid of it.

- download the [bootstrapper](https://docs.microsoft.com/en-us/visualstudio/releases/2022/release-history#release-dates-and-build-numbers) of your choice
- run
  ```powershell
  vs_BuildTools.exe --layout .\VSLayout
  --lang en-US
  --add Microsoft.VisualStudio.Workload.VCTools
  --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64
  --add Microsoft.VisualStudio.Component.Windows10SDK.19041
  ```
- temporarily whitelist the connections coming up
- additional components are listed [here](https://docs.microsoft.com/en-us/visualstudio/install/workload-component-id-vs-build-tools?view=vs-2022)

## privacy

If you find any personal metadata inside the archive, please let me know quietly. I think there shouldn't be, but we both know there are ways and humans make mistakes. Besides, it's 10s of thousands of files and not verifiable, alone.

## legal

Obviously the packaged files belong to Microsoft and I do not claim copyright on them.
All files are taken from public sources only. Public as in, 'run this malware dropper as root', but still. Microsoft oligarchs even bought GitHub, so it's right where it belongs.


[^1]:
    random samples:

    - `vctip.exe` supposedly belongs to the '''Visual Studio Experience Improvement Program'''. You did not even install Visual Studio. You might even have turned all that garbage off via GP. It doesn't care.
    - `mofcompiler.exe` ignores your wishes as well
    - `--noWeb` only prevents total failure, it does not actually mean 'no web'. This is even in their docs.
    - The list goes on and on. Try running even an '''enterprise''' Windows 10 while sniffing. No matter how hard you lock it down, and how much you beg for your basic legal rights, they simply do not care. They'd rather bribe a few politicians with laughable '''fines''' and continue unabashedly. God forbid you're on a metered connection or classic copper.

