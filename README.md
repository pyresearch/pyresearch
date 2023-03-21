## Pyresearch

This is a Computer vision package that makes its easy to run Image processing and AI functions. At the core it uses [OpenCV](https://github.com/opencv/opencv) and [Mediapipe](https://github.com/google/mediapipe) libraries. 



## Installation
You can  simply use pip to install the latest version of pyresearch.

`pip install pyresearch`


<hr>

### 60 FPS Face Detection

<pre>
from pyresearch.FaceDetectionModule import FaceDetector
import cv2

cap = cv2.VideoCapture(0)
detector = FaceDetector()

while True:
    success, img = cap.read()
    img, bboxs = detector.findFaces(img)

    if bboxs:
        # bboxInfo - "id","bbox","score","center"
        center = bboxs[0]["center"]
        cv2.circle(img, center, 5, (255, 0, 255), cv2.FILLED)

    cv2.imshow("Image", img)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
cv2.destroyAllWindows()

</pre>



<p align="center">
<video src="https://user-images.githubusercontent.com/34125851/226322060-6e7da509-718b-40b7-8515-ea84e93687ec.mov"></video>
</p>

<hr>


### Face Mesh Detection
<hr>


<pre>

from pyresearch.FaceMeshModule import FaceMeshDetector
import cv2

cap = cv2.VideoCapture(0)
detector = FaceMeshDetector(maxFaces=2)
while True:
    success, img = cap.read()
    img, faces = detector.findFaceMesh(img)
    if faces:
        print(faces[0])
    cv2.imshow("Image", img)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
cv2.destroyAllWindows()

</pre>



<p align="center">
<video src="https://user-images.githubusercontent.com/34125851/226390465-0c400a81-b3f7-4384-b057-d1b5a9531f5b.mov"></video>
</p>

<hr>






### FPS
<hr>


<pre>

import pyresearch
import cv2

fpsReader = pyresearch.FPS()

cap = cv2.VideoCapture(0)


cap.set(3, 1280)

cap.set(4, 720)

while True:

    success, img = cap.read()
   
    fps, img = fpsReader.update(img,pos=(50,80),color=(0,255,0),scale=5,thickness=5)
   
    cv2.imshow("Image", img)
   
    if cv2.waitKey(1) & 0xFF == ord('q'):
   
        break

cap.release()
cv2.destroyAllWindows()

</pre>



<p align="center">
<video src="https://user-images.githubusercontent.com/34125851/226392480-efd10445-6d6c-4878-b67b-152c4ec50726.mov"></video>
</p>

<hr>






### Stack Images

<hr>


<pre>

import pyresearch
import cv2

cap = cv2.VideoCapture(0)
cap.set(3, 1280)
cap.set(4, 720)

while True:
    success, img = cap.read()
    imgGray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    imgList = [img, img, imgGray, img, imgGray, img,imgGray, img, img]
    stackedImg = pyresearch.stackImages(imgList, 3, 0.4)

    cv2.imshow("stackedImg", stackedImg)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
cv2.destroyAllWindows()


</pre>



<p align="center">
<video src="https://user-images.githubusercontent.com/34125851/226393643-cddf28df-781d-47bf-8ec8-9f25ca53d311.mov"></video>
</p>

<hr>



### Hand Tracking

<hr>


#### Basic Code Example 
<pre>
from pyresearch.HandTrackingModule import HandDetector
import cv2

cap = cv2.VideoCapture(0)

detector = HandDetector(detectionCon=0.8, maxHands=2)

while True:
    # Get image frame

    success, img = cap.read()

    # Find the hand and its landmarks

    hands, img = detector.findHands(img)  # with draw

    # hands = detector.findHands(img, draw=False)  # without draw

    if hands:

        # Hand 1

        hand1 = hands[0]

        lmList1 = hand1["lmList"]  # List of 21 Landmark points

        bbox1 = hand1["bbox"]  # Bounding box info x,y,w,h

        centerPoint1 = hand1['center']  # center of the hand cx,cy

        handType1 = hand1["type"]  # Handtype Left or Right

        fingers1 = detector.fingersUp(hand1)

        if len(hands) == 2:
            # Hand 2
            hand2 = hands[1]
            lmList2 = hand2["lmList"]  # List of 21 Landmark points
            bbox2 = hand2["bbox"]  # Bounding box info x,y,w,h
            centerPoint2 = hand2['center']  # center of the hand cx,cy
            handType2 = hand2["type"]  # Hand Type "Left" or "Right"

            fingers2 = detector.fingersUp(hand2)

            # Find Distance between two Landmarks. Could be same hand or different hands
            length, info, img = detector.findDistance(lmList1[8], lmList2[8], img)  # with draw
            # length, info = detector.findDistance(lmList1[8], lmList2[8])  # with draw
    # Display
    cv2.imshow("Image", img)
    cv2.waitKey(1)
cap.release()
cv2.destroyAllWindows()

</pre>

 

<p align="center">
<video src="https://user-images.githubusercontent.com/34125851/226393643-cddf28df-781d-47bf-8ec8-9f25ca53d311.mov"></video>
</p>

<hr>

