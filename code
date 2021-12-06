import cv2
import numpy as np

def traffic_signal(image):
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    blurred = cv2.medianBlur(gray, 25) 
    signal=[]
    def cb(p):
        if p[0]>=160 and p[1]<=20 and p[2]<=100:
            return True
        return False

    circles = cv2.HoughCircles(blurred, cv2.HOUGH_GRADIENT, 1, 10, param1=50, param2=50, minRadius=1, maxRadius=100)
    
    if circles is not None:
        circles = np.uint16(np.around(circles))
        for i in circles[0,:]:
            color=image[i[1],i[0]]
            if cb(image[i[1]+i[2],i[0]+i[2]]) and cb(image[i[1]-i[2],i[0]-i[2]]):
                if color[0]<=20 and color[1]<=100 and color[2]>=160:
                    signal.append("RED")
                if color[0]<=20 and color[1]>=160 and color[2]<=100:
                    signal.append("GREEN")
                if color[0]<=20 and color[1]>=160 and color[2]>=160:
                    signal.append("YELLOW")
                    
        return signal

if __name__ == "__main__":
    for z in range(1,7):
        img = cv2.imread('test'+str(z)+'.jpeg')
        signal=traffic_signal(img)
        if len(signal)==1:
            print (signal[0])
        else:
            print("ERROR")
   
