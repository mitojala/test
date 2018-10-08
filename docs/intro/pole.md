
Basic Training for ALS Data producers, Bundle : TerraScan, TerraModeler, TerraPhoto, TerraMatch / 3 days
==============

In this training project, we will consider you as an aerial lidar data producer. We will go through all steps from boresight calibration to end products using 4 of our products : TerraScan, TerraModeler, TerraPhoto, TerraMatch.

## Training data sets

###  Jyväskylä ALS data set
* laser data: 21.5.2011, raw data in UTM 35 N, 'ellipsoidal' heights,
* density about 23 points/m2
* images from other flight: 23.5.2012, altitude ca. 850 m, data in UTM 35 N
* trajectory information in text file,  coordinates in GK 26, orthometric heights
### ALS calibration : Calib data set
Overview user interfaces
  * main menu [TScan](http://www.terrasolid.com/guides/tphoto/mw.php), [TPhoto](http://www.terrasolid.com/guides/tscan/index.html?intromainwindowmenucommands.php)
  * main tool box [TScan](http://www.terrasolid.com/guides/tscan/intromaintoolbox.php)
  * general tool box [TPhoto](http://www.terrasolid.com/guides/tphoto/tboxgeneral.php), [TModeler](http://www.terrasolid.com/guides/tmodel/tbox_general.php), 
  * [TMatch tool box](http://www.terrasolid.com/guides/tmatch/match-tool-box.php), [TMatch tie lines box](http://www.terrasolid.com/guides/tmatch/tie-line-tool-box.php)
  
### 3. Project additionnal documents
* Project DGN file based on a 3d mm seed file, contains project limit, 2d objects and level definition
* Point class definition file

## Set up a project in TerraScan

The [project](http://www.terrasolid.com/guides/tscan/introworkingwithprojects.php) in Terrascan is a metadata file allowing you to associate locations to your data, your trajectories etc.. and some other parameters so that that can be saved, transferred, reloaded and documented more easily.
As soon as you start to work properly in a production project, it should be defined. 

A project requires most of the time to set 5 elements :
 1. Coordinate System settings
 2. Raw data
 3. Trajectories
 4. Blocks
 5. Point class
 
 We will first prepare all these settings on a test subset of points before formally defining the project.
 
 --- 
 _Note :_
 Some of them can use the default parameters or be ignored on a particular small project 
---

Open the DGN file in `<trainingFolder>/dgn` via microstation so that we can start.

### Project preparation

#### Coordinate system settings and transformations


The first step for every process in TerraScan consists in setting the coordinate system. As trajectories and/or end product might be in different coordinate systems, we will show you how to activate a coordinate system and how to set a transformation. 

  * [settings for coordinate systems](http://www.terrasolid.com/guides/tscan/tooldefinecoordinatesetup.php)
     * activate Finnish `ETRS-TM35GK and ETRS GK and UTM North zone 35`
     
  ![imsetCoordSys1](img/screenshot.png)
  
  ![setCoordSys2](img/screenshot2.png) 
  
  * [define transformation](http://www.terrasolid.com/guides/tscan/introcoordinatetransformations.php?zoom_highlightsub=transformation)
     * projection change, `UTM 35 → GK 26, modify: xyz`
     
![defTransf1](img/screenshot3.png)

![defTransf2](img/screenshot4.png)


##### Read a subset of points

Your coordinate system being set, it is time to visualize and get familiar with your raw data.

 * In the main menu, go to [`File/Read points`](http://www.terrasolid.com/guides/tscan/mwreadpoints.php?zoom_highlightsub=read+points)

![readPoints](img/screenshot14.png)

* Be sure to select the right transformation we defined earlier and the subset factor (here 1 out of 10 points is read)

![pointsParameters](img/screenshot15.png)

#### Trajectories

A lot of TerraScan and TerraMatch tools, specially during the matching process, need the flight trajectories.

##### Import Trajectories

* raw file formats, [format definition](http://www.terrasolid.com/guides/tscan/setfileformats_usertrajectoryformats.php) in settings
* [set directory (trajectory/)](http://www.terrasolid.com/guides/tscan/toolmanagetrajectories.php) 
   
   ![trajDirectory](img/screenshot5.png)

   * import raw file (trajectory_raw/)
      * text file, format: time northing easting elevation roll pitch heading (TYXZRPH also implemented)
      * angle = degree (depends on raw trajectory file), adjust heading on if transformation from lat/lon to projection system, thinning normally on (`0.10 m/deg for airborne`)
      
      ![image](img/screenshot6.png)
      
##### Cut or split turnarounds of trajectories
   * For matching and tscan processing tasks
   
      * [Draw into design](http://www.terrasolid.com/guides/tscan/trjdrawintodesign.php) allows us to visualize the trajectories by creating lines in the active level
      
        ![drawIntoDesign1](img/screenshot7.png)         
             
        ![drawIntoDesign1](img/screenshot8.png)
                                                                   
   * Several options to [split trajectories automatically or manually](http://www.terrasolid.com/guides/tscan/tool-pulldown-menu.php), here we will [use a polygon](http://www.terrasolid.com/guides/tscan/trjdeletebypolygons.php).
      
      1. Draw polygon around project area
      
      2. Select the polygon
      
     ![polygonSelection](img/screenshot10.png)
     
      3. Pick delete outside polygon
      
     ![deleteOutside1](img/screenshot13.png)    
        
     ![deleteOutside2](img/screenshot11.png)

      
   * To check that the split when right and that the trajectories and points timestamps are coherent, we will deduce from which trajectory points come based on the timestamps. 
   
     1. For this, on the main bar, go to [`Line/Deduce using time`](http://www.terrasolid.com/guides/tscan/mwdeduceusingtime.php)

     ![deduceTime](img/screenshot16.png)  

     2. Then we will [display](http://www.terrasolid.com/guides/tscan/mwdisplaymode.php) the points based on their trajectories
     
   ![displayPoints1](img/screenshot18.png)  
    
    
   ![displayPoints2](img/screenshot19.png)
    
   
   ![displayPoints3](img/screenshot17.png)     
    
 * At this stage, you can get familiar with the data through the [section](http://www.terrasolid.com/guides/tscan/tboxviewlaser.php) and display tools.
 
    ![section](img/screenshot20.png)   
    
 ---
 _Warning_ : 
 For the section tool, please follow the instruction on the bottom left of your screen.
 ---
 
 ---
 _Note_ :
 Our subset is ready and you checked that the trajectories are well related.
 ---
 
 #### Block Limit Definition
 
To work properly, we will divide our project area into different [blocks](http://www.terrasolid.com/guides/tscan/prjpmblock.php). It will allow to test in one block and then execute processes on every blocks independently. That way if an error arises on a specific block, it will not impact the others. The number of points in memory at a time will also be lower.

There are different ways to design blocks, here we will draw lines dividing our project area shape in three parts.

* To create these lines, active the level 9 and use microstation smart line tool

 ![section](img/screenshot21.png)
 
 ![section](img/screenshot22.png)   

 * Once the lines created, we pick the [`Design Block Boundaries`](http://www.terrasolid.com/guides/tscan/tooldesignblockboundaries.php)
 
 ![section](img/screenshot23.png)
 
  * `Line level` contains user defined block division
  * blocks will be drawn to `Shape level`
  * number of points inside blocks will be drawn to `Label level`
  
 ![section](img/screenshot24.png)  
 
 * If the selected levels are active, you should be able to see the result
  
  ![section](img/screenshot25.png)  
  
  #### Point Class definition
  
In Terrascan, you can create and save [your own point class files](http://www.terrasolid.com/guides/tscan/tooldefineclasses.php). Here we will load an existing one:
`<trainingFolder>/classes.ptc`
 
![section](img/screenshot26.png)  

 
 ---
 _Note_ : 
 We now have trajectories, points, blocks, and point classes checked. We will be able to formally define the project
 ---
 
### Project Formal Definition


The project related tools can be found in the [main tool box](http://www.terrasolid.com/guides/tscan/intromaintoolbox.php).

![section](img/screenshot27.png)  

![section](img/screenshot28.png)

![section](img/screenshot29.png)

Here you have to select the attributes you want to be saved with your project. If you do not pick Color and then add color to your points, then the color will be lost after saving and closing the project.

![projectAttribute](img/screenshot30.png)
 
 ---
 _Warning_ : 
 The storage format is here really important. Only the `Fast Binary`, the default one, supports all the attributes!
 ---
 
 You can chose the location of different important project folders. For your first project, the closer to the default parameter would be the better.
 
 For the block size. We went through the block definition earlier so we will not use these default parameters, you can let them as they are.
 
 #### Saving the project
 
 As the project definition is done, we will save it. This has to be done after every big step.
 
 ![Saveproject](img/screenshot37.png)

 ---
 _Note_ : 
 You can save the project anywhere but, as by default the data will be saved in the same folder, we prefer to use a folder name like Laser01, the number referring to your project step.
 ---
 

![Saveproject2](img/screenshot38.png)
 
#### Creating the Blocks

The block boundaries have already be drawn, we just need to select them and to [declare them as the project blocks](http://www.terrasolid.com/guides/tscan/prjaddbyboundaries.php)

![Saveproject2](img/screenshot31.png)

![Saveproject2](img/screenshot32.png)

![Saveproject2](img/screenshot33.png)

To check that it went well, use the project tool to draw them onto the dgn.

![Saveproject2](img/screenshot34.png)

#### Points import

As you can see on the project window, no file is associated with the blocks. To do this you need to [import the point files into the project](http://www.terrasolid.com/guides/tscan/prjimportpointsintoproject.php). This will create fbi files in the project folder, maybe transforming the coordinate system if asked, and write the blocks metadata into the project file (*.prj).

![Saveproject2](img/screenshot39.png)

![Saveproject2](img/screenshot40.png)

 ---
 _Trick_ : 
 You can import files stored in different folders with the "add" option
 ---

![Saveproject2](img/screenshot41.png)

In this last window, we select the transformation as our point cloud is not in the same coordinate system as our vectors.
Please use the transformation we created earlier `UTM 35 → GK 26`

 ---
 _Note_ : 
 Using `Deduce using time` here save us one step by associating the points to their respective trajectories, it is based on timestamp
 ---

Your blocks are now ready!


## Boresight calibration of the scanner system using [TerraMatch](http://www.terrasolid.com/guides/tmatch/index.html)

### Data preparation : Classification

To help the matching tools, manual or automatic, we will here classify the data. By example, during the [tie lines search](http://www.terrasolid.com/guides/tmatch/search-tie-lines.php?zoom_highlightsub=tie+lines), it speeds up the calculation if you compare only the points of some classes.

#### Macro : automatic steps

The [macro files](http://www.terrasolid.com/guides/tscan/intromacroactions.php?zoom_highlightsub=macro) are text files defining a list of tasks with their parameters. The use of those macros helps a lot, specialy on big project because they can be applied on a set of blocks or on a set of blocks once they are validated. You can also distribute their execution between computers using [TerraSlave](http://www.terrasolid.com/guides/tscan/terraslavequickguide.php?zoom_highlightsub=terraslave). 

##### A look at the steps : 01_prepare_match.mac

Let's go through the steps in the macro prepared for this project. To do this, we use Tools/Macros... in the main menu. 

![Macro1](img/screenshot42.png)

![Macro2](img/screenshot43.png)

![Macro3](img/screenshot44.png)

As you can see, our preprocessing consists in 5 steps. We will now explain them in details.

* Filter water points
The first steps consists in filtering the water points, we do that because they will not help to improve the matching and will slow the calculation.

We could use the intensity return or color on some dataset to do it but here, the water area have already be vectorized in our DGN (level 12). So we apply the classification tool : [By polygons](http://www.terrasolid.com/guides/tscan/crbypolygons.php?zoom_highlightsub=classify+by+polygons) with the macro step [Classify points](http://www.terrasolid.com/guides/tscan/maclassifypoints.php) and set their classification from 1 (Default) to 9 (Water).  

![ClassbyPolygons](img/screenshot45.png)

* Filter low points

There are always some errors in the points with isolated incoherent elevations. This time we will use the classify [Low points](http://www.terrasolid.com/guides/tscan/crlowpoints.php) tool to get rid of them. We sometimes also use the [Isolated points](http://www.terrasolid.com/guides/tscan/crisolatedpoints.php) tool. This step will limit the errors on the ground classification steps.

![ClassLowPoints](img/screenshot46.png)

* Ground processing

For ALS with low density, the [ground classification](http://www.terrasolid.com/guides/tscan/crground.php) tool works really well. Ground definition is a really important aspect of Lidar processing, it is not only used to get end products like the one you can produce with TerraModeler, but also to classify other elements/objets and to do the matching. You should look through the user guide to properly understand how the tool works.

![ClassGround](img/screenshot47.png)

 ---
 _Note_ : 
 After the macro processing, you will have to go through the points and improve the ground manually if needed.
 ---

* Classify by height from ground : High vegetation 

All the matchimg corrections can not be easily found using only the ground. We will also need some aerial planar surfaces such as wall or building roofs. To get these aerial points, we will first put them in the high vegetation class. It will lower the amount of points during the planarity check algorithm. In general, always try to minimize the amount of points when using complex and ressource demanding features of TerraScan.

The tool used here is classify [Height from ground](http://www.terrasolid.com/guides/tscan/crbyheigthfromground.php).

![ClassHeightFromGround](img/screenshot48.png)

As you can see, here the points from default class(1) higher than 2 meters are put to the High Vegetation class(5)

* Classify building roofs

Now that all the high points are in the high vegetation class, we will classify specificly the roofs through a dedicated tool : [Classify buildings](http://www.terrasolid.com/guides/tscan/crbuildings.php). Beware of the name, other tools can help to classify the walls, this one is for the roofs (easier to get with ALS).

![ClassBuildings](img/screenshot49.png)

Its parameters are pretty straight forward.

##### Processing the macro

![runMacroTool](img/screenshot50.png)

* Test run : Step by step

First we will do a test run on a **loaded block** step by step using the **Step** button. It will allow you to look at the point cloud evolution (using a display by Class and some sections) and see if a major problem happens. Once this test run is finished, you can [close the loaded points](http://www.terrasolid.com/guides/tscan/mwclosepoints.php) **without saving them**.

* Project run

This time we will run the macro on the whole project. Two points are importants :
 * First, **in the macro definition window**, check the `Process lines separately`. Indeed, we want to compare the ground and the roofs between the lines to get the correction values.
 
![macroDefWin](img/screenshot51.png)
 
 * Second : **in the run macro window**, use points from neighboring blocks so that there won't be any differences in classification between blocks (block edge effects).
 
![runMacroWind](img/screenshot52.png)

#### Lines Mismatch Visualization

* Compute distance

To visualize the differences between the line, we will use the [Compute distance](http://www.terrasolid.com/guides/tscan/mwcomputedistance.php) tool, in the main window (Tools/Compute distance...).

 ---
 _Note_ : 
 Compute distance is a really important tool used in a lot of processes like [Grouping](http://www.terrasolid.com/guides/tscan/mwpmgroup.php)
 ---

![computeDistance](img/screenshot53.png)

![computeDistance](img/screenshot54.png)

Using the `Line average z` parameter allows us to get a bigger value associated with the points the further appart are the lines. It will be of a huge help.

* Distance display

In the Display mode, we will use the distance we just prepared. Be carefull to follow the settings :

* min value `-0.15` m
* max value `0.15` m
* use depth
* class : `ground and building`
* apply to `view 1`

![displayDist1](img/screenshot55.png)
![displayDist2](img/screenshot56.png)
![displayDist3](img/screenshot57.png)
![displayDist4](img/screenshot58.png)

We set the Display by flight line on view 2 and then we can use the section tool see the matching issues.

First example :
![displayMatchDiff1](img/screenshot60.png)

Second example :
![displayMatchDiff2](img/screenshot61.png)

![GIF](img/screenshot.gif)

* Statistics : [measure match](http://www.terrasolid.com/guides/tmatch/measure-match.php)

To get a global idea about the mismatch, the measure-match tool can be used. It generate a report summarizing the differences between a mean surface and the one generated from each line. Of course we will use our ground class for the best compararison.

![measureMatch1](img/screenshot62.png)

![measureMatch2](img/screenshot63.png)

### Matching

[Two approaches](http://www.terrasolid.com/guides/tmatch/methods-of-line-adjustment.php) are available to do the matching in TerraMatch. The first and "classical" one consists in trying to change parameters to optimize the surfaces differences (same as in measure match). This approach is now replaced most of the time by a tie lines approach. It consist in finding a fair number of features in the point clouds, generate vectors between the same objects in the different lines and finally minimizing those vectors. This approached have proved to be way faster and more flexible, specially with mobile data where fluctuations can be very frequent. We will follow this approach.

#### Define tie lines

TerraMatch need us to define where to look for common features between the lines. [Define tie lines](http://www.terrasolid.com/guides/tmatch/define-tie-lines.php) is the dedicated tool for this.
Specifying maximum gap between the lines, the point class to use and the other parameters will allow a faster and better result.

![defineTieLines1](img/screenshot65.png)

Here we will set those parameters :
* laser time gap, time difference between different lines at the same location : 10s
* max error xy, maximum difference between lines in horizontal positioning : ´0.30´
* max error z, maximum difference between lines in elevation positioning : ´0.50´
* fit tolerance, estimation of noise level in the data : ´0.12´
* point class : `ground`

![defineTieLines2](img/screenshot64.png)

Now that we have set where TerraMatch should look, we can decide the kind of feature we want to use to generate tie lines. This is done through the tool : [search tie lines](http://www.terrasolid.com/guides/tmatch/search-tie-lines.php?zoom_highlightsub=search+tie+lines).

 ---
 _Note_ : 
The tie lines can also be defined manually!
 ---

![searchTieLines1](img/screenshot66.png)

![searchTieLines2](img/screenshot67.png)

With this setting, we are looking for tie lines in ground surface through the change of slope. A feature will be an area with the same elevation fluctuations. To be more precise, TerraMatch will look for 3m long and 1m large area with the same slope (1 degree deviation) in the different lines.

To get a better calibration, tie lines above ground are important. We will look for them on flat building roofs. As those points are in the building class (6), we need first to update the tie lines settings.

![defineTieLines3](img/screenshot68.png)

The we use again the search tie lines tool, completing the tie line list.

![searchTieLines3](img/screenshot69.png)

 ---
 _Note_ : 
We can check if all tie lines found automatically represent "real features", or at least coherant by using the [find worst](http://www.terrasolid.com/guides/tmatch/find-worst.php) tool in the _Line_ menu and delete tie lines which appear wrong with [delete line](http://www.terrasolid.com/guides/tmatch/delete-line.php).
 ---

The vector list can now be saved.

![saveTieLines](img/screenshot70.png)

#### Find correction parameters

All those vectors are the result of different errors during the acquisition process. Part of them are systematic errors, part of the vectors are from varying issue, like IMU drift or from temporary issue like a bad GPS coverage during a short period of time.

To solve all those problems, wh will go from the most systematic and global errors to the more local ones. The approach would be the same with mobile data but with more local variations.

##### Find boresight parameters

The boresight calibration errora should have been minimized by the calibration flight but there are always some residues. They are born from the delta between the head, roll, pich angled measured and the real ones.

![boreSight](img/screenshot71.png)

TerraMatch will try to find the best delta to apply to these angles to minimize the vector lenght between the features. To calculate a new head, pitch, roll proposition, we use [Find Tie Line Match](http://www.terrasolid.com/guides/tmatch/find-tie-line-match.php).

![findTieLineMatch](img/screenshot72.png)

![findTieLineMatch](img/screenshot73.png)

On our dataset, the calibration was already quite good, we can see that the improved angles are not much different from the original ones, the tie line vector length they would generate would not be much better that the existing ones (comparaison between Starting and Final average mismatchs).

![findTieLineMatch3](img/screenshot74.png)


 ---
 _Warning_ : 
Beware of the `Number of usable observations` part of the report. If you use too few tie lines, the new parameters are not worth much. Their space repartition is also a factor. 
 ---

We will not apply those new parameters.

##### Find inter-lines corrections

We will now try to minimize the mismatch by applying different parameters to each line. Again we will use Find Tie Line Match but this time with Solve for ´individual lines´. As z and roll are the easiest parameters to improve and often the biggest errors, we will try find a delta z and a roll angle for each line which improve the overall coherence between the lines.

![findTieLineMatch4](img/screenshot75.png)

![findTieLineMatch5](img/screenshot76.png)

These parameters improving the mismatch in the tie lines from around 5cm to around 1cm, we will apply them. 

#### Apply corrections

* Correction of the tie lines
To do this, we save the correction file and we use the [apply correction tool](http://www.terrasolid.com/guides/tmatch/apply-correction.php).

![applyCorrection1](img/screenshot77.png)

![applyCorrection2](img/screenshot78.png)

Note that we apply the correction to the tie lines first. This will allow us to see if the correction implied an unwanted local increase of the error despite the better average as we do not have any dispertion indicator. 

* Correction of the points

Finally we can apply the correction to the project points. To pay it safer, we will save the corrected data to a new folder. This will also generate a new project that we will open right after the computation.

![applyCorrection3](img/screenshot81.png)

 * Visualization
 
 After having opened the project in folder laser02 and loaded a block, we can recompute the distance. Using the visualization by distance seen previously, we can judge the improvement.
 
![distBeforeCorr](img/screenshot79.png)

![distAfterCorr](img/screenshot80.png)

Finally, like last time, we will measure the mismatch between the points, as the correction was calculated only based on the tie lines.

![measureMatch3](img/screenshot82.png)

![measureMatch4](img/screenshot83.png)

Our matching is done! Now the classification can start.

## Ground classification and delivery products (TerraScan and TerraModeler)

### Cleaning the dataset : Cut Overlap

Even if we improved the matching between the lines, their overlap create a noise effect and density variation. To solve this issue, we will [cut the overlap](http://www.terrasolid.com/guides/tscan/mwcutoverlap.php), moving the ovelapping points to the overlap class.

#### Cross lines : use when needed

Usually cross lines, which are used for matching, are also removed. There are several ways to identify the cross lines like `display by trajectory` followed by identify on the [manage trajectories window](http://www.terrasolid.com/guides/tscan/toolmanagetrajectories.php). Here we will not completely remove the cross line but use its points only when they are the only ones available on some areas.

To achieve this kind of cleaning, we have, in the manage trajectores window, to set the quality of the cross line to `Poor` before  the cut go ovelap tool.

![lineQuality1](img/screenshot84.png)

![lineQuality2](img/screenshot85.png)

#### Cut by offset : limit overall overlap

Cut overlap by offset is a good tool to improve limit the global overlap. It pick the points from the line with the most vertical angle on an area. The quality of those is most of the time better and the density becomes uniform.

#### Macro implementation

We will apply those two actions through one macro step : [Cut overlap](http://www.terrasolid.com/guides/tscan/macutoverlap.php?). Going through the main window in the tool menu, we create our new macro.
We implement the two actions in two different steps. The will allow us to test them on the loaded points through the `Step` button. Once validated, we will save this macro and apply it on the the project points through the project window.

* Step one : all points to class 1
It is often a good solution to clean our classification after the matching, as we will reclassify them from scratch. To do this we use the classify points action, putting all the points to default class (1).

![classifyDefaultMacro1](img/screenshot86.png)

![classifyDefaultMacro2](img/screenshot87.png)

* Step two : cut by quality
We cut the ovelap by quality to get rid of most of our cross line points. The _hole_ parameter allows us to keep the points from this line if they help to fill a hole with a diameter bigger than ´0.5m´. 

![cutQualityMacro](img/screenshot88.png)

* Step three : cut by offset
We cut the overlap using a 10 degrees corridor. It means that the points from a trajectory with a scan angle up to 10 degrees will be kept. If their scan angle is more than 10 degrees, they will be kept only if there is no better point (lower scan angle) from a different trajectory in their area. 

 ---
 _Warning_ : 
Beware of the `Coverage` parameter set to 1. It means that only the points in the class 1 will be used to decide if they are to be kept. It is important because we already put a lot of points in the overlap class in the step 2. 
 ---

![cutOffsetMacro](img/screenshot89.png)

* Running the macro
After testing, we launch the macro on the project with `1m`  from neighbour blocks points. The limit the edge effect.

### Ground classification


