# Ball Tracking Robot
The ball tracking robot uses a Pi camera and an ultrasonic sensor to locate the ball. The robot uses motors to follow or intercept the ball while maintaining a set distance. The computer vision and the PID control make it complex and challenging

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Elian C | St. Joseph's Institution International  | Robotics and Computer Vision | Grade 9

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/3RR2q0Sp2D4?si=z95kCTO16c_35QIf" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Code for the Ultrasonic Sensor Test

```python
import RPi.GPIO as GPIO
import time
GPIO.setmode(GPIO.BCM)
GPIO_TRIGGER1=5
GPIO_ECHO1=6
GPIO_TRIGGER3=16
GPIO_ECHO3=26
GPIO.setup(GPIO_TRIGGER1,GPIO.OUT)
GPIO.setup(GPIO_ECHO1,GPIO.IN)
GPIO.setup(GPIO_TRIGGER3,GPIO.OUT)
GPIO.setup(GPIO_ECHO3,GPIO.IN)
GPIO.output(GPIO_TRIGGER1,False)
GPIO.output(GPIO_TRIGGER3,False)
def sonar(GPIO_TRIGGER,GPIO_ECHO):
      start=0
      stop=0
      GPIO.setup(GPIO_TRIGGER,GPIO.OUT)
      GPIO.setup(GPIO_ECHO,GPIO.IN)
      GPIO.output(GPIO_TRIGGER,False)
      time.sleep(0.01)
      GPIO.output(GPIO_TRIGGER,True)
      time.sleep(0.00001)
      GPIO.output(GPIO_TRIGGER,False)
      begin=time.time()
      while GPIO.input(GPIO_ECHO)==0 and time.time()<begin+0.05:
            start=time.time()
      while GPIO.input(GPIO_ECHO)==1 and time.time()<begin+0.1:
            stop=time.time()
      elapsed=stop-start
      distance=elapsed*34000
      distance=distance/2
      print ("Distance: %.1f"%distance)
      return distance
while True:
      distanceR=sonar(GPIO_TRIGGER3,GPIO_ECHO3)
      distanceL=sonar(GPIO_TRIGGER1,GPIO_ECHO1)
      time.sleep(1)
GPIO.cleanup()
```

# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/wWM_3ryNEk0?si=eCjt4IS2Hsm3CGhY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Code for the Pi Camera and Motors Test

Pi Camera Code:
```python3
from picamera2 import Picamera2
import cv2
import numpy as np
import time
def segment_colour(frame):
    hsv_roi=cv2.cvtColor(frame,cv2.COLOR_BGR2HSV)
    mask_1=cv2.inRange(hsv_roi,np.array([160,160,10]),np.array([180,255,255]))
    ycr_roi=cv2.cvtColor(frame,cv2.COLOR_BGR2YCrCb)
    mask_2=cv2.inRange(ycr_roi, np.array((0.,165.,0.)),np.array((255., 255., 255.)))
    mask=mask_1|mask_2
    kern_dilate=np.ones((8,8),np.uint8)
    kern_erode=np.ones((3,3),np.uint8)
    mask=cv2.erode(mask,kern_erode)
    mask=cv2.dilate(mask,kern_dilate)
    return mask
def find_blob(blob):
    largest_contour=0
    cont_index=0
    contours,hierarchy=cv2.findContours(blob,cv2.RETR_CCOMP,cv2.CHAIN_APPROX_SIMPLE)
    for idx,contour in enumerate(contours):
        area=cv2.contourArea(contour)
        if (area>largest_contour):
            largest_contour=area
            cont_index=idx
    r=(0,0,2,2)
    if len(contours)>0:
        r=cv2.boundingRect(contours[cont_index])
    return r,largest_contour
camera=Picamera2()
config=camera.create_preview_configuration(main={"size": (160, 120), "format": "RGB888"})
camera.configure(config)
camera.start()
time.sleep(0.1)
while True:
    frame=camera.capture_array()
    frame=cv2.flip(frame, 1)
    mask_red=segment_colour(frame)
    loct,area=find_blob(mask_red)
    x,y,w,h=loct
    if (w*h)>=10:
        cv2.rectangle(frame,(x,y),(x+w,y+h),(0,255,0),2)
        centre_x=int(x+w/2)
        centre_y=int(y+h/2)
        cv2.circle(frame, (centre_x,centre_y),3,(0,110,255),-1)
        print("Ball found - area: %d centre:(%d, %d)" % (area, centre_x,centre_y))
    else:
        print("No ball found")
    cv2.imshow("Camera feed", frame)
    cv2.imshow("Red mask", mask_red)
    if cv2.waitKey(1)&0xff==ord('q'):
        break
camera.stop()
cv2.destroyAllWindows()
```

Motor Test Code:
```python3
import RPi.GPIO as GPIO
import time
GPIO.setmode(GPIO.BCM)
MOTOR1A=22
MOTOR1B=27
MOTOR2A=24
MOTOR2B=23
GPIO.setup(MOTOR1A,GPIO.OUT)
GPIO.setup(MOTOR1B,GPIO.OUT)
GPIO.setup(MOTOR2A,GPIO.OUT)
GPIO.setup(MOTOR2B,GPIO.OUT)
def forward():
      GPIO.output(MOTOR1A,GPIO.HIGH)
      GPIO.output(MOTOR1B,GPIO.LOW)
      GPIO.output(MOTOR2A,GPIO.HIGH)
      GPIO.output(MOTOR2B,GPIO.LOW)
def reverse():
      GPIO.output(MOTOR1A,GPIO.LOW)
      GPIO.output(MOTOR1B,GPIO.HIGH)
      GPIO.output(MOTOR2A,GPIO.LOW)
      GPIO.output(MOTOR2B,GPIO.HIGH)
def rightturn():
      GPIO.output(MOTOR1A,GPIO.HIGH)
      GPIO.output(MOTOR1B,GPIO.LOW)
      GPIO.output(MOTOR2A,GPIO.LOW)
      GPIO.output(MOTOR2B,GPIO.HIGH)
def leftturn():
      GPIO.output(MOTOR1A,GPIO.LOW)
      GPIO.output(MOTOR1B,GPIO.HIGH)
      GPIO.output(MOTOR2A,GPIO.HIGH)
      GPIO.output(MOTOR2B,GPIO.LOW)
def stop():
      GPIO.output(MOTOR1A,GPIO.LOW)
      GPIO.output(MOTOR1B,GPIO.LOW)
      GPIO.output(MOTOR2A,GPIO.LOW)
      GPIO.output(MOTOR2B,GPIO.LOW)
print("Forward")     
forward()
time.sleep(3)
stop()
time.sleep(1)
print("Reverse")
reverse()
time.sleep(3)
stop()
time.sleep(1)
print("Right")
rightturn()
time.sleep(3)
stop()
time.sleep(1)
print("Left")
leftturn()
time.sleep(3)
stop()
GPIO.cleanup()
```

# Final Milestone

# Schematics 
 [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Screwdriver | Assembling the robot chassis | $20.27 | <a href="https://www.amazon.sg/dp/B0BBFJ2XKY?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| H-Bridge Motor Drive | Controls the direction and speed of the DC Motors | $20.51 | <a href="https://www.amazon.sg/VKLSVAN-Channel-H-Bridge-Stepper-Controller/dp/B0DQPRDHSK/ref=sr_1_1?crid=Y8BXRSLRBPA2&dib=eyJ2IjoiMSJ9.N12Bqdf_2P8Sg-7hcxYlDFdt5Z4RdXTwKJO_O8gKZyxiHskn-fX8uaW0cgysQlNzSFdROvS8e3FcUe0l00L2-5dAW1d-Rlnw-cVgMJMF-gQlFt_OYgWtLGY7JOvS8YMSjqQ5XiUUDvqhGPtj-Z0rl4iCA0UL3GTLccxvOxph2dm8asICSbQS_waohnQv3jnLPt4Em2QdC7mOdPrb3AZmzTr8uudnXNQxHyM12Qb7HFkpzrYUDLJvCNcm4GpfMWZuPCzbj4U5sMbTd0MenIPGtimoEHj_3oT4jnWfwy3ha9I.yukHYovBVQjkpeKhMBX20XnFG99hJxHm1T11Qm8Gbb4&dib_tag=se&keywords=H-bridge&qid=1782927562&sprefix=h-bri%2Caps%2C278&sr=8-1&th=1"> Link </a> |
| Raspberry Pi 4 | Runs the Python code that processes the camera feed, calculates PID values, and sends GPIO signals to the H-Bridge to control the motors | $216.27 | <a href="https://www.amazon.sg/dp/B0C8LV6VNZ?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Multimeter | Checks the voltage of wires to prevent short circuit | $25.99 | <a href="https://www.amazon.sg/dp/B01ISAMUA6?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Ultrasonic Sensor | Measures the distance to the ball | $25.35 | <a href="https://www.amazon.sg/dp/B0CQCCGXCP?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Chassis Kit | Provides the physical framework to mount and support all components including wheels and the Raspberry Pi | $24.32 | <a href="https://www.amazon.sg/dp/B01LXY7CM3?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Pi Camera | Captures the live video feed, which the code then processes to detect the ball's colour and calculate its position relative to the centre of the frame | $24.45 | <a href="https://www.amazon.sg/dp/B07RWCGX5K?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1"> Link </a> |
| Batteries | Provides power for the motors| $29.86 | <a href="https://www.amazon.sg/dp/B0035LCFNQ?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1"> Link </a> |
| Motor Dual DC | Drives the wheels under the control of the H-Bridge | $19.80 | <a href="https://www.amazon.sg/dp/B09N6NXP4H?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Foam Ball | The target object that the robot tracks and intercepts | $12.95 | <a href="https://www.amazon.sg/dp/B000KYQ406?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Electronics Kit | Provides the breadboard and jumper wires to connect components such as the H-Bridge, ultrasonic sensors, and motors | $9.99 | <a href="https://www.amazon.com/dp/B01ERP6WL4?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |

# Other Resources/Examples

- https://www.instructables.com/Ball-Tracking-Robot

