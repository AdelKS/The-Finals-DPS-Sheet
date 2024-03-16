
# The Finals DPS Sheet

This repo holds weapon statistics / damage information of some of the guns in The Finals

Hopefully The Finals will officially publish the actual configuration
used for the guns so we don't have to do that by hand...

## Update 2.0.0

```
Gun     bullets/sec |      body shots       |      head shots
-------------------------------------------------------------------
                    |  damage/bullet  DPS   |  damage/bullet   DPS
93R     9           |  24             216   |  37              333
V9S     7.5         |  37             278   |  55              413
XP-54   14.7        |  19             279   |  28              412
M11     17.1        |  17             291   |  24              410
FCAR    9.6         |  25             240   |  38              365
FAMAS   8.6         |  23             198   |  35              301
AKM     10.3        |  21             216   |  30              309
```

Note:
- The `V9S` follows the click speed of the player, so this is my own CPS

## How were these numbers computed ?

See the file [The Finals DPS](./The%20Finals%20DPS.ods):
- damage/bullet: visually calculated by counting the number of squares of HP (25 each) the 350 HP dummy in the practice range loses.
  - To improve precision: shoot as many bullets as possible but right before the dummy dies. Prefer stopping on an integer number of remaining 25HP blocks.
- bullets/sec: by recording a 200fps video in practice range (game's FPS > 300) then counting the frames. See folder [videos](./videos/)
  - Frame are counted from the first frame where the bullet number decreases from full mag (bottom right of the screen) to the first frame where the bullet number reaches 0.
  - Frame numbers were added to the videos to simplify the counting ([taken from here](https://www.reddit.com/r/VideoEditing/comments/ibcm8k/counting_number_of_frames_between_two_events_in/))
    ```shell
    ffmpeg -i <original-video> -vf "drawtext=font='Source Code Pro': text='%{frame_num}': start_number=1: x=(w-tw)/2: y=h-(2*lh): fontcolor=black: fontsize=20: box=1: boxcolor=white: boxborderw=5" <video-with-frames> -hide_banner
    ```
