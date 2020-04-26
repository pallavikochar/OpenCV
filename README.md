# Virtual-Keyboard-Documentation-Week2
# OpenCV [open source computer vision library]:
Computer Vision is the way of teaching intelligence to machines and making them see thing just like humans. 
OpenCV is image processwing library. Available on windows, linux, mac. Works in C, C++, Python.
Digital images are typically stored in a matrix. PPI - pixel per inch. Computer sees an image in the form of pixel matrix. Grey scaled images[each pixel represents the intensity of nly one shade][it has only 1 channel] and coloured images[has 3 channels- R[red] G[green] B[blue]]. Standard digital camera has 3 channels.
### Numpy: 
NumPy is the fundamental package for scientific computing with Python. It contains among other things: a powerful N-dimensional array object, sophisticated (broadcasting) functions, tools for integrating C/C++ and Fortran code, useful linear algebra, Fourier transform, and random number capabilities.

## How to read display and save videos using cameras:
```python
import cv2

cap = cv2.VideoCapture(0);                       

while(True):                                     
    ret, frame = cap.read()                          

    cv2.imshow('frame', frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):            
        break   #Come out of the loop                                          

cap.release()   #release the resources                                    
cv2.destroyAllWindows() #it destroys all the windows                        

```
#### EXPLANATION:
cap = cv2.VideoCapture(0);                       #to capture live stream from the default camera, VideoCapture is a class and we create an object of it. As argument we can either provide input file name. If we just want to read a video from a particular file we will give the file name like myfile.avi maybe OR we can provide the device index of the camera. By deafult it is either 0 or -1. If we have multiple cameras and if we want to use the other camera then we can also try one for the second camera or two for the third camera and so on. 



while(True):                                     #while loop is created to capture the frame continuously and we will run this loop indefinitely. while this loop is true, we want to capture the frames. 



ret, frame = cap.read()                          #So we will just define these variable ret and frame and then using this cap instance we will call a method read. Now this read method is going to return true if the frame is available and this frame will be saved into this frame variable. If the frame is available ret will be true otherwise it will be false and this frame variable will actually capture or save the frame.  



if cv2.waitKey(1) & 0xFF == ord('q'):            #We use waitKey to wait for user input. If input is q key quit and destroy all windows
                                                              

## To convert video input from coloured to gray
```python
import cv2

cap = cv2.VideoCapture(0);                       

while(True):                                     
    ret, frame = cap.read()                          
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY) 
    cv2.imshow('frame', gray)

    if cv2.waitKey(1) & 0xFF == ord('q'):            
        break                                          

cap.release()                                    
cv2.destroyAllWindows()                        

```
#### EXPLANATION:
gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)   #To convert our video input from colured to the gray scale image. First argument is source and second argument is conversion which want to do. By default coloured image is captured as BGR channel images.  

cv2.imshow('frame', gray)   #gray imput becomes second argument to get a gray scaled image

When q is pressed all the captured resources get released and all the windows get destroid


### Using cap instance we can read few properties about the video captured
1] whether the video is opened  or not. Whenever we provide the file name and the file path is wrong, it will give us false
```python
import cv2

cap = cv2.VideoCapture(0); 

while(cap.isOpened()):                           #If the file name of the video we want to provide is correct then we get true otherwise isOpened will give us false if path is wrong or index in VideoCapure is wrong.            

ret, frame = cap.read()   

gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)  

cv2.imshow('frame', gray)

if cv2.waitKey(1) & 0xFF == ord('q'):

break                                            

cap.release()                                   

cv2.destroyAllWindows()                          
```
 
#### NOTE:
use print(cap.isOpened()) to see whether isOpened() prints true or false i.e., check whether video is getting captured at that index or at that file name. If cap.isOpened gives us false, we can try using cap.Open.

2]
```python
import cv2

cap = cv2.VideoCapture(0); 

while(cap.isOpened()):   #If the file name of the video we want to provide is correct then we get true otherwise isOpened will give us false if path is wrong or index in VideoCapure is wrong.            

ret, frame = cap.read() 

print(cap.get(cv2.CAP_PROP_FRAME_WIDTH))   #different values of propId. It gives width of the frame
print(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))   #It gives height of the frame

gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)  

cv2.imshow('frame', gray)

if cv2.waitKey(1) & 0xFF == ord('q'):

break                                            

cap.release()                                   
cv2.destroyAllWindows()                          
```

## To save the video
```python
import cv2

cap = cv2.VideoCapture(0); 
fourcc = cv2.VideoWriter_fourcc(*'XVID');   #or fourcc = cv2.VideoWriter_fourcc('X','V','I','D');
out = cv2.VideoWriter('output.avi',fourcc,20.0,(640,480));   

while(cap.isOpened()):             

    ret, frame = cap.read() 
    if ret == True
        print(cap.get(cv2.CAP_PROP_FRAME_WIDTH))   #different values of propId. It gives width of the frame
        print(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))   #It gives height of the frame
        
        out.write(frame)    #out is the instance of video writer and we pass frame which we captured 
        
        gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)  

        cv2.imshow('frame', gray)

        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
        else
            break

cap.release()
out.release()   #release all the resources
cv2.destroyAllWindows()                          
```
### EXPLANATION
out = cv2.VideoWriter('output.avi',fourcc,20.0,(640,480));   #to save the video we create this class. first argument is the name of the output file, second argument is FOURCC code, third is number of frames per second, fourth is size- we provide this in the form of tuple

while(cap.isOpened()):   #If the file name of the video we want to provide is correct then we get true otherwise isOpened will give us false if path is wrong or index in VideoCapure is wrong.   

##### NOTE
Here video will be saved in BGR mode because argument of out.write is frame which is coloured but appearing video will be in a gray mode 

# How to draw geometric shapes on images using Python OpenCV

```python
import numpy as np
import cv

img = cv2.imread('lena.jpg',0)  #reads an image in gray scale

img = cv2.line(img, (0,0), (255,255), (0,0,255), 5)
img = cv2.arrowedLineine(img, (0,0), (255,255), (0,0,255), 5) 

img = cv2.rectangle(img, (384,0), (510,128), (0,0,255), 5)
img = cv2.circle(img, (447, 63), 63, (0,255,0), -1)
font = cv2.FONT_HERSHEY_SIMPLEX
img = cv2.putText(img, 'OpenCV' , (10,500) , font, 4, (255,255,255), 10, cv2.LINE_AA) 

cv2.imshow('image',img) #shows an image into a window

cv2.waitKey(0) #wait for closing event
cv2.destroyAllWindows() #destorys all the windows
``` 

#### EXPLANATION:
##### 1] To draw a line 
img = cv2.line(img, (0,0), (255,255), (255,0,0), 5) #first argument is image, second is starting coordinates of point 1, third is the ending coordinates of point 2, fourth is the colour and fifth is the thickness. Here we will get a blue coloured line with thickness 5. Coordinates are to be given in the form of tuple. Colour is given in the BGR format. (255,0,0) gives blue channel, (0,255,0) gives green channel, (0,0,255) gives red channel. Thickness is provided in numbers. Here we see a black line because the image is loaded in gray scale. To load this image in colored format we will have to change img = cv2.imread('lena.jpg',0) t img = cv2.imread('lena.jpg',1). We can choose colour from google rgb color picker but note that it'll be in reverse order i.e., bgr and rgb.

##### 2] To draw a ray 
img = cv2.arrowedLineine(img, (0,0), (255,255), (0,0,255), 5) #all the arguments are same as that of line class. Here we will get a red coloured line.

##### 3] To draw a rectangle
img = cv2.rectangle(img, (384,0), (510,128), (0,0,255), 5) #first argument is image, second is point 1-top left vertex coordinate, third is point 2- bottom right vertex coordinate, fourth is the colour and fifth is the thickness. Here we will get a red unfilled coloured rectangle. By putting thickness argument as -1, we get a filled rectangle with the colour we specified.

##### 4] To draw a circle
img = cv2.circle(img, (447, 63), 63, (0,255,0), -1) #first argument is image, second is the center of the circle, third is the radius of the circle, fourth is the colour and fifth is the thickness. It gives a green coloured filled circle.

##### 5] To put a text
img = cv2.putText(img, 'OpenCV' , (10,500) , font, 4, (255,255,255), 10, cv2.LINE_AA)  #first argument is image, second is the text we want to put, third is the starting point of the text, fourth is the fontFace, fifth is the fontSize, sixth is the colour, seventh is the thickness and the eight can be lineType. Argument fontFace is given by creating a variable, here it is font. We will get the text OpenCV in white colour.

### To create an image using numpy zeros:
To create an image using numpy zeros method  we can use img = np.zeros(). To create a black image, first argument will be a list with first argument being height, second width and third will be 3 and second argument is datatype- np.uint8.

```python
import numpy as np
import cv

img = np.zeros([512,512,3], np.unit8)
cv2.imshow('image',img) #shows an image into a window

cv2.waitKey(0) #wait for closing event
cv2.destroyAllWindows() #destorys all the windows
``` 
6.
```
import cv2
cap = cv2.VideoCapture(0)
print(cap.get(cv2.CAP_PROP_FRAME_WIDTH))                  # cap.get() :  Used to access some features of the video.
print(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

cap.set(3, 3000)                                       
cap.set(4, 3000)                                          # •	Every property(feature) has a number associated with it.
                                                                   Eg : 3 ; width , 4 ; height


print(cap.get(3))
print(cap.get(4))                                         # •	Properties such as height and width are automatically 
                                                              adjusted to only the available resolution.
while(cap.isOpened()):
    ret, frame = cap.read()
    if ret == True:
a
       gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
       cv2.imshow('frame', gray)

       if cv2.waitKey(1) & 0xFF == ord('q'):
         break
    else:
        break

cap.release()
cv2.destroyAllWindows()
```
7.
# Datetime Module
 Datetime module supplies classes to work with date and time. These classes provide a number of functions to deal with dates, times and time intervals. Date and datetime are an object in Python, so when you manipulate them, you are actually manipulating objects and not string or timestamps.

The datetime classes are categorize into 6 main classes –



- date :
An idealized naive date, assuming the current Gregorian calendar always was, and always will be, in effect. Its attributes are year, month and day.
- time :
An idealized time, independent of any particular day, assuming that every day has exactly 24*60*60 seconds. Its attributes are hour, minute, second, microsecond, and tzinfo.
- datetime :
Its a combination of date and time along with the attributes year, month, day, hour, minute, second, microsecond, and tzinfo.
- timedelta :
A duration expressing the difference between two date, time, or datetime instances to microsecond resolution.
- tzinfo :
It provides time zone information objects.
- timezone :
A class that implements the tzinfo abstract base class as a fixed offset from the UTC (New in version 3.2).


[Datetime module examples](https://www.geeksforgeeks.org/python-datetime-module-with-examples/)



```
import cv2
import datetime                                                                # datetime package is imported 
cap = cv2.VideoCapture(0)
print(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
print(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
#cap.set(3, 3000)
#cap.set(4, 3000)
#print(cap.get(3))
#print(cap.get(4))
while(cap.isOpened()):
    ret, frame = cap.read()
    if ret == True:

       font = cv2.FONT_HERSHEY_SIMPLEX
       text = 'Width: '+ str(cap.get(3)) + ' Height:' + str(cap.get(4))         # str() : converts the passed data into a string data
                                                                                # str() is used since cap.get() returns an integer value
       datet = str(datetime.datetime.now())                                     # current date & time is stored in this variable
       frame = cv2.putText(frame, text, (10, 50), font, 1,
                           (0, 255, 255), 2, cv2.LINE_AA)
       frame = cv2.putText(frame, datet, (10, 100), font, 1,
                           (0, 255, 255), 2, cv2.LINE_AA)
       cv2.imshow('frame', frame)

       if cv2.waitKey(1) & 0xFF == ord('q'):
         break
    else:
        break

cap.release()
cv2.destroyAllWindows()
```
8.
```python
import numpy as np                                                        #importing numpy package as np
import cv2                                                                #importing OpenCv package as cv2

#events = [i for i in dir(cv2) if 'EVENT' in  i]                          #Getting the list of all the fucntions/Classes whoose name have the word "EVENT"
#print(events)                                                            #Printing the list

def click_event(event, x, y, flags, param):                               #Creating the function click_event
    if event == cv2.EVENT_LBUTTONDOWN:                                    #if we click Left Button then it will enter this block
        print(x,', ' ,y)
        font = cv2.FONT_HERSHEY_SIMPLEX
        strXY = str(x) + ', '+ str(y)                                     #strXY will contain the x,y coordinates of where we had clicked the left Button
        cv2.putText(img, strXY, (x, y), font, .5, (255, 255, 0), 2)       #Put the text-"strXY" into the image-"img" at the location-(x,y)having font size-0.5 with the colour having BGR colour-(255,255,0) having line thickness 2
        cv2.imshow('image', img)                                          #Showing the image after putting the text
    if event == cv2.EVENT_RBUTTONDOWN:                                    #If we click the right button then we will enter this block
        blue = img[y, x, 0]                                               #We will get the Blue value at the point where we had clicked
        green = img[y, x, 1]                                              #We will get the Green value at the point where we had clicked
        red = img[y, x, 2]                                                #We will get the Red value at the point where we had clicked
        font = cv2.FONT_HERSHEY_SIMPLEX
        strBGR = str(blue) + ', '+ str(green)+ ', '+ str(red)             #Storing BGR value at the point where we have right clicked in strBGR
        cv2.putText(img, strBGR, (x, y), font, .5, (0, 255, 255), 2)      #Put the text-"strBGR" into the image-"img" at the location-(x,y)having font size-0.5 with the colour having BGR colour-(255,255,0) having line thickness 2  
        cv2.imshow('image', img)                                          #Showing the image

#img = np.zeros((512, 512, 3), np.uint8)                                  #Creating image-"img" of size 512 by 512 having data type uint8 in which the values of all the pixels is 0 i.e creating a full black image
img = cv2.imread('lena.jpg')                                              #Storing image-"lena.jpg" in img
cv2.imshow('image', img)                                                  #Showing the image-"img"

cv2.setMouseCallback('image', click_event)                                #If we press any Mouse key then this function will be called and the event,(x,y) coordinates of the mouse clicked will be passed to the function click_event

cv2.waitKey(0)                                                            #To show the image for an infinte time
cv2.destroyAllWindows()                                                   #Destroying all the windows


```
9.

```python
import cv2
import numpy as np

#run one function at a time or change names and call seperately

def click_event(event, x, y, flags, param):                 #fuction to make a small circle on every left click and join the two points
    if event== cv2.EVENT_LBUTTONDOWN:                       #check if left click
        cv2.circle(img, (x, y), 5, (0, 0, 255), -1)         #draw a circle on the point of click
        points.append((x, y))                               #add the point to an array 
        if len(points) >=2:                                 #just to make sure atleast two points are there to draw a line
            cv2.line(img, points[-1], points[-2], (255, 0, 0), 5)   #draw line joining the last two clicks
        cv2.imshow('image', img)                            #showing image in a window named image

def click_event(event, x, y, flags, param):                 #function to open a new window with the same color as of the point clicked
    if event== cv2.EVENT_LBUTTONDOWN:                       #check if left click
        blue = img[x, y, 0]                                 #
        green = img[x, y, 1]                                #
        red = img[x, y, 2]                                  #
        mycolorImage = np.zeros((512,512,3), np.uint8)      #creating a new window

        mycolorImage[:] = [blue, green, red]                #assigning color to the new window
        cv2.imshow('color', mycolorImage)                   #showing the new window

#img = np.zeros((512,512,3), np.uint8)                      #to open a black window
img = cv2.imread('lena.jpg',-1)                             #to open the image lena
cv2.imshow('image', img)                                    #showing the image 
points = []                                                 #the empty array points, points will be append to it on each click

cv2.setMouseCallback('image', click_event)                  #        
cv2.waitKey(0) & 0xFF                                       #
cv2.destroyAllWindows()                                     #
```
10.
```python
import numpy as np
import cv2

img = cv2.imread('messi5.jpg')

print(img.shape) # returns a tuple of number of rows, columns and channels in this order
print(img.size) # returns total number of pixels inside the image which is accessed
print(img.dtype) # returns image datatype
b,g,r = cv2.split(img) # (returns three values) splits image (taken as argument) in 3 channels blue, green and red in order
img = cv2.merge((b,g,r)) # takes the channels in the form of tuples; merges the blue, green and red channels into an image

ball = img[280:340, 330:390] # y coordinate min to max, x coordinate min to max (values in the bracket)
# this assigns the desired matrix (which contains information about our roi) from the main image to a new variable ball
img[273:333, 100:160] = ball
# this changes the pixels (of desired location of indexing) in main image to that of ball

img2 = cv2.imread('opencv-logo.png')
#dst = cv2.add(img, img2)
# the above commented line will lead to an error as images with different size cannot be added
img = cv2.resize(img, (512,512))
# first argument in this method is the source and second is the required size(no of rows, no of columns)
img2 = cv2.resize(img2, (512,512)) # now these two can be added
dst = cv2.add(img, img2)

dst2 = cv2.addWeighted(img, 0.9, img2, 0.1, 0)
# this method adds two images with a specified weight, first argument will be the first source (image), second will be the required weight of first source (alpha), third is the source two, fourth is the weight of second image (beta), fifth argument is the gama value which is a scalar value to be added

cv2.imshow('image',img)
cv2.imshow('added',dst)
cv2.imshow('weighted addition',dst2)

cv2.waitKey(0)
cv2.destroyAllWindows()
```
11.

# Bitwise operations

Bitwise operations can be useful when working with masks. Masks are binary images that indicates pixel in which an operation is to be performed.

   ```python
 
import cv2
import numpy as np
img1 = np.zeros((250, 500, 3), np.uint8)  # to create a black image(by this black pixels have zero value and white pixels have value =1)
img1 = cv2.rectangle(img1,(200, 0), (300, 100), (255, 255, 255), -1)
img2 = cv2.imread("image_1.png")

bitAnd = cv2.bitwise_and(img2, img1)     # returns 1 if and only if both pixel values are 1(white pixel) , otherwise returns 0 
bitOr = cv2.bitwise_or(img2, img1)       # returns 0 if and only if both pixel values are 0(black pixel) , otherwise returns 1 
bitXor = cv2.bitwise_xor(img1, img2)     # returns 1 if and only if exactly one pixel value is 1(white pixel) , otherwise returns 0
bitNot1 = cv2.bitwise_not(img1)          # Same as negation, if pixel value= 1 returns 0 and if pixel value= 0 returns 1
bitNot2 = cv2.bitwise_not(img2)

cv2.imshow("img1", img1)
cv2.imshow("img2", img2)
cv2.imshow('bitAnd', bitAnd)
cv2.imshow('bitOr', bitOr)
cv2.imshow('bitXor', bitXor)
cv2.imshow('bitNot1', bitNot1)
cv2.imshow('bitNot2', bitNot2)

cv2.waitKey(0)
cv2.destroyAllWindows()

```
12.
```python
import numpy as np                                          #importing numpy package as np
import cv2 as cv                                            #importing OpenCv package cv2 as cv

def nothing(x):                                             #Defining a function "nothing" which takes one argument and prints that argument
    print(x)

# Create a black image, a window                            #Creating a black image whoose size is 300 by 512.Has all the pixel values 0 and the data type of image is uint8
img = np.zeros((300,512,3), np.uint8)
cv.namedWindow('image')                                     #Creating a window having name-"image"
                                
cv.createTrackbar('B', 'image', 0, 255, nothing)            #Creating TrackBar "B" on Window "image" having lower limit 0 and upper limit 255 and passing the value of Thrackbar to the function "nothing"
cv.createTrackbar('G', 'image', 0, 255, nothing)
cv.createTrackbar('R', 'image', 0, 255, nothing)

switch = '0 : OFF\n 1 : ON'                                 #Creating a switch with 0 as OFF and 1 as ON
cv.createTrackbar(switch, 'image', 0, 1, nothing)

while(1):                                                   #infinite loop
    cv.imshow('image',img)                                  #Showing the image-"img" with the name "image"
    k = cv.waitKey(1) & 0xFF                                #The window will waiting on the screen for 1 milliseconds
    if k == 27:                                             #If one presses esc key on keyboard the loop will break.The ASCII value for esc key is 27
        break
                                            
    b = cv.getTrackbarPos('B', 'image')                     #Getting the value of the Trackbar-"B" which is in the window-"image" 
    g = cv.getTrackbarPos('G', 'image')                     #Getting the value of the Trackbar-"G" which is in the window-"image" 
    r = cv.getTrackbarPos('R', 'image')                     #Getting the value of the Trackbar-"R" which is in the window-"image" 
    s = cv.getTrackbarPos(switch, 'image')                  #Getting the value of the Trackbar-"switch" which is in the window-"image" 

    if s == 0:                                              #If the value of the switch is 0 then the image will become entirely black
       img[:] = 0
    else:               
       img[:] = [b, g, r]                                   #If the switch is ON then the image will have the colour whoose BGR values are same to the values of the TrackBar-'B','G','R'


cv.destroyAllWindows()                                      #To destroy all the windows created
```
13.
# Object Detection and Object Tracking Using HSV Color Space

## HSV->

### Hue
Hue corresponds to the colour components(base pigment) hence just by selecting a range of hue u can select any colour(0-360)

### Saturation
Saturation is the amount of colour(depth of pigment)(dominance of hue)(0-100%)

### Value
Value  is the brightness of the colour(0-100%)

![hsv](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/HSV_color_solid_cone.png/800px-HSV_color_solid_cone.png)



## Code
### To detect an object in an image:

```
import cv2
import numpy as np

def nothing(x):                                                 #call back function,dummy function in this case
    pass

cv2.namedWindow("Tracking")                                     #creating window named tracking
cv2.createTrackbar("LH", "Tracking", 0, 255, nothing)           # Creating trackbars for lower and upper hue,saturation and value
cv2.createTrackbar("LS", "Tracking", 0, 255, nothing)           
cv2.createTrackbar("LV", "Tracking", 0, 255, nothing)
cv2.createTrackbar("UH", "Tracking", 255, 255, nothing)
cv2.createTrackbar("US", "Tracking", 255, 255, nothing)
cv2.createTrackbar("UV", "Tracking", 255, 255, nothing)

while True:                                                 #to keep running program to keep getting new trackbar positions until escaped
    frame = cv2.imread('smarties.png')

    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)            #converting defualt BGR format of frame to HSV and storing in hsv variable

    l_h = cv2.getTrackbarPos("LH", "Tracking")              # getting trackbar positions for getting lower and upper bounds of HSV
    l_s = cv2.getTrackbarPos("LS", "Tracking")
    l_v = cv2.getTrackbarPos("LV", "Tracking")

    u_h = cv2.getTrackbarPos("UH", "Tracking")
    u_s = cv2.getTrackbarPos("US", "Tracking")
    u_v = cv2.getTrackbarPos("UV", "Tracking")

    l_b = np.array([l_h, l_s, l_v])                         # creating arrays storing bounds in H,S,V format
    u_b = np.array([u_h, u_s, u_v])

    mask = cv2.inRange(hsv, l_b, u_b)                       #mask for thresholding hsv image to only get regions in the bounds set by trackbar

    res = cv2.bitwise_and(frame, frame, mask=mask)          # applying mask on coloured image using bitwise_and function and storing it as result=res

    cv2.imshow("frame", frame)                              #displaying orignal image,mask and resultant image
    cv2.imshow("mask", mask)
    cv2.imshow("res", res)

    key = cv2.waitKey(1)
    if key == 27:
        break

cv2.destroyAllWindows()
```
---

### To detect an object in a video:

```
import cv2
import numpy as np

def nothing(x):                                                 #dummy function
    pass

cap = cv2.VideoCapture(0);

cv2.namedWindow("Tracking")                                         #creating a window named 'tracking'
cv2.createTrackbar("LH", "Tracking", 0, 255, nothing)               #creating trackbars for lower and upper bounds of hsv
cv2.createTrackbar("LS", "Tracking", 0, 255, nothing)
cv2.createTrackbar("LV", "Tracking", 0, 255, nothing)
cv2.createTrackbar("UH", "Tracking", 255, 255, nothing)
cv2.createTrackbar("US", "Tracking", 255, 255, nothing)
cv2.createTrackbar("UV", "Tracking", 255, 255, nothing)

while True:                                         #to keep running program to keep getting new trackbar positions and frames from video until escaped
    _, frame = cap.read()                           #getting frame from video

    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV).   # coverting BGR to HSV and storing in hsv variable

    l_h = cv2.getTrackbarPos("LH", "Tracking")      #getting trackbar positions for getting lower and upper bounds of HSV
    l_s = cv2.getTrackbarPos("LS", "Tracking")
    l_v = cv2.getTrackbarPos("LV", "Tracking")

    u_h = cv2.getTrackbarPos("UH", "Tracking")
    u_s = cv2.getTrackbarPos("US", "Tracking")
    u_v = cv2.getTrackbarPos("UV", "Tracking")

    l_b = np.array([l_h, l_s, l_v])                 # creating arrays storing bounds in H,S,V format
    u_b = np.array([u_h, u_s, u_v])

    mask = cv2.inRange(hsv, l_b, u_b)               #mask for thresholding hsv image to only get regions in the bounds set by trackbar

    res = cv2.bitwise_and(frame, frame, mask=mask)  #applying mask on coloured image using bitwise_and function and storing it as result=res

    cv2.imshow("frame", frame)                      #displaying orignal image,mask and resultant image(which due to loop give a video output) 
    cv2.imshow("mask", mask)
    cv2.imshow("res", res)

    key = cv2.waitKey(1)
    if key == 27:
        break

cap.release()
cv2.destroyAllWindows()
```
## references

[youtube video](https://www.youtube.com/watch?v=3D7O_kZi8-o&list=PLS1QulWo1RIa7D1O6skqDQ-JZ1GGHKK-K&index=14)

14.
# Simple Image Thresholding
Thresholding is a popular segmentation technique used for separating an object from its background.Process of thresholding involves comparing each pixel of an image with a predefined threshold value.

First output of threshold is ret but here we have written _ because we won't be using this variable anywhere.
First parameter in threshold is image or source
Second parameter in threshold method is threshold value and third parameter is maximum threshold value
Fourth parameter is threshold type(it can be of several types)

**cv.THRESH_BINARY** - We are comparing each and every value of pixel to threshold value and if pixel value < threshold value then pixel value = 0 and if pixel value > threshold value then pixel value = 255(white pixel)

**cv.THRESH_BINARY_INV** -Gives result opposite to cv.THRESH_BINARY.If pixel value < threshold value then pixel value = 255(white pixel)
and if pixel value > threshold value then pixel value = 0

**cv.THRESH_TRUNC** - Upto threshold, value of pixels will not be changed.After threshold, pixel values would be equal to threshold value.

**cv.THRESH_TOZERO** - When pixel value < threshold value, the value assigned to pixel will be zero(black pixel)

**cv.THRESH_TOZERO_INV** - Opposite of cv.THRESH_TOZERO.If pixel value > threshold value then pixel value will be zero otherwise pixel value would be equal to threshold value.

```python

import cv2 as cv
import numpy as np
img = cv.imread('gradient.png',0)

_, th1 = cv.threshold(img, 50, 255, cv.THRESH_BINARY)
_, th2 = cv.threshold(img, 200, 255, cv.THRESH_BINARY_INV)
_, th3 = cv.threshold(img, 127, 255, cv.THRESH_TRUNC)
_, th4 = cv.threshold(img, 127, 255, cv.THRESH_TOZERO)
_, th5 = cv.threshold(img, 127, 255, cv.THRESH_TOZERO_INV)

cv.imshow("Image", img)
cv.imshow("th1", th1)
cv.imshow("th2", th2)
cv.imshow("th3", th3)
cv.imshow("th4", th4)
cv.imshow("th5", th5)

cv.waitKey(0)
cv.destroyAllWindows()

```
15.
# ADAPTIVE THRESHOLDING

In **simple thresholding**, the threshold value is **global**, i.e., it is same for all the pixels in the image. **Adaptive thresholding is the method where the threshold value is calculated for smaller regions and therefore, there will be different threshold values for different regions.**

In OpenCV, you can perform Adaptive threshold operation on an image using the method **adaptiveThreshold()** of the **Imgproc** class. 

Following is the syntax of this method.

`adaptiveThreshold(src, dst, maxValue, adaptiveMethod, thresholdType, blockSize, C)`

This method accepts the following parameters −

**src**− An object of the class Mat representing the source (input) image.

**dst** − An object of the class Mat representing the destination (output) image.

**maxValue** − A variable of double type representing the value that is to be given if pixel value is more than the threshold value.

**adaptiveMethod** − A variable of integer the type representing the adaptive method to be used. This will be either of the following two values

- **ADAPTIVE_THRESH_MEAN_C** − threshold value is the mean of neighborhood area.

- **ADAPTIVE_THRESH_GAUSSIAN_C** − threshold value is the weighted sum of neighborhood values where weights are a Gaussian window.

**thresholdType** − A variable of integer type representing the type of threshold to be used.

**blockSize** − A variable of the integer type representing size of the pixelneighborhood used to calculate the threshold value.

**C** − A variable of double type representing the constant used in the both methods (subtracted from the mean or weighted mean).

## Code
```python

import cv2 as cv
import numpy as np

img = cv.imread('sudoku.png',0)
_, th1 = cv.threshold(img, 127, 255, cv.THRESH_BINARY)
th2 = cv.adaptiveThreshold(img, 255, cv.ADAPTIVE_THRESH_MEAN_C, cv.THRESH_BINARY, 11, 2);
th3 = cv.adaptiveThreshold(img, 255, cv.ADAPTIVE_THRESH_GAUSSIAN_C, cv.THRESH_BINARY, 11, 2);

cv.imshow("Image", img)
cv.imshow("THRESH_BINARY", th1)
cv.imshow("ADAPTIVE_THRESH_MEAN_C", th2)
cv.imshow("ADAPTIVE_THRESH_GAUSSIAN_C", th3)

cv.waitKey(0)
cv.destroyAllWindows()
```

## references

- [tutorialspoint](https://www.tutorialspoint.com/opencv/opencv_adaptive_threshold.htm)
- [youtube video](https://www.youtube.com/watch?v=Zf1F4cz8GHU&list=PLS1QulWo1RIa7D1O6skqDQ-JZ1GGHKK-K&index=17)
16.
```python
import cv2
from matplotlib import pyplot as plt

img = cv2.imread('lena.jpg',-1) # opencv reads an image in bgr format
cv2.imshow('image',img) # the image will be shown correctly as bgr format is used
cv2.waitKey(0)
cv2.destroyAllWindows()
plt.imshow(img)
plt.show()
# matplotlib reads in rgb format, therefore this will show image incorrectly
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) # to convert bgr format to rgb using opencv
plt.imshow(img)
plt.show()
# now img with true colors is shown
plt.imshow(img)
plt.xticks([]), plt.yticks([]) # hides the x and y value marks or axes in the image
plt.show()
```

```python
# using the code in the last tutorial to get 6 different images and to show them in a single matplotlib window

import cv2
import numpy as np
from matplotlib import pyplot as plt

img = cv2.imread('gradient.png', 0) # image involves different pixel values starting from 0 to 255

_, th1 = cv2.threshold(img, 50, 255, cv2.THRESH_BINARY)
_, th2 = cv2.threshold(img, 200, 255, cv2.THRESH_BINARY_INV)
_, th3 = cv2.threshold(img, 127, 255, cv2.THRESH_TRUNC)
_, th4 = cv2.threshold(img, 127, 255, cv2.THRESH_TOZERO)
_, th5 = cv2.threshold(img, 127, 255, cv2.THRESH_TOZERO_INV)

titles = ['Original', 'BINARY', 'BINARY_INV', 'TRUNC', 'TOZERO', 'TOZERO_INV'] # an array of titles
images = [img, th1, th2, th3, th4, th5] # array of matrices containing the information of different images

for i in range(6):
    plt.subplot(2,3, i+1) # arguments of this method are - no of rows, no of columns, index of the image (that is to be assigned)
    plt.imshow(images[i], 'gray') # image is picked of index i, when thresholding is done grayscale images are used so just put gray in second parameter
    plt.title([titles[i]]) # this method gives the title which is given as argument to the corresponding image
    plt.xticks([]), plt.yticks([])

plt.show()
```
17.
## Morphological Transformation
```Python

import cv2                                                                           
import numpy as np                                                                   # import various libraries
from matplotlib import pyplot as plt                                                  

img = cv2.imread('smarties.png', cv2.IMREAD_GRAYSCALE)                               # reading image named smarties is imported in grayscale
_, mask = cv2.threshold(img, 220, 255, cv2.THRESH_BINARY_INV)                        # the image is masked to convert to black or white

kernal = np.ones((5,5), np.uint8)                                                    # a kernal is created to use as a filter for pixels

dilation = cv2.dilate(mask, kernal, iterations=2)                                    # a pixel element is '1' if atleast one pixel under the kernel is '1'
erosion = cv2.erode(mask, kernal, iterations=1)                                      # a pixel in the original image (either 1 or 0) will be considered 1 only if all the pixels under the kernel is 1, otherwise it is eroded (made to zero)
opening = cv2.morphologyEx(mask, cv2.MORPH_OPEN, kernal)                             # opening is just another name of erosion followed by dilation
closing = cv2.morphologyEx(mask, cv2.MORPH_CLOSE, kernal)                            # closing is reverse of opening, dilation followed by erosion
mg = cv2.morphologyEx(mask, cv2.MORPH_GRADIENT, kernal)                              # it is the difference between dilation and erosion of an image
th = cv2.morphologyEx(mask, cv2.MORPH_TOPHAT, kernal)                                # it is the difference between input image and opening of the image

titles = ['image', 'mask', 'dilation', 'erosion', 'opening', 'closing', 'mg', 'th']  # defining array named 'titles' which has array elements as titles of images.
images = [img, mask, dilation, erosion, opening, closing, mg, th]                    # defining array named 'images' which has array the images.
for i in range(8):                                                                   # displaying the images
    plt.subplot(2, 4, i+1), plt.imshow(images[i], 'gray')
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])

plt.show()
```
18.

``` python
import cv2
import numpy as np
from matplotlib import pyplot as plt

img = cv2.imread('lena.jpg')
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)    #because we are using matplotlib

kernel = np.ones((5, 5), np.float32)/25       #creating the kernel for homogenous(average) filter
dst = cv2.filter2D(img, -1, kernel)           # using cv2.filter2D() to convolve over the image with the above defined kernel. 
                                              #It is a general function can be used with a customized kernel.
                                              #Here -1 is the depth(no. of channels) of the output image. (-1 means depth same as input image)
blur = cv2.blur(img, (5, 5))                  #Opencv has a default function for average filter(the one we implemented above)
                                              #kernel size can be adjusted.
gblur = cv2.GaussianBlur(img, (5, 5), 0)      #In gaussian blur we convolve over the image woth a different kind of kernel
                                              #(it is weighted in both x and y directions with the center being the highest weighted.)
                                              #Kernel size can be adjusted. 0 is the standard deviation of kernel values in x-direction.
median = cv2.medianBlur(img, 5)               #Median filter replaces the current pixel with the median value among the values in the kernel. 
                                              #Kernel size can be adjusted. Median filter excellent for salt and pepper noise. 
bilateralFilter = cv2.bilateralFilter(img, 9, 75, 75)   #Bilateral filter is helpful when you need to smoothen the image but keep the edges sharp.
                                                        # 9 is the diameter of pixel neighbourhood(equivalent to kernel size)
                                                        #next two parameters are sigmacolour and sigmaspace respectively(explained in the link below)
titles = ['image', '2D Convolution', 'blur', 'GaussianBlur', 'median', 'bilateralFilter']   
images = [img, dst, blur, gblur, median, bilateralFilter]
                                                                                #plotting all the images in a single window.
for i in range(6):
    plt.subplot(2, 3, i+1), plt.imshow(images[i], 'gray')
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])

plt.show()
```
[sigmacolour and sigmaspace](https://docs.opencv.org/2.4/modules/imgproc/doc/filtering.html?highlight=bilateralfilter#bilateralfilter)
19.
# Image Gradients and Edge Detection 
```Python
#Code for image gradient and Edge detection
#Image Gradient is directional change the intensity or color in an image

import numpy as np                                 #
import cv2                                         #importing numpy,opencv and matplotlib libraries.
import matplotlib.pyplot as plt                    #

img=cv2.imread('messi.jpg',cv2.IMREAD_GRAYSCALE)   #reading image named 'messi.jpg' from directory as a grayscale image

lap=cv2.Laplacian(img,cv2.CV_64F,ksize=3)          #Applying Laplacian gradient on img(1st arg) with datatype as 64 bit 
                                                   #float(2nd arg) and kernel size as 3(3rd arg).
                                                   #64 bit float is used due to the negative slop induced during conversion 
                                                   #from white to black while applying Laplacian gradient.
                                                   #Kernel size can be changed as 1,3,5,etc.                                                 
                                                   
sobelX=cv2.Sobel(img,cv2.CV_64F,1,0)               #Applying Sobel method of image gradient on image(1st arg) with datatype 
                                                   #64 bit float in x direction(3rd arg),not in y direction(4th arg)
                                                   #3rd and 4th arguments stand for SobleX and SobelY application. 
                                                   
sobelY=cv2.Sobel(img,cv2.CV_64F,0,1)               #Applying sobel method in y direction with similar arguments as before. 

lap=np.uint8(np.absolute(lap))                     #Taking absolute value of transformed laplacian image and converting back   
                                                   #the 'lap' image to unsighned 8 bit integer. 
sobelX=np.uint8(np.absolute(sobelX))               #similar process for sobelX image.
sobelY=np.uint8(np.absolute(sobelY))               #similar process for sobelY image.

sobelcombined=cv2.biwise_or(sobelX,sobely)         #combining both sobleX and sobleY using bitwise 'or' operator.

titles=['image','Laplacian','sobelX','sobelY',     #defining array named 'titles' which has array elements as titles of 
         'sobelcombined']                          #displaying images.
images=[img,lap,sobelX,sobelY,                     #defining array named 'images' which has array elemnts as displaying 
         sobelcombined]                            #images.
                                                   
for i in range(5):                                 #introducing for loop
  plt.subplot(2,3,i+1)                             #for displaying multiple images simultaneously in the format 2x3.         
  plt.imshow(images[i],'gray')                     #showing images in grayscale mode.
  plt.title(titles[i])                             #giving titles.
  plt.xticks([]),plt.yticks([])                    #giving zero ticks.
plt.show()                                         #displaying of images


#when we apply sobelx,sobely methods, change in intensities are along x,y directions respectively.
#combining sobelX and sobelY method gives us better result in edge detection.
#we can also include kernel size in sobelx and sobely method.
#increasing kernel size in Laplacian gradient deteriorates edge detection result.
```
20.
# Canny Edge Detector
The Canny edge detector is used to detect multiple edges in an image (using multi-stage algorithm). Canny Edge detection gives more precise edges and reduces noise as compared to Laplacian or Sobel method. The algorithm is mainly gray-scale. 
The detection algorithm is of essentially 5 steps.

### 1. Noise reduction
   Since the mathematics involved behind the scene are mainly based on derivatives (cf. Step 2: Gradient calculation), edge detection results are highly sensitive to image noise. One way to get rid of the noise on the image, is by applying Gaussian blur to smooth it. To do so, image convolution technique is applied with a Gaussian Kernel (3x3, 5x5, 7x7 etc…). The kernel size depends on the expected blurring effect. Basically, the smallest the kernel, the less visible is the blur. In our example, we will use a 5 by 5 Gaussian kernel.
   ![](https://miro.medium.com/max/1050/1*YpLYVBomcYNNbwncG5iP9Q.png)

### 2. Gradient calculation
   The Gradient calculation step detects the edge intensity and direction by calculating the gradient of the image using edge detection operators. Edges correspond to a change of pixels’ intensity. To detect it, the easiest way is to apply filters that highlight this intensity change in both directions: horizontal (x) and vertical (y)
When the image is smoothed, the derivatives Ix and Iy w.r.t. x and y are calculated. It can be implemented by convolving I with Sobel kernels Kx and Ky, respectively. 
![](https://miro.medium.com/max/1254/1*ZCyKWsmDoj6V-dNwKlKxyA.png)
   In the result some of the edges are thick and others are thin. Non-Max Suppression step will help us mitigate the thick ones.
Moreover, the gradient intensity level is between 0 and 255 which is not uniform. The edges on the final result should have the same intensity (i-e. white pixel = 255).

### 3. Non-max suppression
   The principle is simple: the algorithm goes through all the points on the gradient intensity matrix and finds the pixels with the maximum value in the edge directions. Let's take an example:
   ![](https://miro.medium.com/max/1094/1*CWrXNSbe7s4qSFr5vylyvQ.png)
   The upper left corner red box present on the above image, represents an intensity pixel of the Gradient Intensity matrix being processed. The corresponding edge direction is represented by the orange arrow with an angle of -pi radians (+/-180 degrees).
   ![](https://miro.medium.com/max/804/1*K-gnZg4_VPk57Xs0XflIrg.png)
   The edge direction is the orange dotted line (horizontal from left to right). The purpose of the algorithm is to check if the pixels on the same direction are more or less intense than the ones being processed. In the example above, the pixel (i, j) is being processed, and the pixels on the same direction are highlighted in blue (i, j-1) and (i, j+1). If one those two pixels are more intense than the one being processed, then only the more intense one is kept. Pixel (i, j-1) seems to be more intense, because it is white (value of 255). Hence, the intensity value of the current pixel (i, j) is set to 0. If there are no pixels in the edge direction having more intense values, then the value of the current pixel is kept.
   
### 4. Double Threshold
   The double threshold step aims at identifying 3 kinds of pixels: strong (high enough intensity to contribute to edge), weak (intensity value not high but not small enough to be considered irrelevant for edge detection), and non-relevant (non-relevant for the edge). Now you can see what the double thresholds holds for:
- High threshold is used to identify the strong pixels (intensity higher than the high threshold)
- Low threshold is used to identify the non-relevant pixels (intensity lower than the low threshold)
- All pixels having intensity between both thresholds are flagged as weak and the Hysteresis mechanism (next step) will help us identify the ones that could be considered as strong and the ones that are considered as non-relevant.
![](https://miro.medium.com/max/1332/1*FF6b8FJ2oppREoh9T-hdfA.png)

### 5. Edge tracking in hysteresis
   Based on the threshold results, the hysteresis consists of transforming weak pixels into strong ones, if and only if at least one of the pixels around the one being processed is a strong one, as described below:
   ![](https://miro.medium.com/max/1350/1*jnqS5hbRwAmU-sgK552Mgg.png)
   
There is a built-in function for Canny Edge Detection.
```Python
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('sports.jpg', 0) #read the image in gray-scale.
canny = cv2.Canny(img, 100, 200) 
#We need to provide two threshold values (argument 2 and 3) for hysteresis which is last step. To adjust threshold values add trackbar.
titles =['image', 'canny']
for i in range(2):
    plt.subplot(1,2,i+1)
    plt.imshow(images[i], 'gray')
    plt.title(titles[i])
    plt.xticks([]), plt.yticks([])
```
21.
# Image Pyramids

**Pyramid**, or **pyramid representation**, is a type of multi-scale signal representation developed by the computer vision, image processing and signal processing communities, in which a signal or an image is subject to repeated **smoothing** and **subsampling**. Pyramid representation is a predecessor to **scale-space representation** and **multiresolution analysis**. With Image pyramids, we can create images with different resolutions.

![Visual Representation of an Image Pyramid with 5 levels](https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/Image_pyramid.svg/300px-Image_pyramid.svg.png)

**There are two kinds of image pyramids:**
### Gaussian Pyramid
In a Gaussian pyramid, subsequent images are weighted down using a Gaussian average (Gaussian blur) and scaled down. Each pixel containing a local average corresponds to a neighborhood pixel on a lower level of the pyramid. This technique is used especially in texture synthesis.
Gaussian pyramids use **cv.pyrDown()** to decrease the resolution of the image and **cv.pyrUp()** to increase the resolution of the image. 
### Laplacian Pyramid
A Laplacian pyramid is very similar to a Gaussian pyramid but saves the difference image of the blurred versions between each levels. Only the smallest level is not a difference image to enable reconstruction of the high resolution image using the difference images on higher levels. This technique can be used in image compression. A level in Laplacian Pyramid is formed by the difference between that level in **Gaussian Pyramid** and **Expanded version of its upper level in Gaussian Pyramid**.

![Image to be changed](https://upload.wikimedia.org/wikipedia/en/thumb/7/7d/Lenna_%28test_image%29.png/220px-Lenna_%28test_image%29.png)

**In this video, the gaussian and laplacian images of the above image are made.**

**The code for the above conversion is:**
```python
import cv2
import numpy as np
img = cv2.imread("lena.jpg")                                                    # reading above image
layer = img.copy()                                                              # making a copy of the image
gaussian_pyramid_list = [layer]                                                 # creating a list of the gaussian images of the given image 

for i in range(6):                                                              # creating a for loop to get all the gaussian transformed versions of the image
    layer = cv2.pyrDown(layer)                                                  # reducing the resolution of the image 
    gaussian_pyramid_list.append(layer)                                         # adding the created image to the list 
    cv2.imshow(str(i), layer)                                                   # command to show the reduced resolution version of the image 

layer = gaussian_pyramid_list[5]                                                # assigning the most reduced image to layer                                            
cv2.imshow('upper level Gaussian Pyramid', layer)                               # showing the most reduced image
laplacian_pyramid_list = [layer]                                                # creating a list for laplacian converted images  

for i in range(5, 0, -1):                                                       # creating an inverse for loop to get all the laplacian transformed versions of the image
    gaussian_expanded = cv2.pyrUp(gaussian_pyramid_list[i])                     # increasing the resolution of the image from the gaussian list which represents the expanded version
    laplacian = cv2.subtract(gaussian_pyramid_list[i-1], gaussian_expanded)     # subtracting a gaussian image having the same resolution from expanded version 
    cv2.imshow(str(i), laplacian)                                               # showing the laplacian image 

cv2.imshow("Original image", img)                                               # showing the original image
cv2.waitKey(0)
cv2.destroyAllWindows()
```
22.
# Image Blending using Pyramids

One application of Pyramids is Image Blending. For example, in image stitching, you will need to stack two images together, but it may not look good due to discontinuities between images. In that case, image blending with Pyramids gives you seamless blending without leaving much data in the images. One classical example of this is the blending of two fruits, Orange and Apple.

![Apple and Orange image](http://opencv-python-tutroals.readthedocs.org/en/latest/_images/orapple.jpg)

**There are five steps to achieve this:**

1. Load the two images of apple and orange.
2. Find the Gaussian Pyramids for apple and orange (in this particular example, number of levels is 6).
3. From Gaussian Pyramids, find their Laplacian Pyramids.
4. Now join the left half of apple and right half of orange in each levels of Laplacian Pyramids.
5. Finally from this joint image pyramids, reconstruct the original image.

```python
import cv2
import numpy as np
apple = cv2.imread('apple.jpg')                                                                 # read apple image
orange = cv2.imread('orange.jpg')                                                               # read orange image 
print(apple.shape)
print(orange.shape)
apple_orange = np.hstack((apple[:, :256], orange[:, 256:]))                                     # adding the first half of apple and the second half of orange 

                                                                                                # generate Gaussian pyramid for apple
apple_copy = apple.copy()
gp_apple = [apple_copy]
for i in range(6):
    apple_copy = cv2.pyrDown(apple_copy)
    gp_apple.append(apple_copy)


                                                                                                # generate Gaussian pyramid for orange
orange_copy = orange.copy()
gp_orange = [orange_copy]
for i in range(6):
    orange_copy = cv2.pyrDown(orange_copy)
    gp_orange.append(orange_copy)

                                                                                                # generate Laplacian Pyramid for apple
apple_copy = gp_apple[5]
lp_apple = [apple_copy]
for i in range(5, 0, -1):
    gaussian_expanded = cv2.pyrUp(gp_apple[i])
    laplacian = cv2.subtract(gp_apple[i-1], gaussian_expanded)
    lp_apple.append(laplacian)

                                                                                                # generate Laplacian Pyramid for orange
orange_copy = gp_orange[5]
lp_orange = [orange_copy]
for i in range(5, 0, -1):
    gaussian_expanded = cv2.pyrUp(gp_orange[i])
    laplacian = cv2.subtract(gp_orange[i-1], gaussian_expanded)
    lp_orange.append(laplacian)

                                                                                                # Now add left and right halves of images in each level
apple_orange_pyramid = []                                                                       # creating a list for all the images formed by adding the laplacian halves of apple and orange 
n = 0
for apple_lap, orange_lap in zip(lp_apple, lp_orange):                                          # running for loop by creating a zip for laplacian apple and laplacian orange and assigning them to the variables
    n += 1
    cols, rows, ch = apple_lap.shape                                                            # getting number of columns, rows in the shape of apple
    laplacian = np.hstack((apple_lap[:, 0:int(cols/2)], orange_lap[:, int(cols/2):]))           # joining the halves of apple and orange
    apple_orange_pyramid.append(laplacian)                                                      # adding it to the list made above
                                                                                                # now reconstruct
apple_orange_reconstruct = apple_orange_pyramid[0]                                      
for i in range(1, 6):
    apple_orange_reconstruct = cv2.pyrUp(apple_orange_reconstruct)                              # increasing the resolution of the image
    apple_orange_reconstruct = cv2.add(apple_orange_pyramid[i], apple_orange_reconstruct)       # adding the reconstruct version to the image we made by adding the two halves

cv2.imshow("apple", apple)
cv2.imshow("orange", orange)
cv2.imshow("apple_orange", apple_orange)
cv2.imshow("apple_orange_reconstruct", apple_orange_reconstruct)                                # showing the blended image
cv2.waitKey(0)
cv2.destroyAllWindows()
```
23.
Contours are defined as the line joining all the points along the boundary of an image that are having the same intensity.
OpenCV has _findContour()_ function that helps in extracting the contours from the image. It works best on binary images, so we should first apply thresholding techniques, Sobel edges, etc.
The function returns a Python list of all the contours in the image. Each individual contour is a Numpy array of (x, y) coordinates of boundary points of the object.

``` python
import numpy as np
import cv2

img = cv2.imread('baseball.png')      #reading the image
imgray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)    # coverting the image to grayscale

# Applying threshold, here 0 is code for binary threshold method
ret, thresh = cv2.threshold(imgray, 127, 255, 0)   

# arguments passed are image whose contours are to be found,
# second is contour retreival mode and third countour approximation method
# we need to find contours in this way only defining two variables
contours, hierarchy = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_NONE)
print("Number of contours = " + str(len(contours)))
print(contours[0])

# for drawing contours on the image arguments passed are:-
# input image, where contours are stored, index of contour use -1 for drawing all contours
# color and thickness
cv2.drawContours(img, contours, -1, (0, 255, 0), 3)
cv2.drawContours(imgray, contours, -1, (0, 255, 0), 3)

# shows the image
cv2.imshow('Image', img)
cv2.imshow('Image GRAY', imgray)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
24.
# Detect Simple Geometric Shapes

## Goal

The aim of this code to know how can we detect simple Geometric Shapes using OpenCv library.

## Function:

(1). The functions ```approxPolyDP``` approximate a curve or a polygon with another curve/polygon with less vertices so that the distance between them is less or equal to the specified precision.

* [approxPolyDP](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html#approxpolydp) - ```cv2.approxPolyDP(curve, epsilon, closed[, approxCurve])```

| Argument	 | Function  |
| ---------	 |-----------|
| curve        	 | the contour of the curve                                               |
| epsilon     	 | the approximation accuracy (epsilon = 0.1\*cv2.arcLength(contour,True) |
| closed         | input True if the curve is closed else False				  |

(2). The function ```boundingRect``` calculates the up-right bounding rectangle of a point set, the function calculates and returns the minimal up-right bounding rectangle for the specified point set.

* [boundingRect](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html#boundingrect)
* [boundingRect2](https://docs.opencv.org/3.1.0/dd/d49/tutorial_py_contour_features.html) (refer to point 7) - 
```x,y,w,h = cv2.boundingRect(points)```

## Code

```python
import cv2                                                                                  
import numpy as np                                                                          
                                                                                            
img = cv2.imread('shapes.jpg')                                                             
imgGrey = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)                                             
_, thrash = cv2.threshold(imgGrey, 240, 255, cv2.THRESH_BINARY)                             
contours, _ = cv2.findContours(thrash, cv2.RETR_TREE, cv2.CHAIN_APPROX_NONE)                

for contour in contours:                                                                    
    approx = cv2.approxPolyDP(contour, 0.01*cv2.arcLength(contour, True), True)             #this method approximates a polygonal curve with a specific precision
    cv2.drawContours(img, [approx], 0, (0, 0, 0), 5)                                        
    x = approx.ravel()[0]                                                                   #coordinates of the shape to put Text
    y = approx.ravel()[1] - 15                                                              #ravel is a method to get coordinates
    if len(approx) == 3:                                                                    
        cv2.putText(img, 'Triangle', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))      
    elif len(approx) == 4:                                                                  
        x1, y1, w, h = cv2.boundingRect(approx)                                             #using boundingRect method get Width and
        aspectRatio =float(w)/h                                                             #Height and check the aspect ratio
        print(aspectRatio)                                                                  
        if aspectRatio >= 0.95 and aspectRatio<=1.05:                                       #considering noises check for a square or rectangle
            cv2.putText(img, 'Square', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))    
        else:                                                                               
            cv2.putText(img, 'Rectangle', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0)) 
    elif len(approx) == 5:                                                                  
        cv2.putText(img, 'Pentagon', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))      
    elif len(approx) == 10:                                                                 
        cv2.putText(img, 'Star', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))          
    else :                                                                                  
        cv2.putText(img, 'Circle', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))        

cv2.imshow("shapes", img)                                                                   
cv2.waitKey(0) & 0xFF                                                                       
cv2.destroyAllWindows()                                                                     
```
## References

* [YouTube Video](https://youtu.be/mVWQNeY1Pb4)
* [Structural Analysis and Shape Descriptors](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html#approxpolydp)
25.
# Detect Simple Geometric Shapes

## Goal

The aim of this code to know how can we detect simple Geometric Shapes using OpenCv library.

## Function:

(1). The functions ```approxPolyDP``` approximate a curve or a polygon with another curve/polygon with less vertices so that the distance between them is less or equal to the specified precision.

* [approxPolyDP](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html#approxpolydp) - ```cv2.approxPolyDP(curve, epsilon, closed[, approxCurve])```

| Argument	 | Function  |
| ---------	 |-----------|
| curve        	 | the contour of the curve                                               |
| epsilon     	 | the approximation accuracy (epsilon = 0.1\*cv2.arcLength(contour,True) |
| closed         | input True if the curve is closed else False				  |

(2). The function ```boundingRect``` calculates the up-right bounding rectangle of a point set, the function calculates and returns the minimal up-right bounding rectangle for the specified point set.

* [boundingRect](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html#boundingrect)
* [boundingRect2](https://docs.opencv.org/3.1.0/dd/d49/tutorial_py_contour_features.html) (refer to point 7) - 
```x,y,w,h = cv2.boundingRect(points)```

## Code

```python
import cv2                                                                                  
import numpy as np                                                                          
                                                                                            
img = cv2.imread('shapes.jpg')                                                             
imgGrey = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)                                             
_, thrash = cv2.threshold(imgGrey, 240, 255, cv2.THRESH_BINARY)                             
contours, _ = cv2.findContours(thrash, cv2.RETR_TREE, cv2.CHAIN_APPROX_NONE)                

for contour in contours:                                                                    
    approx = cv2.approxPolyDP(contour, 0.01*cv2.arcLength(contour, True), True)             #this method approximates a polygonal curve with a specific precision
    cv2.drawContours(img, [approx], 0, (0, 0, 0), 5)                                        
    x = approx.ravel()[0]                                                                   #coordinates of the shape to put Text
    y = approx.ravel()[1] - 15                                                              #ravel is a method to get coordinates
    if len(approx) == 3:                                                                    
        cv2.putText(img, 'Triangle', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))      
    elif len(approx) == 4:                                                                  
        x1, y1, w, h = cv2.boundingRect(approx)                                             #using boundingRect method get Width and
        aspectRatio =float(w)/h                                                             #Height and check the aspect ratio
        print(aspectRatio)                                                                  
        if aspectRatio >= 0.95 and aspectRatio<=1.05:                                       #considering noises check for a square or rectangle
            cv2.putText(img, 'Square', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))    
        else:                                                                               
            cv2.putText(img, 'Rectangle', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0)) 
    elif len(approx) == 5:                                                                  
        cv2.putText(img, 'Pentagon', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))      
    elif len(approx) == 10:                                                                 
        cv2.putText(img, 'Star', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))          
    else :                                                                                  
        cv2.putText(img, 'Circle', (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.5, (0, 0, 0))        

cv2.imshow("shapes", img)                                                                   
cv2.waitKey(0) & 0xFF                                                                       
cv2.destroyAllWindows()                                                                     
```
## References

* [YouTube Video](https://youtu.be/mVWQNeY1Pb4)
* [Structural Analysis and Shape Descriptors](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html#approxpolydp)
26.

~~~python
import numpy as np
import cv2
from matplotlib import pyplot as plt

img=cv2.imread("lena.jpg")
img1=cv2.imread("lena.jpg",0)
hist=cv2.calcHist((img1),[0],None,[256],[0,256])#first argument is source,second argument is channel number
                                                # to find the histogram of full image we have to give third argument as none
                                                #fourth argument is bin count,fifth argument will be the min and max range on x axis

b,g,r=cv2.cv2.split(img)#split the img array into three diffrent channels

cv2.imshow("img",img)
#cv2.imshow("b",b)
#cv2.imshow("g",g)
#cv2.imshow("r",r)


plt.hist(b.ravel(),256,[0,256])#b.ravel is used to flatten the b array
                               #second argument is the maximum value of pixel
                               #third argument is the range
plt.hist(g.ravel(),256,[0,256])
plt.hist(r.ravel(),256,[0,256])

plt.show()

cv2.waitKey(10000)
cv2.destroyAllWindows()


~~~
27.
# Template Matching Using OpenCV
```Python
#code for template matching using opencv
#Template matching is searching and finding location of template image in original reference image

import cv2                                                           #importing opencv and 
import numpy as np                                                   #numpy libraries

img = cv2.imread("messi.jpg")                                        #reading the original image 'messi.jpg'
grey_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)                     #converting img into grayscale image
template = cv2.imread("messi_face.jpg", 0)                           #reading the template image 'messi_face.jpg' 

w, h = template.shape[::-1]                                          #assigning width and height of template image into 
                                                                     #variables w and h.
                                                                     
res = cv2.matchTemplate(grey_img, template, cv2.TM_CCORR_NORMED )    #template matching of 'template'(2nd arg) with respect 
                                                                     #'grey_img'(1st arg) using a method called 
                                                                     #'TM_CCORR_NORMED'(3rd arg)
                                                                     
print(res)                                                           #prints matrix containing decimal values
                                                                     #we have to extract all the brightest points from res 
                                                                     #matrix.The point where template images's topleft corner
                                                                     #matches with original image,res will have its brightest
                                                                     #point there.
                                                                     
threshold = 0.99;                                                    #filtering out brightest points inside matrix by giving 
loc = np.where(res >= threshold)                                     #threshold value.Increasing threshold value will give 
                                                                     #less no.of values and thus we can find the brightest 
                                                                     #point.
print(loc)                                                           #printing the desired brightest points.        

for pt in zip(*loc[::-1]):                                           #for loop is used in case we get multiple no.of  
                                                                     #desired templates in same image.
    cv2.rectangle(img, pt, (pt[0] + w, pt[1] + h), (0, 0, 255), 2)   #drawing rectangle around the original image,same as the 
                                                                     #same as the size of template with img(1st arg),
                                                                     #iterating variable(2nd arg),width and height(3rd arg),
                                                                     #red colour(4th arg),thickness(5th arg)

cv2.imshow("img", img)                                               #displaying of image with rectangle drawn.
cv2.waitKey(0)
cv2.destroyAllWindows()

#increasing threshold will give more no. of points on x axis and y axis.Thus the same rectangle is drawn multiple times.
#decreasing threshold value will give us exact points resulting in precision to draw the rectangle.
#Other than 'cv2.TM_CCORR_NORMED ' method ,there are another template matching methods also.

```
28.
# HOUGH TRANSFORM

Hough Transform is basically a feature extraction technique used in image analysis, computer vision and digital image processing. The aim is to find instances (though imperfect) of objects within a certian class of shapes governed by some sort of voting procedure. 

A very high level glimpse is that we transform our co-ordinates to a new parametric space. Using this, the objects that we are trying to search for are found as the local maxima in accumulator space contructed by the algorithm. 

Initially, the transform was aimed at extracting probable lines in the image but now it has been extended to identify some classes of shapes. 

One could argue that the edge detector can do the job of finding straight lines. Indeed, to some extent that works but that has certain limitations - 
* There can be missing points/pixels on the desired curve obtained using the edge detector.
* There can be devations between the actual curves and the desired curves that can lead to some sort of non-detectability. 

So, Hough Transform Algorithm helps to deal with these imperfections inherently present in the data or caused by the edge detector. This algorithm develops some sort of grouping of the edge pixels and based on the parameters set, tries to see if the desired object can be traced in the image depending on the explicit voting procedure that is undertaken. 

Let's now delve into the technical details of the Transform and the corresponding algorithm.

### Cartesian Form 
  The general equation of a straight line is given as by : *y = mx + c*. Now think about transforming it to the *(m, c)* space. How does the line look in the *(m, c)* space? That look like a point. And any general point on the line is a line in the *(m, c)* space. This can be realised by representing the equation in the following format : *c = -mx + y*, so the slope of this line is *x* and the intercept being *y*.  
  So this now gives a general idea to see if a line is present in the image or not. For all points on the edge, we draw the corresponding line on the *(m, c)* space and in the accumulator space, we obtain the votes i.e. the number of lines through it, of each co-ordinate of the *(m, c)* space. If it is more than some threshold, then a line with that *(m, c)* is said to exist in the image and that completes our job. 


  
  ![640px-Hough_transform_diagram svg](https://user-images.githubusercontent.com/55907159/79689144-7f2fab80-8270-11ea-80e4-2acc97e5711f.png)



  The above diagram gives some insights to what is actually going on. Bascially, this shows that the *(m, c)* with the highest number of votes is probably the object we are looking for. In this case, we see that (405, 60&deg;) is somewhat and optimal choice for the *(r, &theta;)* of the line.

  We can extend this idea to the *(r, &theta;)* space i.e. the Polar form using the Hesse Normal Form of a line : *r = xcos&theta; + ysin&theta;*. 

### Polar Form 
  The general equation of a line in normal form is : *r = xcos&theta; + ysin&theta;*. Now, each point on the line transformed into the *(r, &theta;)* space gives some sort of a sinusoidal curve in contrast to the line in the *(m, c)* space.
  In the same way as the cartesian form, we draw the sinusoids in the *(r, &theta;)* space and in the accumulator space, we obtain the votes i.e. the number of curves through it, of each co-ordinate of the *(r, &theta;)* space. If it is greater than some threshold value, then a line with *(r, &theta;)* exists on the image. 

The polar form is preferred over the cartesian form because of the fact that for vertical lines, the slope blows up and hence it is not possible to represent the line in *(m, c)* space, but that limitation doesn' show up in polar form.  

---

### References

* [Wikipedia](https://en.wikipedia.org/wiki/Hough_transform)
* [Youtube Video](https://www.youtube.com/watch?v=7m-RVJ6ABsY&list=PLS1QulWo1RIa7D1O6skqDQ-JZ1GGHKK-K&index=32)
29.


