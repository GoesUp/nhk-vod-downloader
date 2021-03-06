# NHK Video-On-Demand Downloader

Downloads videos from NHK's Video On Demand Service.

Download a built version for Windows: [Releases](../../releases)

### Requirements
- Google Chrome (this code uses `chromedp` to obtain the "hidden" video ID due to NHK's fancy schmancy Javascript shenanigans. I didn't want to bother reading their 15k+ lines of JS code just to be able to reproduce the request to get the ID.)
- FFmpeg (only if you want to convert your video to mkv afterwards) - not yet implemented

### Command line arguments
- `-u "url"` - This is how you let the program know which video you want downloaded. *Required.*
- `-p "path"` - If you don't want this program to save the video next to the executable, use this argument and specify your desired output path. *Optional.* (not yet implemented)
- `-c` - Use this if you want to convert the downloaded and merged video to MKV. Why MKV? Because I like it best and I don't really think anyone else will use the code anyway. Note: this only copies the video information into a different kind of media container, no actual encoding is done here. *Optional.* (not yet implemented)
- `-dm` - Use this if you don't want to merge the small TS files into a single big file. No clue why anyone would want this, but hey, it's here. *Optional.* 
- `-h` - Use this to start Chrome in headless mode if you're reeealy bothered by the Chrome window opening for a few seconds at the start. Highly not really very recommended due to the fact that you will have to restart your computer or manually kill the `chrome.exe` processes if you want to use the program more than once in a row. Don't blame me - this happens because `chromedp` is broken. Just don't use `-h` unless you know what you're doing or you're fine with killing Chrome manually after each use. Check the Troubleshooting section if you got in trouble because of this. *Optional, obviuosly.*
- `-?` - Lists all possible arguments. *Optional.*

### Troubleshooting
- If the Chrome window doesn't close, you probably didn't specify a valid video URL. If the video didn't load on the page for some reason, just try refreshing the page in the Chrome window.
- If the only output is `timeout waiting for initial target` after a few seconds of running, run `taskkill -f -im chrome.exe` in your command prompt and try again (Windows only, I didn't try it on Linux). This *probably* happened because you used `-h` as a command line argument.  
- If converting fails, you probably didn't add FFmpeg to PATH. Do that first.


### Disclaimer
I didn't check, so I'm not sure if using this code is allowed by NHK's TOS. Use only if you've checked and you're sure downloading from their website is not disallowed.

I don't guarantee that this code works. On the contrary - I can guarantee that you'll be able to break it with relative ease. This is not meant to be a robust and future-proof solution for downloading from NHK, it's just something I put together some boring Saturday afternoon.

### TODO:
- goroutines
- implement the rest of the command line arguments
- ensure this downloader can run normally on Linux (path formatting and stuff)
