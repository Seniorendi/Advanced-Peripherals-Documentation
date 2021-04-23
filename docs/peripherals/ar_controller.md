# AR Controller
<!--!!! picture inline end
    ![Header](https://srendi.de/wp-content/uploads/2021/03/Chat-box-e1617224333272.png){ align=right }-->

The AR Controller is used to control your AR Goggles wirelessly. You can draw anything you wish into an overlay that will be visible as long as you're wearing the goggles.

!!! hint
    To link your goggles to an AR Controller, right click it with them in your hand. Multiple Goggles can be linked to one controller.

##Functions
While the controller is in relative mode, it interprets all coordinates as if they were on a virtual screen the size you specified, and then scales them according to your screen size.

All color values are hexadecimal color codes (for example ```0xff00ff```)
| Function | Returns  | Description |
|------------|--------------|-------------|
| isRelativeMode()  | boolean\[, int, int\] | Returns true and the size of the virtual screen if relative mode is active, or just false if it isn't |
| setRelativeMode(boolean enabled\[, int virtualScreenWidth, int virtualScreenHeight\])  | | Activates or deactivates relative mode. Requires virtual screen width and height if it's being enabled. |
| drawString(string text, int x, int y, int color) | | Draws the given string to the specified position and the specified color. |
| drawCenteredString(string text, int x, int y, int color) | | The same as ```drawString()```, but centers the string horizontally around the specified position. |
| drawRightboundString(string text, int x, int y, int color) | | The same as ```drawString()```, but the string is positioned with its right end at the specified position. |
| horizontalLine(int minX, int maxX, int y, int color) | | Draws a horizontal line in the given color from minX to maxX at vertical y. |
| verticalLine(int x, int minY, int maxY, int color) | | Draws a vertical line in the given color from minY to maxY at horizontal x. |
| fill(int minX, int minY, int maxX, int maxY, int color) | | Fills a rectangle with the given color from the corner minX, minY to maxX, maxY. |
| fillGradient(int minX, int minY, int maxX, int maxY, int colorFrom, int colorTo) | | Draws a rectangular gradient from colorFrom to colorTo with the given corners. |
| clear() | | Clears the entire canvas. |

Everything that's painted onto the canvas remains there until ```clear()``` is called, however, it might be repositioned if relative mode is toggled on or off.

!!! hint
    Use negative coordinates to specify an x value from the right end of the screen or a y value from the bottom!

##Example
Olfi01 made a simple script that shows the current date and time in the top right corner of the screen and updates every second.
```lua
controller = peripheral.wrap("left") -- Defines the controller to the left of the computer
controller.setRelativeMode(true, 1600, 900) -- Convenient Aspect ratio for most screens
while true do
  local timer = os.startTimer(1)
  local event, id
  repeat
    event, id = os.pullEvent("timer")
  until id == timer
  controller.clear() -- If you don't do this, the texts will draw over each other
  controller.drawRightboundString(os.date(), -10, 10, 0xffffff)
end
```

##Changelog/Trivia

//TODO: add implementation version