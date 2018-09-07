# Poles1
#### 1. Laser data classification and grouping

test
==============

https://www.youtube.com/watch?v=JfvIN4HiM9s&feature=youtu.be&list=RDJfvIN4HiM9s&t=82

<dl>      
  <iframe id='test1' name='part1' width="1062" height="597" src="https://www.youtube.com/embed/CVNTzl544y0?start=225&end=268;rel=0&amp;showinfo=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
    </div> </dl>


.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube.com/watch?v=JfvIN4HiM9s&feature=youtu.be&list=RDJfvIN4HiM9s&t=82 frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
test2
==============
https://youtu.be/2zjLBWnZGTU?t=115

#### 2. Definition of sample objects
#### 3. Creation of cell elements
#### 4. poles with the Find Poles tool





Basic Training TerraScan, TerraModeler, TerraPhoto, TerraMatch / 3 days
==============

#### Training data sets
##### 1. TerraScan, TerraMatch, TerraModeler, TerraPhoto : Jyväskylä ALS data set
* laser data: 21.5.2011, raw data in UTM 35 N, 'ellipsoidal' heights,
* density about 23 points/m2
* images from other flight: 23.5.2012, altitude ca. 850 m, data in UTM 35 N
* trajectory information in text file,  coordinates in GK 26, orthometric heights
##### 2. ALS calibration : Calib data set
Overview user interfaces
  * main menu TScan, TPhoto
  * main tool bar TScan, TPhoto, TModeler, TMatch   
#### Boresight calibration of the scanner system (calibration data set)
* separate training part with 'Calib' data set
#### Set up a project in TerraScan
Coordinate system settings and transformations
  * settings for coordinate systems
     * activate Finnish `ETRS-TM35GK and ETRS GK and UTM North zone 35`
     
  ![image](img/screenshot.png)
  ![image](img/screenshot2.png) 
  
  * define transformation
     * projection change, `UTM 35 → GK 26, modify: xyz`
     
![image](img/screenshot3.png)
![image](img/screenshot4.png)

#### Import trajectories
   * raw file formats, format definition in settings
   * set directory (trajectory/)
![image](img/screenshot5.png)
   * import raw file (trajectory_raw/)
      * text file, format: time northing easting elevation roll pitch heading (TYXZRPH also implemented)
      * angle = degree (depends on raw trajectory file), adjust heading on if transformation from lat/lon to projection system, thinning normally on (`0.10 m/deg for airborne`)
 ![image](img/screenshot6.png)
      
#### Cut or split turnarounds of trajectories
   * for matching and tscan processing tasks
   * several options to split trajectories automatically or manually
      * draw polygon around project area, delete outside polygon
   * draw into design


![image](img/screenshot2.png)


    • save tie lines in tielines.til
    

![image](img/screenshot.gif)


![GIF](img/screenshot.gif)

