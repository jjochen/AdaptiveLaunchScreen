# Adaptive iOS launch screen

It's not easy to use a launch screen storyboard that uses different images for iPad in portrait and landscape mode. 
For the iPhone this can be solved using hight and width classes. 
But as iPads have regular height and regular width it's not possible to determine the orientation of the device within the launch screen storyboard.

This iOS project has an adaptive launch screen storyboard using spacer views that position the correct image in the visible area and move the other one off screen.

You can NOT provide different images for different screen sizes (iPhone 4, iPhone X, ...), but if you want **different images for iPhone and iPad** and **different images for portrait and landscape** this solution is for you.

[![Constraints in Interface Builder][1]][1]

The important constraints are
```
PortraitSpacer.width ≤ 5 × view.width
PortraitSpacer.width ≤ 5 × view.height

LandscapeSpacer.width ≥ 5 × view.width
LandscapeSpacer.width ≥ 5 × view.height

PositionSpacer.width = 5 × view.width
```
where `view.width` and `view.height` are the main view's width and height.

The `PortraitSpacer` positions the portrait image at `5 × min(view.width, view.height)`, 
the `LandscapeSpacer` positions the landscape image at `5 × max(view.width, view.height)`, 
and the `PositionSpacer` has the same width as `PortraitSpacer` in portrait mode and the same width as `LandscapeSpacer` in landscape mode.

We multiply everything with 5 so the two images do not overlap. This works for all devices where the following is true
```
5 × min(view.width, view.height) + max(view.width, view.height) ≤ 5 × max(view.width, view.height)
```
In landscape mode this would mean
```
5 / 4 ≤ view.width / view.height
```
which is the case for all current devices: iPad has the lowest aspect ratio with 4:3 which is still greater than 5:4.

You can then of course configure images per device (iPhone, iPad) in the asset catalog.  


  [1]: https://i.stack.imgur.com/fXN9X.png
