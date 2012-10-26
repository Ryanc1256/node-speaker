node-speaker
============
### Output raw PCM audio data to the speakers


A Writable stream instance that accepts raw PCM audio data and outputs it to the
speakers. The output is backed by `mpg123`'s audio output modules, which in turn
use any number of audio backends commonly found on Operating Systems these days.

Installation
------------

Simply compile and install `node-speaker` using `npm`:

``` bash
$ npm install speaker
```


Example
-------

Here's an example of piping `stdin` to the speaker, which should be 2 channel,
16-bit audio at 44,100 samples per second (a.k.a CD quality audio).

``` javascript
var Speaker = require('speaker');

// Create the Speaker instance
var speaker = new Speaker({
  channels: 2,          // 2 channels
  bitDepth: 16,         // 16-bit samples
  sampleRate: 44100     // 44,100 Hz sample rate
});

// Raw PCM data from stdin gets piped into the speaker
process.stdin.pipe(speaker);
```


API
---

### Speaker class

TODO: document...


Audio Backend Selection
-----------------------

`node-speaker` is backed by `mpg123`'s "output modules", which in turn use one of
many popular audio backends like ALSA, OSS, SDL, and lots more. The default
backends for each operating system are described in the table below:

| **Operating System** | **Audio Backend** | **Description**
|:---------------------|:------------------|:----------------------------------
| Linux                | `alsa`            | Output audio using Advanced Linux Sound Architecture (ALSA).
| Mac OS X             | `coreaudio`       | Output audio using Mac OS X's CoreAudio.
| Windows              | `win32`           | Audio output for Windows (winmm).
| Solaris              | `sun`             | Audio output for Sun Audio.

To manually override the default backend, pass the `--mpg123-backend` switch to
`npm`/`node-gyp`:

``` bash
$ npm install speaker --mpg123-backend=openal
```
