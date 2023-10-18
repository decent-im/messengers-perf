# For the courageous and generous souls who want to contribute data

## [1/2] Extract

We extract data via ADB while the device has USB unplugged.
This won't happen on its own.

## Debug-train your device

Connect your Android and your PC with a USB data cable.
In Settings - System - "Developer Options", enable "USB debugging".
On newer Androids, there's "Wireless debug" option, enable it too.

You should be able to

* run `adb devices -l` and see your device.
* run `adb shell echo hello world` and see it succeed.

## Remote-debug-train your device

Now enable the same access *by local network*.

On the phone, have your screen on and expect a system dialog to appear later.

On PC, run `adb tcpip 5555`

Do the following on a PC: `adb connect PHONE-LAN-IP:5555`.
Alternatively, you can do this in Termux on the phone itself: `adb connect 127.0.0.1:5555`.

You should be able to run `adb -s PHONE-LAN-IP:5555 shell echo hello world` and see it succeed.

## Start data extraction

The following can be done on a different PC than the one you've used above.
It is better to run this on an always-on PC in a persistent terminal session, using `tmux` or alternatives.

Clone the repo https://github.com/decent-im/messengers-perf (or just copy the `extract` tool).

Create an empty directory for dumping data, step into it, and launch the `extract` tool, telling it how to reach your device.
It will loop, taking a snapshot of data every minute. Disk space consumption rate is up to 400 MB/day.

```
git clone https://github.com/decent-im/messengers-perf
mkdir my-android
cd my-android
../messengers-perf/extract PHONE-LAN-IP:5555
```

You should see dots appearing in your terminal every minute.

Androids tend to disconnect for various reasons.
So check your terminal from time to time, for example, in the morning and in the evening.

## [2/2] Transform and load

I will writte this down later.
For now, once you have established data extraction, please contact me by email at messengers-perf@autkin.net .
We will set up continuous uploading of your data.
