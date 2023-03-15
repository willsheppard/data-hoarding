# awesome-data-hoarding

A single-page cheat sheet of commands and tools for scraping, saving, hoarding, archiving, collecting, organising and browsing data.

Inspired by Reddit's [/r/DataHoarder](https://www.reddit.com/r/DataHoarder/)

## Quick reference

Which archiving tool should you choose?

- Amazon Video: Unknown. Check torrents instead.

- BBC iPlayer: [youtube-dl](https://youtube-dl.org/) / [yt-dlp](https://github.com/yt-dlp/yt-dlp)

- Discord: DiscordChatExporter (see below for notes)

- Mediawiki website: Native dump using `/wiki/Special:AllPages` and `/wiki/Special:Export`.

- Netflix: Unknown. Check torrents instead.

- Reddit thread: TO DO

- Tumblr: [TumblThreeApp](https://github.com/TumblThreeApp/TumblThree) (Windows)

- Twitter: [ThreadReaderApp](https://threadreaderapp.com/)

- Torrents: Use [unblockit](https://www.google.com/search?q=unblockit) for a list of torrent sites. Official [Twitter](https://twitter.com/thepirateproxy) / [Reddit](https://www.reddit.com/r/Unblockit/).

- Private torrent trackers: Might contain any TV or movie ever broadcat. It can be difficult to get an invite, and you may need to maintain an upload ratio.

- Websites generally: wget, httrack or [ArchiveBot](https://wiki.archiveteam.org/index.php?title=ArchiveBot).

- Youtube video/music: [youtube-dl](https://youtube-dl.org/) (see below for notes) / [yt-dlp](https://github.com/yt-dlp/yt-dlp)

## Scraping tools

Details of precise sets of commands.

### General purpose

- [wget](https://www.gnu.org/software/wget/manual/wget.html)

```
wget \
    -e 'robots=off' \
    --accept '*.*' \
    --mirror \
    --wait 2 \
    --random-wait \
    --convert-links \
    --user-agent 'Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.7113.93 Safari/537.36' \
    'http://www.example.com/'
```

- [StreamRipper](http://streamripper.sourceforge.net)
    - Example: `streamripper ###URL### -u "FreeAmp/2.x" -q -l 86400`

- [Chrome DevTools](https://developer.chrome.com/docs/devtools)
    - [network tab](https://developer.chrome.com/docs/devtools/network/reference)
    - [resources tab](https://developer.chrome.com/docs/devtools/resources)

### Specialised

- Mediawiki
    - For an XML dump containing wikitext...
    - Copy names of pages from `/wiki/Special:AllPages`...
    - Paste into `/wiki/Special:Export`
    - (optional) Parse resulting wikitext with [mwparserfromhell](https://github.com/earwig/mwparserfromhell).

- [youtube-dl](https://yt-dl.org) / [yt-dlp](https://github.com/yt-dlp/yt-dlp)
    - Example: `youtube-dl ###URL### --ignore-errors --extract-audio --audio-quality 0 --audio-format mp3 --prefer-ffmpeg --output "%(title)s.%(ext)s" `
    - Playlist: `youtube-dl ###URL### ...etc... --output "%(playlist_title)s/%(playlist_title)s - %(playlist_index)02d - %(artist)s - %(title)s.%(ext)s"`
    - Album: `youtube-dl ###URL###  ...etc... --output "%(album)s - %(artist)s - %(track)s.%(ext)s"`

- [DiscordChatExporter](https://github.com/Tyrrrz/DiscordChatExporter) + excellent [wiki](https://github.com/Tyrrrz/DiscordChatExporter/wiki)
    - Example: `docker run --rm -v /var/www/zaphod/adhd:/app/out tyrrrz/discordchatexporter:stable export --channel ###ID### --token ###SECRET### --format Json`
    - List guilds: `docker run tyrrrz/discordchatexporter:stable guilds`
    - List channels: `docker run tyrrrz/discordchatexporter:stable channels --guild ###ID###`

## Processing tools

- [jq](https://stedolan.github.io/jq/)
    - Example: `jq -j -M --stream -f discord1.jq` [discord1.jq](https://gist.github.com/willsheppard/f9b7cc9b130784ffd7bd8f144cf892f8)

- [XPath Helper](https://chrome.google.com/webstore/detail/xpath-helper/hgimnogjllphhhkhlmebbmlgjoejdpjl)
    - Example: Ctrl-Shift-X (or Command-Shift-X on Mac)

## Techniques

### Extract from chrome devtools

Good for: Structured data

- The network tab shows XHR requests being made 

## Discussion

- If an archive of data is made, and that data cannot be viewed in a way similar to its original presentation, then the average person can't view it at all. It may as well not exist for that person. You might retort "A viewer program could be built". But if that viewer program doesn't yet exist, then the data still can't be viewed. It's a Schroedinger's archive.

## Communities

- https://www.reddit.com/r/DataHoarder

## Similar projects

- https://github.com/igorbarinov/awesome-data-engineering
- https://github.com/lorien/awesome-web-scraping
