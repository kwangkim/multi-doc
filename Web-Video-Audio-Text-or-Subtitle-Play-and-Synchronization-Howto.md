# Web Video Audio Text or Subtitle Play and Synchronization Howto
## About
* TODO

## Web Players
* [popcorn.js player](http://popcornjs.org/)
 * HTML5 Java Script Library for integrating the web into video
 * License: Mozilla Project (free)
 * [reference - synchronizing and highlighting HTML Text to Audio](http://stackoverflow.com/questions/10743683/synchronize-and-highlight-html-text-to-audio)
 * [Example Demo-1](view-source:http://fiddle.jshell.net/thisgeek/At3xg/show/): text color is changed with audio progress, or if you click text word then audio skips there
 * [Example Demo-2](http://www.npr.org/2012/07/17/156611072/press-play-poetry-summer-song): poem play with line highlighting)
 * [Example Demo-3](http://www.samuelnegredo.com/zaragoza-public-spaces/iaacc.htm): interactive text descriptions with audio progress
 * you must sync the A/T manually
* [Jaraoke](http://randallagordon.com/jaraoke/)
 * [howto](http://randallagordon.com/blog/2009/07/19/jaraoke-html5-audio-tag-demo/)
 * HTML5 Audio Tag Sync using Javascript
 * [download jaraoke.js](http://randallagordon.com/jaraoke/js/jaraoke.js)
 * Example: [Martin Luther Kin Jr.'s I Have a Dream](http://j.hn/lab/html5karaoke/dream.html)
 * Restricted License: [Creative Commons Attribution-Noncommercial-Share Alike 3.0 United States License](http://creativecommons.org/licenses/by-sa/3.0/us/)
```js
var currCue = 0;  
var cues = [ 24.78, 26.81, 29.69, 34.88, ... ];  
var lyrics = [  "Am I...",  
                "Am I still tough enough?",  
                "Feels like I'm wearing down, down, down, down, down...",  
                "Is my viciousness", ... ];  
  
this.apN.addEventListener("timeupdate", timeUpdate, true);  
  
function timeUpdate() {  
    if(jaraoke.apN.currentTime > (cues[currCue] - CUEOFFSET)) {  
        var el = $(document.createElement('li')); 
        el.update(lyrics[currCue++]); 
        $('lyricsList').insertBefore(el, $('lyricsList').firstChild);  
    }  
}  
```
* [Good Reference - Rock Star Market](http://rockstarmarket.com/html5_audio/)
 * HTML5 Audio Play with Progress bar
 * If you click any text, the audio goes there
* [ESV Text/Audio Aligner](https://github.com/westonruter/esv-text-audio-aligner)
 * internally calls CMUSphinx
 * dependency: Python 2.7, Java, ant, [sox](http://sox.sourceforge.net/), svn
 * ESV: English Standard Version of Bible (c)2001 by Crossway Bibles, [license](http://www.crossway.org/rights-permissions/esv/)
 * [Bible Karaoke](http://j.hn/lab/html5karaoke/): need some modifications for browser detection routine
 * [a JavaScript audio text aligner](http://johndyer.name/html5-audio-karoke-a-javascript-audio-text-aligner/)
 * License: MIT or GPL v2
```sh
# python align.py Gen 1; // align Genesis 1
# python align.py -f John 3; // overrides any existing timings
# python align.py Gen 1 2 3 Ps 1 Col; // align Genesis 1-3, Psalm 1, and all of Colossians
```
* [jPlayer](http://www.jplayer.org)
 * Open Source (no licensing restrictions)
 * lightweight - only 12KB minified and gzipped
 * totally customizable and skinnable using HTML and CSS
 * free plugins available
 * [audio-text synch](http://happyworm.com/jPlayerLab/audiotextsync/v13/#) - A/T sync by click
* timesheets.js: a declarative approach for HTML timing using SMIL timesheets
 * [here](http://wam.inrialpes.fr/timesheets/slideshows/audio.html)
 * Audio / Text time sync + slides
* [Media Element JS](http://mediaelementjs.com/)
 * Video + Audio + Subtitles (.srt)
 * HTML5 <video>, <audio> with <track>
```js
<code><script src="jquery.js"></script>
<script src="mediaelement-and-player.min.js"></script>
<link rel="stylesheet" href="mediaelementplayer.css" /></code>
```
* [videojs - San Francisco (http://videojs.com)](https://github.com/videojs/video.js)
 * Open Source HTML5 & Flash Video Player
 * [designer - video.js player skin editor using a live CSS editor](https://github.com/videojs/designer)
 * Text Track: [WebVTT](http://dev.w3.org/html5/webvtt/) File

## Video - Audio - Time Location - Slides
* [here](http://videolectures.net/w3cworkshop2013_brelstaff_solutions/)

## Reference Links
* [Online Audio Story Material](http://storycorps.org/about/)
* [CMU Sphinx-4 - Long Audio Aligner Project](https://github.com/cmusphinx/sphinx4)
 * After 3 years of work since 2011 at GSoC, CMU Sphinx-4 is equipped with the new feature of Long Audio Aligner. Just download Sphinx4 and "mvn install"
 * input file must be 16kHz, 16bits mono
 * numbers are not handled yet
```sh
# java -cp sphinx4-samples/target/sphinx4-samples-1.0-SNAPSHOT-jar-with-dependencies.jar \
edu.cmu.sphinx.demo.aligner.AlignerDemo file.wav file.txt en-us-generic \
cmudict-5prealpha.dict cmudict-5prealpha.fst.ser
+ of                        [10110:10180]
  there                     [11470:11580]
  are                       [11670:11710]
- missing
```
* Sonalight - mobile dictation application: [here](http://sonalight.com/)
 * CMUSphinx-powered app
