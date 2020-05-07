# Problem: Read-only file system
> Fri May  8 02:49:57 IST 2020

- macOS Catalina Read-only file system with ***SIP disabled***
- How to create a symbolic link at / in Catalina with ***SIP disabled***?

A new feature introduced in Catalina - the system folder now resides in a read only partition so it cannot be messed with.

## Solution
Just run the following (you need to redo it if you reboot):
```
sudo mount -uw /
killall Finder
```
And you should be good to go.

*Reference*: [*reddit*](https://www.reddit.com/r/MacOS/comments/caiue5/macos_catalina_readonly_file_system_with_sip/)