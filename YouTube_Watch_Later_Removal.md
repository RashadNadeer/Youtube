
# YouTube "Watch Later" Automatic Removal Script

This JavaScript script automates the removal of all videos from your "Watch Later" playlist on YouTube. It repeatedly finds the first video, opens its action menu, and clicks the "Remove from Watch Later" option until all videos are removed.

## Usage Instructions

1. **Open YouTube's "Watch Later" playlist**: Go to [YouTube](https://www.youtube.com) and navigate to your "Watch Later" playlist.

2. **Open Developer Console**:
   - **Windows/Linux**: Press `Ctrl + Shift + J`
   - **Mac**: Press `Cmd + Option + J`

3. **Paste and Run the Code**: Copy the code below, paste it into the console, and press `Enter` to run.

    ```javascript
    const interval = setInterval(function () {
        // Select the first video in the playlist
        const video = document.querySelector('ytd-playlist-video-renderer');

        if (video) {
            // Open the action menu for this video
            const actionMenuButton = video.querySelector('#primary button[aria-label="Action menu"]');
            if (actionMenuButton) {
                actionMenuButton.click();

                // Look for the "Remove from" option in the action menu
                setTimeout(() => {
                    const removeOption = document.evaluate(
                        '//span[contains(text(),"Remove from")]',
                        document,
                        null,
                        XPathResult.FIRST_ORDERED_NODE_TYPE,
                        null
                    ).singleNodeValue;

                    if (removeOption) {
                        removeOption.click();
                        console.log("Video removed from playlist.");
                    }
                }, 300); // Allow time for the menu to open
            }
        } else {
            // No videos left in the playlist, stop the interval
            clearInterval(interval);
            console.log("All videos removed from the playlist.");
        }
    }, 1000);
    ```

## How It Works

- **Repeating Action**: The code uses `setInterval`, which repeats every 1000 milliseconds (1 second) to check and remove each video.
- **Finds Each Video**: The first video in the "Watch Later" list (`ytd-playlist-video-renderer`) is selected each time.
- **Opens Action Menu**: The script finds and clicks the action menu button using `aria-label="Action menu"`.
- **Clicks "Remove from Watch Later"**: The `XPath` selector locates the "Remove from" option and clicks it to remove the video.

## Notes

- The script will continue to run, removing one video at a time until the "Watch Later" playlist is empty.
- **Stop the Script**: To stop the script manually, refresh the page or close the Developer Console.

### Disclaimer
This script is for personal use to manage YouTube playlists and may be affected by future YouTube updates.

---
