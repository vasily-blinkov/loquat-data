# MPlayer

## Run examples

### Fullscreen and subtitles with a specified encoding

Create an alias (tcsh):

```tcsh
alias mplayer 'mplayer -fs -subcp utf-8 $1'
```

then just run it.

```tcsh
mplayer 12-divided.avi
```
