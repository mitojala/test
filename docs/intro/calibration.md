**Boresight calibration (calibration data)** / \< 0.5 day
---------------------------------------------------------

### Preparing the data

-   open design file ***calib.dgn*** and start TerraScan and TerraMatch
-   open files from ***laserraw/***, delete data outside calibration
    area
-   activate coordinate systems UTM North, zones 32-3x
-   set trajectory directory to ***/trajectory***
-   import trajectories from ***/trjraw***

    -   WGS 84: UTM 32 Ntime: GPS seconds-of-week
    -   input angles: TopEye radiansadjust heading: on
    -   thin positions: xyz 0.1 m, angles 0.1 deg

-   draw trajectories into design file
-   deduce using time
-   save points as ***laser/calib.fbi***
-   check laser data in section views

-   Classify ground per flightline (required for tie lines, if terrain
    is not open)

    -   use prepared macro calib.mac, process flightlines separately
    -   run on loaded points

-   Compute distance to flightline average Z
-   Visualize distance coloring to see misalignment

    -   -0.5 ... +0.5 m, display one flightline at the time in top view
    -   section views with flightline coloring

### Tie line measurement

-   define tie lines

    -   laser time gap: 2 s max error xy: 2.0 mmax error z: 1.0 mfit
        tolerance: 0.10 m
    -   ground class: 2

-   view 1: view point color by elevation
-   search tie lines

    -   loaded pointsignore first/intermediate echos
    -   spacing 5 mfind surface linesslope direction
    -   length: 3.5 mdepth: 1 mmax angle: 1 deg

-   find worst, check validity worst tie line
-   save tie lines as ***calib.til***

### Find boresight paramaters

-   find tie line match

    -   airborneactive tielineswhole data setcombined solution
    -   roll, pitch, heading and mirror scale

-   save result as ***calib\_hrps.tms***
-   apply corrections on loaded tie lines and loaded points
-   find worst to check for error tie lines

    -   might be one or two under shrubs which are not really good →
        delete tie lines

-   restore observations from ***calib.til***
-   run find tie line match again, overwrite ***calib\_hrps.tms***
-   close points and load ***calib.fbi***
-   apply corrections on loaded tie lines and loaded points
-   check output report from tie lines

-   Compute distance to flightline average Z
-   Visualize distance coloring to see misalignment

    -   -0.5 ... +0.5 m → equal distribution of distance colors
    -   -0.1 ... +0.1 m → fl 1 and 2 seem to be a bit worse than 3 and 4
        → no calibration problem anymore

=\> result of calibration: HRP (mirror scale) correction angles for
laser data

=\> correction can be applied when generating the project point cloud
(with scanner software) or as a first workflow step in Terrasolid
software
