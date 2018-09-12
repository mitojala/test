

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
##### Set up a project in TerraScan
Coordinate system settings and transformations
  * settings for coordinate systems
     * activate Finnish `ETRS-TM35GK and ETRS GK and UTM North zone 35`
     
  ![image](img/screenshot.png)
  
  ![image](img/screenshot2.png) 
  
  * define transformation
     * projection change, `UTM 35 → GK 26, modify: xyz`
     
![image](img/screenshot3.png)

![image](img/screenshot4.png)

##### Import trajectories
   * raw file formats, format definition in settings
   * set directory (trajectory/)
   
   ![image](img/screenshot5.png)

   * import raw file (trajectory_raw/)
      * text file, format: time northing easting elevation roll pitch heading (TYXZRPH also implemented)
      * angle = degree (depends on raw trajectory file), adjust heading on if transformation from lat/lon to projection system, thinning normally on (`0.10 m/deg for airborne`)
      
      ![image](img/screenshot6.png)
      
##### Cut or split turnarounds of trajectories
   * for matching and tscan processing tasks
   
        * draw into design
      
        ![image](img/screenshot7.png)         
             
        ![image](img/screenshot8.png)
                                                                   
   * several options to split trajectories automatically or manually, here we will use a polygon
      
      * draw polygon around project area
      
      * select the polygon
      
     ![image](img/screenshot10.png)
     
      * pick delete outside polygon
      
     ![image](img/screenshot13.png)    
        
     ![image](img/screenshot11.png)






    • save tie lines in tielines.til
    

![image](img/screenshot.gif)


![GIF](img/screenshot.gif)

