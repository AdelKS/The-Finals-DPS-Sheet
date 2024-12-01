
# The Finals DPS Sheet

This repo holds weapon statistics / damage / reload information of some of the guns in The Finals

Hopefully The Finals will officially publish the actual configuration
used for the guns so we don't have to do that by hand...

![stats](/stats.png)

Note:
- The Light's Bow stats have not been calcualted in the same way as the other guns: it's an average over many shots while trying to shoot right at max charge

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
