# MPlayer

## Run

### Getting started: simplest run procedure

```tcsh
mplayer 12-divided.avi
```

### Run examples

#### Fullscreen and subtitles with a specified encoding

Create an alias (tcsh):

```tcsh
alias mplayer 'mplayer -fs -subcp utf-8 $1'
```

then just run it.

```tcsh
mplayer 12-divided.avi
```

## Usage

* Volume
  * Mute/unmute: `m`
  * Decrease: `9`
  * Increase: `0`
* Pause/resume: `space`
* Toggle fullscreen: `f`
* Choose audio track: `#`
* Choose subtitles track: `j`
* Quit: `q`

## CLI reference

* `-fs`: fullscreen
* `-subcp ENCODING`: subtitles encoding, where `ENCODING` is en encoding name, like `cp1251` or `utf-8`; example: `mplayer -subcp cp1251 12-divided.avi`
