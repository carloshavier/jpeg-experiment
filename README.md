# jpeg-experiment
Experiment on JPEG results picking up the correct puzzle position: Tests the JPEG-size attack on raw TIFF images, resized to 405 x 270 (a size similar to the one of the Capy challenges)

This experiment is to check a very interesting question from Prof. Kuhn during my presentation mentioning the attack published to Capy, KeyCAPTCHA, Garb and any other puzzle (image recomposition) CAPTCHAs. He commented that maybe the good results were related to the images having being pre-compressed using JPEG - interesting idea!. That is why I run this experiment using RAW images.

Instructions to repeat the experiment:

 1 - Download RAISE dataset of RAW images from http://mmlab.science.unitn.it/RAISE/

 2 - Convert them to .PNG (lossless compression) from RAW TIFF, as RAW TIFF is poorly supported by Python PIL library
     we use the following command line (installing first imagemagick)
        $mogrify -format png *.TIF
     and then delete the thumbnails produced
        $rm *-1.png

 3 - Run the experiment (function "main"). There is an option that affects the result: 
     if the images are resized & cropped or just cropped to a size similar to Capy

     The results I got are:
     - if they are resized & cropped, we get aprox. a 30% success ratio
     - if they are only cropped, we get aprox. a 25.7% success ratio
     Note this experiment is not directly comparable to Capy or the other puzzle CAPTCHAs, as it does not use
     a "puzzle shape" in the puzzle piece (just a box).
     Yet it is useful to check that the attack does work even if the images have never been JPEG-compressed before.

 The experiment - What this program does:
 
 1 - Pick each image in the indicated directory (RAW PNG images)
 
     Optionally : crop or crop/resize, maintaining aspect ratio.
 
 2 - Substitute a 80 x 90 pixel square with a subimage from another random image in the directory
     This square can be located anywhere in a 10 x 10 pixel grid (as does Capy)
 
 3 - Perform the JPEG-size attack (described better in the 
     paper "[Using JPEG to Measure Image Continuity and Break Capy and Other Puzzle CAPTCHAs](https://ieeexplore.ieee.org/abstract/document/7307898/)", 
     Internet Computing Magazine, Nov/Dec 2015), 
     with quality = 100, and check whether it is successfull
     
 4 - Save & show statistics (and optionally the images from the challenges and their computed solutions)

