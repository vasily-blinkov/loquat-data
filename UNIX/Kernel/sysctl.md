# sysctl

The `sysctl` is a utility to configure kernel parameters at runtime

## List tunable parameters

```tcsh
sysctl -a
```

## `hw.snd.vpc_0db`

If you are hard of hearing, you may find the `hw.snd.vpc_0db` tunable option is useful when the volume level of a playing media (for example with `mplayer` or `firefox`) is low.

Firstly, find out the current value of the parameter: `sysctl hw.snd.vpc_0db`. In FreeBSD it's defaulted to `45`.

Then, start the media playback.

Finally, increase the playing media volume by decreasing the parameter: `sudo sysctl hw.snd.vpc_0db=15`.

### Notes

1. Do not listen media at high volume for a long time as it may corrupt your hearing more.
1. The `hw.snd.vpc_0db` parameter is also (of course) tunable in the `/boot/loader.conf` file.
1. If the value of the parameter is set to `0` already, you need to reset it to its maximum `100` before starting playback because the `hw.snd.vpc_0db` is relative to the current volume level.
1. In `firefox` you may need to close the tab and open its URL again to take effect.
1. Pausing playback (especially in `firefox`) may cause resetting the system volume level back to normal. If that is happen, you will need to repeat the procedure again.
