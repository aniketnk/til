# Errors trying to install C/C++ packages from source in Mojave or higher
> Fri May  8 02:44:57 IST 2020

## Errors similar to these:
```
/usr/include missing on macOS Catalina (with Xcode 11)

error: expected '=', ',', ';', 'asm' or '__attribute__' before '__OSX_AVAILABLE_STARTING'
```

## Solution
*Solution 1*
```
export CPATH=`xcrun --show-sdk-path`/usr/include
```

*Solution 2*
Alternatively you can make a soft-link to the above at `/usr/include` if you have SIP disabled(not recommended)
```
sudo ln -s `xcrun --show-sdk-path`/usr/include /usr/include
```

*Reference 1: [stackoverflow](https://apple.stackexchange.com/a/372600/374785)*

*Reference 2: [stackoverflow](https://stackoverflow.com/a/58000319/9726680)*
