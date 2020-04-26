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

