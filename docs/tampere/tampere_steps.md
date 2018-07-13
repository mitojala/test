# Tampere

#### 1. Open design file \introduction\dgn\tampere.dgn.
#### 1. Start 'Define Classes' and open point classes \mission\tampere.ptc.
#### 2. Run 'File / Read points' to read \laser01\tampere.fbi into memory.
#### 3. Practise viewing tools and get familiar with data set.
#### 4. Select 'Tools / Macro' to open macro window.
#### 5. Open macro \macro\01_isolated_low_ground_below.mac and run on loaded points.
#### 6. Open macro \macro\02_height_from_ground_normals.mac and run on loaded points.
#### 7. Open mission \mission\tampere.mis.
#### 8. Select 'Images / Load list' to read image list \mission\images_final.iml.
#### 9. Run 'Tools / Extract color from images' using:
* For class: `Any class`
*   Color source: `Raw images & color points`
* Channels: `4`
* Cpt file: `\mission\tampere_four_channels.cpt`
*  Image numbers: `Compute -- do not store`
* Use images: `Closest in xy`
* Footprint: `1.0 pixels`
#### 10. View point colors.
#### 11. Set values in 'Settings' tool and 'Point display' category:
* Normalized difference: `0.000`
* Visible band difference: `0.050`
#### 12. View vegetation index coloring.
#### 13. Open macro \macro\03_vegindex_best_match.mac on loaded points.
#### 14. Run 'Vectorize Buildings' using:
* Roof class: `6 - Building`
* User roof class: `None`
* Lower classes: `2 - Ground`
* Process: `Active block`
* Use polygons: `Do not use`
* Maximum gap: `2.0 m`
*   Planarity tolerance: `0.150 m`
* Increase tolerance: `0.250 m`
* Minimum area: `10.0 m2`
* Minimum detail: `2.0 m2`
* Max roof slope: `75.0 deg`
