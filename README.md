# hkmc.track-button-swap v1.0

Reverses the steering-wheel track buttons on the Kia EV6 (Gen5W) head unit:
UP = next track, DOWN = previous track. Requires NEMESIS.

Tested on a 2023 Kia EV6 GT-Line, US version.

Package id on the head unit: `hkmc.track-button-swap`

---

## Install via ADB (USB cable)

Run these from the folder that contains `hkmc-track-button-swap-v1.0.nemesis.zip`.

1. Confirm the head unit is connected (it should be listed as `device`):
   ```
   adb devices
   ```

2. Copy the package to the head unit:
   ```
   adb push hkmc-track-button-swap-v1.0.nemesis.zip /data/local/tmp/
   ```

3. Install it (works for a fresh install or an upgrade):
   ```
   adb shell "nemesis root -c 'nemesis install --update /data/local/tmp/hkmc-track-button-swap-v1.0.nemesis.zip'"
   ```
   Expected: `ok installed hkmc.track-button-swap` or `ok updated hkmc.track-button-swap`.

4. Wait about 20 seconds, then confirm the swap was written:
   ```
   adb shell "nemesis root -c 'grep -n CHANNEL /system/usr/keylayout/daudio_wp_daudioplus_cvev_base.kl'"
   ```
   Expected: `key 34 CHANNEL_DOWN` and `key 35 CHANNEL_UP`.

5. Reboot the head unit:
   ```
   adb reboot
   ```
   When the home screen is back, test the wheel: UP = next track.

6. (Optional) Remove the copied package file:
   ```
   adb shell "rm -f /data/local/tmp/hkmc-track-button-swap-v1.0.nemesis.zip"
   ```

Note: always run NEMESIS commands through `nemesis root -c '...'` over ADB.

---

## Install via USB flash drive

1. Use a USB flash drive formatted as **FAT32** or **exFAT**.

2. Extract the contents of `hkmc-track-button-swap-v1.0.usb.zip` to the
   **root** of the drive. The drive should contain:
   ```
   NEMESIS.data
   README-hkmc-track-button-swap.md
   packages/hkmc-track-button-swap.nemesis.zip
   ```
   Keep only one `NEMESIS.data` on the drive (no other package installers).

3. Safely eject the drive.

4. In the car, with the head unit fully booted, insert the drive and tap
   **Yes** on the install prompt (or the update prompt if already installed).

5. Wait about 20 seconds, then remove the drive.

6. Reboot the head unit: press and hold the audio power button (volume knob)
   for about 10 seconds until it restarts. A normal car off/on may not fully
   reboot the head unit.

7. Test the wheel: UP = next track.

---

The swap takes effect after a reboot. Uninstalling (NEMESIS Manager >
Packages > Uninstall, then reboot) restores the stock button behavior.
