# Voice support tools and scripts for Music Assistant

Bridge the gap between Home Assistant Assist and Music Assistant for voice-initiated music control.

This repository is meant to be an effort to collect scripts, blueprints, HOWto's etc. and their translations to enable full Voice control of music playback.
Home Assistant itself has very limited intents for music/media control, and especially there is no support for initiating playback of music by voice.
While this support is on the horizon to be added, there is still a lot to investigate about that to create a universal way to provide that support in HA natively. Maybe the resources/experiments from this repository can help make that journey easier in the future.

**Community driven effort!**
Please reach out if you want to help out or have great ideas!
If you have something to share here, feel free to PR it or ask to be added to the maintainers.

## Option 1: Local Assistant Blueprint

Blueprint to initiate media playback using pure local intent handling (custom sentences) so no Cloud-LLM involved.
This however means that requests need to be very carefuly formulated.

The Blueprint is located in the local-assistant-blueprint folder of this repository.

### Usage

All sentences must:

- start with the words `Play` or `Listen to` followed by the item type `artist/track/album/playlist/radio station` and then the name of the item

- for album and track be optionally followed by `by (the) artist` and then the artist name

- then be optionally followed by an area name or device name

- then, for artist, track, album or playlist, be optionally followed by the phrase `using radio mode`

#### Acceptable variations

There are acceptable variations to some words and inclusion of the word `the` is optional.

#### Examples

```

Play the artist Pink Floyd in the kitchen

Listen to album Jagged Little Pill in the study

Listen to the album Greatest Hits by the artist James Taylor in the kitchen

Play track New Years Day in the bedroom

Play track New Years Day in the bedroom using radio mode

Play the song A Hard Days Night by Billy Joel in the bedroom

Listen to the playlist Classic Rock in the study

Listen to the radio station BBC Radio 1 in the bedroom

Play the album Classical Nights on the Bedroom Sonos Speaker

Listen to the record Classical Nights on the Bedroom Sonos Speaker

Play the band U2
```
