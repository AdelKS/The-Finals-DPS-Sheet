
# The Finals DPS Sheet

This repo holds weapon statistics / damage / reload information of some of the guns in The Finals

Hopefully The Finals will officially publish the actual configuration
used for the guns so we don't have to do that by hand...

![stats](/stats.png)

Note:
- The Light's Bow stats have not been calcualted in the same way as the other guns: it's an average over many shots while trying to shoot right at max charge

## How were these numbers computed ?

Technical notes:
- Recording 200fps videos in practice range (game's FPS > 300) then counting the frames. See folder [videos](./videos/)
  - Frame numbers were added to the videos to simplify the counting ([taken from here](https://www.reddit.com/r/VideoEditing/comments/ibcm8k/counting_number_of_frames_between_two_events_in/))
    ```shell
    ffmpeg -i <original-video> -vf "drawtext=font='Source Code Pro': text='%{frame_num}': start_number=1: x=(w-tw)/2: y=h-(2*lh): fontcolor=black: fontsize=20: box=1: boxcolor=white: boxborderw=5" <video-with-frames> -hide_banner
    ```
- A bullet is considered as fired on the first video frame where the number of bullets decreases by 1, as shown in the bottom right of the screen (where you see the mag size and number of bullets remaining): those are the frames used to measure bullets/sec and reload times.

Readings:
- damage/bullet: visually calculated by counting the number of squares of HP (25 each) the 350 HP dummy in the practice range loses.
  - To improve precision: shoot as many bullets as possible but right before the dummy dies. Prefer stopping on an integer number of remaining 25HP blocks.
- bullets/sec: computed by dividing
    - the time interval between the frame where the first bullet is fired and the frame where the bullet number reaches 0.
    - the number of bullets in the mag
- Reload times
  - Empty mag reload time is the time interval between the frame the bullet number reaches 0 and the frame where the first bullet of the new mag is fired.
  - Non-emtpy mag reload time is counted from the first frame the last bullet is fired before reloading a non-emtpy mag, to the first frame the first bullet of the new mag is fired.

See the file [The Finals DPS](./The%20Finals%20DPS.ods) for the actual readings from the [videos](./videos/)
