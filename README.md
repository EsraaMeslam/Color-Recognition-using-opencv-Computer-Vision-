steps of the project

<br>
Capture Video:
<br>
cap = cv2.VideoCapture(0)
<br>
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 700)
<br>
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 400)
<br>



<br>
Processing Loop:

<br>
<br>
Capture Frame:
<br>
_, frame = cap.read()
<br>
<br>
Convert to HSV:
<br>
hsv_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
<br><br>
Determine Center Pixel:
<br>
height, width, _ = frame.shape<br>
cx, cy = int(width / 2), int(height / 2)<br>
pixel_center = hsv_frame[cy, cx]<br>
hue_value = pixel_center[0]<br><br>

Identify Color:<br>

if hue_value < 5:<br>
    color = "RED"<br>
elif hue_value < 15:<br>
    color = "ORANGE"<br>
elif hue_value < 21:<br>
    color = "YELLOW"<br>
elif hue_value < 83:<br>
    color = "GREEN"<br>
elif hue_value < 128:<br>
    color = "BLUE"<br>
elif hue_value < 153:<br>
    color = "VIOLET"<br>
elif hue_value < 170:<br>
    color = "PINK"<br>
else:<br>
    color = "Undefined"<br>
Display Color on Frame:<br><br>

pixel_center_bgr = frame[cy, cx]<br>
b, g, r = int(pixel_center_bgr[0]), int(pixel_center_bgr[1]), int(pixel_center_bgr[2])<br>
cv2.putText(frame, color, (cx - 70, cy + 50), cv2.FONT_HERSHEY_SIMPLEX, 1, (b, g, r), 2)<br>
cv2.circle(frame, (cx, cy), 5, (25, 25, 25), 3)
cv2.imshow("Frame", frame)
Exit on ESC:
python
Copy code
key = cv2.waitKey(1)
if key == 27:
    break
Release Resources:

python
Copy code
cap.release()
cv2.destroyAllWindows()
