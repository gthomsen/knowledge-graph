Tags: #linux #ffmpeg #utilities #x265-codec

**NOTE: Always verify which `ffmpeg` you're running.  Anaconda's has different features than the system's.**

`ffmpeg` has a challenging interface.  Codec licensing, codec-specific options, and sequencing of flags/arguments makes configuring it difficult, though combined with experimenting with hardware makes this it a trial of keeping one's sanity.

This command line worked reasonably well to convert 4K videos recorded on a Go Pro 8 to bit rates acceptable by an [[Hardware Accelerated Codecs on Amazon Fire TV 4K|Amazon Fire TV 4K]] (attempting to not exceed the hardware's 30 Mbps limit):
```shell
# target a 15 Mbps output using a 30 MB buffer (2 seconds).  empiracally
# this does not typically exceed the Fire TV's 30 Mbps capabilities.
$ ENCODING_RATE_X265=15000
$ ENCODING_BUFFER_SIZE_X265=30000

# uncomment if rescaling is desired.  this forces output of 1080p.
# RESCALE_OPTIONS="-vf scale=-1:1080,setsar=1:1"

# balance CPU utilization against output quality.  empirically this
# works well enough to produce movies for a 65" 4K TV's screensaver.
PRESET=fast

$ ffmpeg \
    -i ${INPUT_PATH} \
    -x265-params vbv-bufsize=${ENCODING_RATE_X265}:vbv-maxrate=${ENCODING_RATE_X265}:bitrate=${ENCODING_BUFFER_SIZE_X265} \
    -c:a copy \
    -c:v libx265 \
    -preset ${PRESET} \
    ${RESCALE_OPTIONS} \
    ${OUTPUT_PATH}$
```

# Goldilocks and the Variable Bitrate
Buckle up.

Finding the correct bit rate to encode at is non-trivial and requires experimentation with `-b:v ${RATE}`, `-maxrate ${RATE}`, and `-bufsize ${RATE}`.  `RATE` is specified in Mbs (e.g. `RATE=30` for 30 Mbps). `ffmpeg`'s [documentation on bitrate](https://trac.ffmpeg.org/wiki/Limiting%20the%20output%20bitrate) helps explain the interplay though basicaly says "go experiment until you find something that works".

That said, bulk conversion of 4K 60 FPS videos from a Go Pro was done using the `libx265`-specific settings `bitrate`, `vbv-maxrate`, and `vbv-bufsize`.  These must be specified like so: `-c:v libx265 -x265-params vbv-bufsize=${X265_RATE}:vbv-maxrate=${X265_RATE}:bitrate=${X265_BUFFER_SIZE}`.  `X265_RATE` and `X265_BUFFER_SIZE` are specified in 1000's (e.g. `X265_RATE=30000` for 30 Mbps). See this [Reddit post](https://www.reddit.com/r/ffmpeg/comments/7y4wm0/how_to_get_specific_bitrate_in_hevc_encoding/) for additional details.  A comment in the conversion script indicated that the `libx265` outputs looked better, though was not specific.

**NOTE:** `maxrate` and `vbv-maxrate` are **NOT** hard limits and can be exceded.  Set them lower than the target hardware's maximum to give headroom and test, test, test.

# Quicktime is Obnoxious
Quicktime will refuse to play videos unless videos are created with `-tag:v hvc1`.

# Framerate Change
Specifying the framerate is done via `-r <fps>` though it matters where it is placed.