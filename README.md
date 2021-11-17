# HAND GESTURE RECOGNITION
소개
이 프로젝트는 파이썬 2.7에서 OpenCV를 사용하여 손 인식 및 손동작 인식 시스템을 구현합니다. 히스토그램 기반 접근 방식은 배경 영상에서 손을 분리하는 데 사용됩니다. 최적의 결과를 얻기 위해 배경 삭제(취소) 기술이 사용됩니다. 검출된 손은 손가락과 손바닥의 위치와 치수를 인식하기 위해 윤곽과 볼록 껍질을 찾아 처리하고 모델링합니다. 마지막으로, 제스처 객체는 정의된 제스처 사전과 비교되는 인식된 패턴에서 생성됩니다.

### INTRODUCTION
This project implements a hand recognition and hand gesture recognition system using OpenCV on Python 2.7. A histogram based approach is used to separate out a hand from the background image. Background cancellation techniques are used to obtain optimum results. The detected hand is then processed and modelled by finding contours and convex hull to recognize finger and palm positions and dimensions. Finally, a gesture object is created from the recognized pattern which is compared to a defined gesture dictionary.
플랫폼: 파이썬 2.7

**Platform:** Python 2.7
라이브러리: OpenCV 2.4.8, Numpy

**Libraries:** OpenCV 2.4.8, Numpy
하드웨어 요구사항: 카메라/웹캠

**Hardware Requirements:** Camera/Webcam
사용법
HandRecognition.py를 실행하여 프로그램을 시작합니다.

### USAGE
Windows 사용자 참고: 모든 .py 파일에서 이 줄을 제거하십시오('#!/usr/bin/python'). 그렇지 않으면 오류가 발생할 수 있습니다.

Run HandRecognition.py to begin the program.
카메라 피드를 보여주는 창이 나타납니다. 창의 오른쪽에 직사각형 프레임이 있습니다. 그것이 모든 감지와 인식이 작동하는 틀입니다.

**Note for Windows users:**
Remove this line from all .py files: '#!/usr/bin/python' or else you might get some error.
시작하기 전에 배경 환경만 캡처할 수 있도록 손과 몸을 프레임 바깥에 두고 'b'를 누릅니다. 이렇게 하면 배경이 캡처되고 모델이 만들어집니다. 이 모델은 프로그램 설정이 완료되면 캡처한 모든 프레임에서 배경을 제거하는 데 사용됩니다.

You will find a window that shows your camera feed. Notice a rectangular frame on the right side of the window. That's the frame where all the detection and recognition works.
이제 손 히스토그램을 캡처해야 합니다. 프레임에 있는 9개의 작은 상자 위에 손을 올려서 손의 최대 음영 범위를 포착합니다. 최상의 결과를 위해 상자 부위에 그림자나 공극이 나타나지 않도록 하십시오. 'c'를 눌러 손을 캡처하고 히스토그램을 생성합니다.

To begin, keep your hand and body outside the frame, so as to capture just the background environment, and press 'b'. This will capture the background and create a model of it. This model will be used to remove background from every frame captured once the program setup is complete. 
이제 설정이 완료되었습니다. 이제, 여러분은 손을 직사각형 틀 안에 두면, 그것이 감지되고 여러분은 손바닥 영역 안에 있는 원을 볼 수 있을 것입니다. 그 안에서 손가락 쪽으로 선이 돌출되어 있습니다. 손을 움직이거나, 손가락 몇 개를 숨기거나, 프로그램에 구현된 샘플 제스처 중 하나를 시도해 보세요.

Now, you have to capture your hand histogram. Place your hand over the 9 small boxes in the frame so as to capture the maximum range of shades of your hand. Don't let any shadow or air gap show on the boxed areas for best results. Press 'c' to capture the hand and generate a histogram. 
구현된 샘플 제스처는 설명서에 스크린샷으로 설명되어 있습니다.

The setup is now complete. Now you will see, by keeping your hand inside the rectangular frame, it gets detected and you will notice a circle inside your palm area, with lines projecting out from it towards your fingers. Try moving your hands, hiding a few fingers or giving it one of the sample gestures implemented in the program.
그것들은 다음과 같습니다:

The sample gestures implemented are described with screenshots in the documentation. 
검지와 가운뎃손가락으로 "V"를 합니다.

They are:
엄지손가락과 집게손가락으로 뒤집힌 "L"L"합니다

1. "V" with your index and middle finger
집게손가락을 수직으로 가리킵니다

2. A flipped "L" with thumb and index finger
참고: 프로그램을 중지하려면 언제든지 'q'를 누르고 프로그램을 다시 시작하려면 'r'를 누르십시오.

3. Pointing with your index finger in vertical position
어떻게 작동하죠?
"docs" 폴더의 구현에 대한 자세한 설명은 전체 설명서를 참조하십시오.

**Note:** Press 'q' at any time to stop the program or 'r' to restart the program.
설정 중에 먼저 사용자가 'b'를 누르면 배경 모델이 생성됩니다. 그런 다음 사용자가 'c'를 눌러 손을 샘플로 제공하면 히스토그램이 생성됩니다. 설정이 완료되면 프로그램은 다음과 같은 무한 루프로 들어갑니다.

### HOW DOES IT WORK?
카메라 입력 프레임이 numpy 배열에 저장됩니다. 배경 모델에 따라 마스크가 생성되어 프레임에 적용됩니다. 이렇게 하면 캡처된 프레임에서 배경이 제거됩니다. 이제 전경만 포함하는 프레임이 HSV 색상 공간으로 변환된 다음 히스토그램 비교(백 투영 생성)가 수행됩니다. 이것은 우리에게 감지된 손을 남겨줍니다. 틀에서 적절한 손 모양을 얻기 위해 형태학과 매끈함을 적용했습니다. 임계값은 이 이미지를 이진 이미지로 변환합니다.

Read full documentation for detailed explanation about implementation in "docs" folder.
다음으로 얻은 이진 이미지의 윤곽을 찾고 가장 큰 윤곽을 찾아 볼록 껍질을 찾습니다.

During setup, first a background model is generated when the user presses 'b'. Then, a histogram is generated when the user provides his hand as a sample by pressing 'c'. When the setup is completed, the program goes into an infinite while loop which does as follows.
가장 큰 윤곽선의 점을 사용하여 윤곽선 내부에 새겨진 가장 큰 원을 찾은 다음 손바닥의 치수를 확인하여 손바닥의 중심을 결정합니다. 손바닥의 중앙을 기준으로 볼록 껍데기에서 손의 일부로 보이지 않는 모든 점을 제거합니다. 또한, 근처의 볼록 껍데기 점들이 제거되어 손가락의 수가 늘어남에 따라 정확히 그 많은 점들만 남게 됩니다.

Camera input frame is saved to a numpy array. A mask is generated based on background model and applied on the frame. This removes background from the captured frame. Now the frame containing only the foreground is converted to HSV color space, followed by histogram comparison (generating back projection). This leaves us with the detected hand. Morphology and smoothening is applied to get a proper hand shape out of the frame. A threshold converts this into a binary image.
손가락과 손바닥 치수의 위치를 이용하여, 우리는 손을 모델링합니다.

Next, we find contours of the binary image obtained, look for the largest contour and find its convex hull.
그런 다음 모델을 제스처에 정의된 제스처 사전과 비교합니다.API.py에서 제스처의 존재를 확인합니다.

Using points from the largest contour we determine center of the palm by finding the largest circle inscribed inside the contour and then the dimension of palm. Using the center of palm as reference, we eliminate all points from the convex hull which do not seem to be part of hand. Also, nearby convex hull points are eliminated so that we are left with exactly only those many points as the number of fingers stretched out.
스크린샷에 대한 전체 설명은 /docs/Documentation.pdf에서 제공됩니다.

Using the positions of fingers and palm dimensions, we model our hand.

Then we compare the model with a dictionary of Gestures defined in GestureAPI.py to determine presence of gestures.

**Full explanation with screenshots is provided in /docs/Documentation.pdf**

For any queries, contact: mahaveer.verma1@gmail.com
문의 사항은 mahaveer.verma1@gmail.comkr로 문의하십시오.
