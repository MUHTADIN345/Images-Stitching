# Images-Stitching

## Table Of Content
- [Install Packages](Install-Packages)
- [Execution of Stitching Images](Execution-Of-Stitching-Images)

## Install Packages

1. Install Imutils
   
   To install the packages use the command
   ```bash
   pip3 install imutils
   ```
3. Install opencv
   
   To install it use the command
   ```bash
   Pip3 install opencv-python
   ```
5. Install matplotlib
   ```bash
   Pip3 install matplotlib
   ```

## Execution of Stitching Images
1. Enter the directory that contains the image stitching code and the directory of images to be stitched

<img width="1000" alt="file" src="https://github.com/MUHTADIN345/Images-Stitching/assets/126330305/3811e97f-245c-45d7-87da-e4b93f555715">


image_stitching_simple.py is the program that will be used to execute image stitching. 

2. The directory of images to be stitched:

   <img width="800" alt="Screenshot 2023-11-18 193326" src="https://github.com/MUHTADIN345/Images-Stitching/assets/126330305/43c096fa-0e59-4074-bed9-e69d87e41fb7">


3. image_stitching_simple.py contains the following code.
    ```bash
   # USAGE
   # python image_stitching_simple.py --images images/scottsdale --output output.png

   # import the necessary packages
   from imutils import paths
   import numpy as np
   import argparse
   import imutils
   import cv2

   # construct the argument parser and parse the arguments
   ap = argparse.ArgumentParser()
   ap.add_argument("-i", "--images", type=str, required=True,
   	help="path to input directory of images to stitch")
   ap.add_argument("-o", "--output", type=str, required=True,
   	help="path to the output image")
   args = vars(ap.parse_args())
   
   # grab the paths to the input images and initialize our images list
   print("[INFO] loading images...")
   imagePaths = sorted(list(paths.list_images(args["images"])))
   images = []
   
   # loop over the image paths, load each one, and add them to our
   # images to stich list
   for imagePath in imagePaths:
   	image = cv2.imread(imagePath)
   	images.append(image)
   
   # initialize OpenCV's image sticher object and then perform the image
   # stitching
   print("[INFO] stitching images...")
   stitcher = cv2.createStitcher() if imutils.is_cv3() else cv2.Stitcher_create()
   (status, stitched) = stitcher.stitch(images)
   
   # if the status is '0', then OpenCV successfully performed image
   # stitching
   if status == 0:
   	# write the output stitched image to disk
   	cv2.imwrite(args["output"], stitched)
   
   	# display the output stitched image to our screen
   	cv2.imshow("Stitched", stitched)
   	cv2.waitKey(0)
   
   # otherwise the stitching failed, likely due to not enough keypoints)
   # being detected
   else:
   	print("[INFO] image stitching failed ({})".format(status))
   ```
4. Then enter the command below to execute it
   ```bash
   python3 image_stitching_simple.py --images images/scottsdale --output coba.png
   ```
5. Then the output will appear in the form of images that have been stitched

   ![output](https://github.com/MUHTADIN345/Images-Stitching/assets/126330305/15f688b6-e235-464c-b2b2-eb8faad94d72)


   

   
   
