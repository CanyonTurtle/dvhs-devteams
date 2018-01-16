# Common Spacing Distances - Documented!

Remember to use a [Spacing Calculator](articles/external.md?id=spacing-calculator) in conjunction with this info, to really speed up the spacing process on the fly!

### Inward-facing C-Channels, Cross-braced ] [
This configuration is for when 2 C-channels are joined by another channel or plate running across, and the C-channels have the largest face pointing towards the other C-channel. This is the distance on the inside, between the faces.

`Distance(inches) = (CrossLength - 1) * 0.5 - 0.6`

`CrossLength` means the # of holes of the joining metal running across both C-channels.

> The `- 0.6` comes from the horizontal distance from the center of the top hole to the outside face being 0.3", so this is multiplied by 2.

| CrossLength (# holes) | Distance (inches) |
|-----------------------|-------------------|
| 3                     | 0.4               |
| 4                     | 0.9               |
| 5                     | 1.4               |
| 6                     | 1.9               |
| 7                     | 2.4               |
| 8                     | 2.9               |

### Same-Direction-facing C-Channels, Cross-braced [ [
Same as above, but the C-channel main face is pointed both in the same direction, either both right or both left.

`Distance(inches) = (CrossLength - 1) * 0.5 - 0.062`

> The `-0.062` is because one side is + 0.238" from the center of the hole to the inside face, and the other is 0.300" from the center to the outside face, so the addition is -0.062.

| CrossLength (# holes) | Distance (inches) |
|-----------------------|-------------------|
| 3                     | 0.938             |
| 4                     | 1.438             |
| 5                     | 1.938             |
| 6                     | 2.438             |
| 7                     | 2.938             |
| 8                     | 3.438             |


### Outward-facing C-Channels, Cross-braced [ ]
When the C-channel main faces are pointed away from each other.

`Distance(inches) = (CrossLength - 1) * 0.5 + 0.476`

> The `+0.476` is because both sides are + 0.238" from the center of the hole to the inside face, so multiplying that by 2 yields the value.

| CrossLength (# holes) | Distance (inches) |
|-----------------------|-------------------|
| 3                     | 1.476             |
| 4                     | 1.976             |
| 5                     | 2.476             |
| 6                     | 2.976             |
| 7                     | 3.476             |
| 8                     | 3.976             |
