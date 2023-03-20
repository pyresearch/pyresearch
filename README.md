## Pyresearch


## Installation
You can  simply use pip to install the latest version of cvzone.

`pip install pyresearch`

<hr>

### 60 FPS Face Detection

<hr>

<p align="center">
<video src="https://user-images.githubusercontent.com/34125851/226322060-6e7da509-718b-40b7-8515-ea84e93687ec.mov"></video>
</p>

<pre>
from cvzone.FaceDetectionModule import FaceDetector
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

<hr>
