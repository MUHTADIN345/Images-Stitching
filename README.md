# Images-Stitching

## Table Of Content
- [Install Packages](#Install-Packages)
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

![WhatsApp Image 2023-11-16 at 14 47 04_68fca445](https://github.com/tasyabarus20/Image-Stitching/assets/150136650/324e23a0-0d3b-425d-8cb2-f63ff2ca46f2)

image_stitching_simple.py is the program that will be used to execute image stitching. 

2. The directory of images to be stitched:

   ![image](https://github.com/tasyabarus20/Image-Stitching/assets/150136650/cfe66552-476e-4a64-9369-3500dc10c198)

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

   ![WhatsApp Image 2023-11-16 at 14 54 43_218ad8d7](https://github.com/tasyabarus20/Image-Stitching/assets/150136650/ae9ca6a7-953d-4b22-9a5d-d964a612a50f)

   

   
   
