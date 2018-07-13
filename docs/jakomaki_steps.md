#### 1. Open point classes \mission\jakomaki.ptc.
#### 2. Read points \laser06\jakomaki000002.fbi.
#### 3. View the data set.
#### 4. Run macro \macro\groups.mac on the data.
#### 5. Fix grouping so that each pole is its own group.
#### 6. Save points as \laser07\jakomaki000002.fbi.
#### 7. Select two yellow trajectory vectors and run 'Group / Classify / By centerline':
* Groups with: `All points`
* From class: `Classes 4-5`
* To class: `15 - Temp`
* Use: `Selected linear elements`
*  Centerline rule: `Majority of points`
* Compare with: `Any line`
* Side: `On either side`
* Offset: `0.00 - 10.00 m`
#### 8. Check classification result.
#### 9. Check 'Settings' tool and 'Object library' category. You should have three
* pole types enabled: `Jakomaki A, Jakomaki B and Jakomaki C.`
#### 10. Check that poles.cel cell library is active.
#### 11. Select two yellow trajectory vectors and run 'Find Poles':
* Groups with: `All points`
* From class: `15 - Temp`
* Ground class: `2 - Ground`
* Inside fence: `Not used`
* Tolerance: `0.150 m`
* Rotation: `From selected vectors`
*  Angle tolerance: `10.0 deg`
* Clip view: `View 3`
