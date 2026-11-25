# BareMP3

**Keep the audio. Strip the metadata.**

An offline browser tool for removing supported embedded MP3 metadata and artwork. Add MP3 files, ZIP archives, or a mix of both. Download cleaned MP3s together in one ZIP, with original filenames and folder paths preserved.

## Use

Open `index.html` in a modern browser, select files, click **Clean & build ZIP**, then download the result. No build, server, account, or external script downloads are needed. Audio is processed locally in your browser.

## GitHub Pages

In repository **Settings → Pages**, choose **Deploy from a branch**, then select **main** and **/ (root)** and save. The root `index.html` is the website entry point.

## Supported cleanup

- ID3v1 and ID3v2.2/2.3/2.4 tags, including source URLs, comments, lyrics, private frames and artwork.
- Supported APEv1/v2 and Lyrics3 layouts.
- Xing/Info/VBRI information frames at the start of audio sections.
- Original ZIP comments, extra fields, sidecars and timestamps are not copied. New ZIP entries use a fixed date.

Audio frames are copied without re-encoding. Removing information frames can affect gapless playback, seeking and duration estimates.

## Limits and privacy

Up to 200 MP3s, 250 MB total input, and 500 MB expanded audio. Free-format MP3s and encrypted, multi-volume or ZIP64 archives are unsupported. ZIPs inside ZIPs are ignored. Unsupported or structurally invalid files are excluded; duplicate output paths stop processing. ZIP entries are checked for size and CRC integrity.

This is not an anonymity guarantee. Filenames, speech, watermarks and identifiers within audio frames remain. Filesystem attributes are not part of browser uploads; the browser or operating system may add new download-origin attributes to the ZIP or extracted files. A website cannot clear those attributes.

## Validation

Tested with 75 MP3 fixtures (59 supported files cleaned; 16 invalid cases rejected), 500 deterministic tag combinations, and 28 ZIP scenarios. FFprobe and Mutagen checked supported outputs. All 59 supported fixtures decoded successfully. Audio packet hashes matched for 38 standard fixtures. These are fixture-based checks, not proof against every possible encoding or hidden identifier. The interface handlers were exercised in a simulated DOM; full visual and cross-browser testing remains to be done.

## Third-party software

Includes fflate 0.8.2 by Arjun Barrett under the MIT license. Its license notice is included in `index.html`.
