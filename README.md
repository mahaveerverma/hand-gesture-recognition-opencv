# HAND GESTURE RECOGNITION

### INTRODUCTION
This project implements a hand recognition and hand gesture recognition system using OpenCV on Python 2.7. A histogram based approach is used to separate out a hand from the background image. Background cancellation techniques are used to obtain optimum results. The detected hand is then processed and modelled by finding contours and convex hull to recognize finger and palm positions and dimensions. Finally, a gesture object is created from the recognized pattern which is compared to a defined gesture dictionary.

**Platform:** Python 2.7

**Libraries:** OpenCV 2.4.8, Numpy

**Hardware Requirements:** Camera/Webcam

### USAGE

Run HandRecognition.py to begin the program.

**Note for Windows users:**
Remove this line from all .py files: '#!/usr/bin/python' or else you might get some error.

You will find a window that shows your camera feed. Notice a rectangular frame on the right side of the window. That's the frame where all the detection and recognition works.

To begin, keep your hand and body outside the frame, so as to capture just the background environment, and press 'b'. This will capture the background and create a model of it. This model will be used to remove background from every frame captured once the program setup is complete. 

Now, you have to capture your hand histogram. Place your hand over the 9 small boxes in the frame so as to capture the maximum range of shades of your hand. Don't let any shadow or air gap show on the boxed areas for best results. Press 'c' to capture the hand and generate a histogram. 

The setup is now complete. Now you will see, by keeping your hand inside the rectangular frame, it gets detected and you will notice a circle inside your palm area, with lines projecting out from it towards your fingers. Try moving your hands, hiding a few fingers or giving it one of the sample gestures implemented in the program.

The sample gestures implemented are described with screenshots in the documentation. 

They are:

1. "V" with your index and middle finger

2. A flipped "L" with thumb and index finger

3. Pointing with your index finger in vertical position

**Note:** Press 'q' at any time to stop the program or 'r' to restart the program.

### HOW DOES IT WORK?

Read full documentation for detailed explanation about implementation in "docs" folder.

During setup, first a background model is generated when the user presses 'b'. Then, a histogram is generated when the user provides his hand as a sample by pressing 'c'. When the setup is completed, the program goes into an infinite while loop which does as follows.

Camera input frame is saved to a numpy array. A mask is generated based on background model and applied on the frame. This removes background from the captured frame. Now the frame containing only the foreground is converted to HSV color space, followed by histogram comparison (generating back projection). This leaves us with the detected hand. Morphology and smoothening is applied to get a proper hand shape out of the frame. A threshold converts this into a binary image.

Next, we find contours of the binary image obtained, look for the largest contour and find its convex hull.

Using points from the largest contour we determine center of the palm by finding the largest circle inscribed inside the contour and then the dimension of palm. Using the center of palm as reference, we eliminate all points from the convex hull which do not seem to be part of hand. Also, nearby convex hull points are eliminated so that we are left with exactly only those many points as the number of fingers stretched out.

Using the positions of fingers and palm dimensions, we model our hand.

Then we compare the model with a dictionary of Gestures defined in GestureAPI.py to determine presence of gestures.

**Full explanation with screenshots is provided in /docs/Documentation.pdf**

For any queries, contact: mahaveer.verma1@gmail.com