# Building Vectorization, Tree Mapping, and 3D City Model Visualization 

 

## Data set: 

part of Jyväskylä city, laser data prepared (ground, building roofs classified), class file, images from 5 cameras (vertical, oblique), mission, adjusted image list , (true-)orthophotos 

laser data from 2011, images from 2012 


## Building vectorization (automatically/manual improvements) 


load project into TScan 

check laser data: classification, line matching, density, noise level on roofs 

cut overlap not done → would be better to do to reduce noise level and to avoid issues due to mismatch in data 

issue in this data set: no points on many dark roofs → vectorization from laser data not possible 

density with overlap ~23pts/m2, without overlap ~10pts/m2 

10 pts/m2 are good for vectorizing buildings with major details on roofs, less density allows only vectorization of large buildings, more density improves result only marginally 

classification based on grouping done 

points on roofs, roof details in separate class 

 

load model keypoints into TScan 

 

check TPhoto Settings > Memory usage > Image cache = 4000 MB (64-bit version) 

check Builtin projection systems > Finnish ETRS GK26 

 

open mission, load model keypoints from TScan, open image list (hrp-adjusted image list) 

 

look at images with Define color corrections dialog, check images from different cameras 

Images > Define color corrections 

last number in image number indicates camera, e.g. 1=vertical cam, 2=backward-looking oblique cam, etc. 

 

delete images from oblique cameras 

Images > Delete > By camera 

save image list as images_hrp_adjusted_vertical.iml 

 

check macro for building vectorization, check settings for the vectorization step 

user roof class: forces the vectorization of smaller details on roof represented by points in this class, ignores minimum detail setting 

low classes: help to place edges, use ground only if images are available, use ground and low vegetation if no images are available 

footprints can be used, only buildings with footprints are vectorized 

planarity: how well points must fit to the plane equation describing a roof plane, ~15 cm for “normal” ALS data, normally not smaller than 10 cm 

increase tolerance: close-to-horizontal planes should be modeled as one roof plane, requires increase in planarity tolerance 

use images if available,  ~ 90% vectorization done from laser points, 10% from images 

 

select block 33 in TScan Project window 

run macro on project, selected blocks only, 200m of neighbours, Do not save points 

can not run in TSlave if images are used 

 

check level usage in TScan Settings > Building vectorization > Levels 

roof, wall, base polygons are drawn on separate levels 

read text file(s) with building models 

random wall color 

look at models in design file with smooth rendering, a bit of lightning 

 

start Check building models tool 

unchecked buildings 

arrange views on 

check different views for building modification 

Check building models dialog → list of all (unchecked) models in dgn, largest buildings first in list 

View 1 → display of active (selected) model, wireframe rendering, rotated top view, good for understanding xy relationship of model, level with colored edges visible 

View 5 → rotated view, smooth rendering, good for 3D understanding of model, only level with active model should be visible 

View 7 → perspective/camera view, raw image displayed with lens distortion applied, viewer = camera position, displays best image for showing whole building (“overview”) 

View 8 → another camera view, displays image that is best for placing an edge or corner of the model (“detail view”), updated when a building modification tool is used to select an edge or corner 

start modification with easier buildings → scroll a bit down in list and select a simple building model 

check different modification tools from Building patches and Building edges tool sets 

see more info and example usage in the User Guide and the training animation 

Colored point cloud and textured vector models 

attach orthophotos as references in TPhoto 

Manage raster references, File > Attach directory, select ortho folder 

display in view 1 and Render view 

 

extract color for points from orthophotos 

activate color attribute for project 

TScan Project window Tools > Extract color from images 

all classes, extract from ortho images, footprint 1 pixel 

 

switch off display of orthos view 1 (keep R on for rendering), load laser points from all files of the project and display points by color to check result 

 

check TScan Settings > Point display > Depth separation, maybe change value to something big like 4.0 m, point cloud visualization gets less noisy 

 

close image list in TPhoto 

load list with all images (hrp_adjusted) 

delete images from vertical camera 

Images > Delete > By camera 

save list as images_hrp_adjusted_oblique.iml 

make all levels with vector models visible in dgn, all other levels invisible 

 

select vector models 

create wall textures 

Rectify > Rectify wall rasters 

minimum area 5 m210% coverage0.10 m pixel size 

format tiffdo not use depth maps 

output folder same as design file folder (dgn) 

prefix wall_modify element color on 

 

rotate view 1 

use TPhoto Render view tool, display rendered view with wall textures 

 

Display Rendering Settings tool 

Drape rasters on levels that contain roof polygons (e.g. 1,5) 

open Manage raster references tool, attach directory, folder with orthophotos, switch only R (render) on 

step was done before but wall texture creation seems to detach references 

use TPhoto Render view tool, display rendered view with orthos draped on roofs 

 

TerraModeler Surfaces tool, File > Import xyz binary file, select key15.fbi file from laser folder 

Default exclusion, Exclude outer triangles off 

name for surface model = key15, ok 

use Display raster triangles tool of TModeler to display surface model key15 on level 55 

display level 55 in view 1 

use TPhoto Render view tool, display rendered view with orthos draped on surface model 

 

open block 33 

display medium, high vegetation and pole classes, all other classes off 

trees best represented in point cloud, display true dimensions and shape for tree crowns 

use TPhoto Render view tool, display rendered view with points on trees and poles 

 

color from images not so good for smaller, espec. linear objects, constant or intensity colors better for visualization, constant color can highlight certain objects in point cloud 

open Display mode dialog, Color by intensity custom, Colors button 

save the intensity coloring scheme into a file 

cancel, close Display mode dialog 

 

 

assign intensity coloring to points in poles class 

Tools > Assign color, class poles, intensity coloring, select intensity color file 

use TPhoto Render view tool, display rendered view with points on trees and poles, check pole visualization 

 

save points 

Tree mapping for cities 

check cell library, attach ″karttali″ from terra installation folder 

check settings for tree species in TScan 

sample species birch and spruce 

use cells from the sample library 

draw fence around trees along a road 

Create tree cells 

one example species 

all points of a group inside fence 

select tree cells, Modify tree cells 

top, section, camera view 

use oblique images in camera view for detecting tree crown dimensions and trunk width 

select tree cells, Output tree cells 

write tree information into text file 

import for DB application 

Creation of a fly-through animation 

read all FBI files of the project, switch off time, line,... attributes, just keep attributes that are good for visualization (color, intensity) 

 

change active level to an empty level (e.g. 20) 

 

digitize a line string element that can serve as camera path for fly-over animation 

MS Place smart line tool, rounded corners 

use TModeler Set linear elevation tool and move line string to 300 m 

select element 

 

start Create fly-through movie tool in TPhoto 

back clipping 2500 m, front clipping 1 m 

render quality = High quality (for vector models and images draped on ground/roofs, lower quality for rendering only laser data, Capture if text needs to be included) 

video speed 25 frames/second, default speed = camera speed = 30-40 m/seconds for fly-overs 

change active level to empty level and color to other color 

Target > Create vectors 

to define the viewing direction of camera 

direction forward onto surface, step 50 m, distance 250 m, surface = key15, dz = 0 

open view 7, setup the view for recording frames of fly-over animation: 

view size (=frame size) 

view content (= frame content), e.g. level visibility (vector models, surface model triangles), point cloud display 

open TPhoto Define rendering settings > Enhance depth perception on, maybe sky background on 

check a few views with the preview option of the Create fly-through dialog, type frame number, click Preview, fix display if necessary 

create a few frames 

use e.g. Windows Movie Maker software to combine frames into a movie 
 
More information about this topic 

TScan Users Guide, Chapter 9: 3D Building Models http://www.terrasolid.com/download/user_guides.php) 

Training animations: http://www.terrasolid.com/download/animations/deliverybpt.php 
