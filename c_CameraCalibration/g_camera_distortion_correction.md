# Overview
- 카메라 캘리브레이션 및 왜곡 보정은 영상처리 분야에서 거의 필수적으로 필요한 내용이다.
- 전반적인 카메라 시스템에 대한 이해와 많은 시간이 필요하다.
  - 우리나라는 진입장벽이 높은 편이다.

![image](https://user-images.githubusercontent.com/69780812/146633705-b2f0652f-92a3-4ce7-806b-68523562be15.png)
- 카메라에 FOV가 넓은 광각렌즈나 초광각 렌즈를 사용하면 넓은 범위를 볼 수 있으나 상대적으로 영상왜곡이 심해지는 문제가 있다.
- 영상 왜곡은 시각적문제 외에도 영상분석을 통한 정확한 수치 계산 필요 시 특히 문제가 된다.
  - 영상에서 검출한 물체의 실제 위치를 알기위해 영상좌표를 물리적인 좌표로 변환하면 영상 왜곡 정도에 따라 심각한 오차가 발생한다.

# 1. 렌즈계 왜곡 종류
- radial distortion(방사왜곡), tangential distortion(접선왜곡)이있다.

![image](https://user-images.githubusercontent.com/69780812/146633743-04cb0ea2-51a9-4dd1-ad7d-54677fc4b92a.png)
- 위는 radial distortion에 대한 그림이다.
- 볼록 렌즈의 굴절률에 의한 것으로 위와같이 영상의 왜곡 정도가 중심에서 거리에 의해 결정되는 왜곡이다.

![image](https://user-images.githubusercontent.com/69780812/146633935-c351a486-bf38-454e-94ba-6665ddafb3ef.png)
- 접선왜곡은 카메라 제조 과정에서 카메라 렌즈와 이미지 센서의 수평이 맞지 않거나 또는 렌즈 자체의 centering이 맞지 않아 발생하는 왜곡이다.
- 타원형 형태로 왜곡 분포가 달라진다.
- [참고](https://carstart.tistory.com/181)

# 2. 렌즈계 왜곡의 수학적 모델
- 렌즈 왜곡에 대한 수학적 모델은 카메라 내부 파라미터의 영향이 제거된 normalized image plane에서 정의된다.

![image](https://user-images.githubusercontent.com/69780812/146634018-c43da056-0309-472a-aa60-51d294d8f0a3.png)
- 렌즈계 왜곡이 없다고 할 경우 3차원 공간상 한점 (Xc, Yc, Zc)는 central projection(pinhole projection)에 의해 normalized image plane 상 한점 (x_n_u, y_n_u)로 투영된다. (n:normalized, u:undistorted)

![image](https://user-images.githubusercontent.com/69780812/146634062-ef4fd70b-6edf-4399-8333-8d0173d7db2a.png)
- 그러나 실제로는 x_n_u, y_n_u는 렌즈계의 비선형성에 의해 주로 radial distortion이 일어난다.
- (x_n_d, y_n_d)를 렌즈계의 왜곡이 반영된 normalized 좌표라면 렌즈계 왜곡 모델은 위와 같다.
- 단, 위 수식에서 우변의 첫째항은 radial distortion, 두 번째 항은 tagential distortion을 나타낸다.
  - k1, k2, k3 : radial distortion coefficient
  - p1, p2 : tangential distortion coefficient

![image](https://user-images.githubusercontent.com/69780812/146634090-d355bd3c-999f-46be-9a38-75eb267fcb3f.png)
- r_u는 왜곡이 없을 때의 중심(principal point)까지의 
거리이다. (반지름)

![image](https://user-images.githubusercontent.com/69780812/146634167-85439756-aeed-4d6b-88f2-50d882a25531.png)

![image](https://user-images.githubusercontent.com/69780812/146634190-d3c99036-f68c-4dd2-9679-b151a0d66691.png)
- x_n_d, y_n_d는 normalized image plane에서의 좌표이며 실제 영상 픽셀 좌표 x_p_d, y_p_d는 카메라 내부 파라미터를 반영하여 위와 같이 구해진다.
- fx, fy : focal length
- cx, cy : 렌즈 중심 영상 좌표 (principal point)
- skew_c : 비대칭 계수

# 3. 영상 왜곡 보정
- 왜곡된 영상을 보정하기 위해서는 먼저 카메라 캘리브레이션을 통해 카메라 내부 파라미터를 구해야한다.
- 왜곡된 영상을 Id, 보정된 영상을 Iu라하자.
  - Iu의 각 픽셀값을 해당 픽셀 좌표를 왜곡시켰을 때의 Id의 대응되는 픽셀 값으로 채우는 것이다.

![image](https://user-images.githubusercontent.com/69780812/146634253-70bd99c0-1cc2-4103-81b5-8149399c1876.png)

![image](https://user-images.githubusercontent.com/69780812/146634257-178e4f3f-60d3-458f-8bcd-2d794f4d623b.png)
- 영상 Iu의 한점을 (xp_u, yp_u)라하면, 이것을 카메라 파라미터를 역으로 적용해 normalized 좌표 (xn_u, yn_u)로 변환한다.

![image](https://user-images.githubusercontent.com/69780812/146634298-b67e75be-fb12-4048-94a1-dc9c0793236f.png)
- 다음으로 중심까지거리 ru = xn_u^2 + yn_u^2를 구하고 왜곡모델을 적용해 왜곡된 xn_d, yn_d를 구한다.

![image](https://user-images.githubusercontent.com/69780812/146634330-1c3eeab4-b108-443f-924f-304304530590.png)
- 마지막으로 (xn_d, yn_d)를 다시 픽셀 좌표계로 변환하면 (xp_u, yp_u)의 왜곡된 영상에서의 좌표 (xp_d, yp_d)를 구할 수 있다.

# 4. 영상 좌표 왜곡 보정
- 실제 영상처리에서는 종종 보정된 영상을 구하는 것보다 보정된 영상 좌표를 구하는 것이 훨씬 중요하다.
  - 때로는 영상 전체를 보정한 후 영상처리 알고리즘을 적용하는 것보다는 원래 왜곡된 영상에서 처리한 후 그 결과만 보정하는 것이 효과적일 수 있기 때문이다.
- 왜곡된 영상좌표로 부터 왜곡 보정된 영상좌표를 구하는 것은 closed-form solution이 없어 매우 어려운 문제이므로 보통 근사적으로 해를 구한다.

![image](https://user-images.githubusercontent.com/69780812/146634347-6decc1cb-acdf-4d95-95e6-ef16dc7a4a24.png)
- 왜곡된 영상좌표 p_d로부터 왜곡 보정된 좌표 p_u를 구하는 한 방법은 p_u = p_d로 가정하고 위 식을 이용해 p_u를 왜곡시켜 보는 것이다.
- 이렇게 구한 점이 실제 p_d와 얼마나 오차가 나는지 계산하고 그 오차를 p_u에 역으로 반영 시킨다.
  - p_u를 왜곡 시킨 점이 p_d보다 10만큼 크다면 p_u를 10만큼 감소시킨다.
  - 이러한 과정을 오차가 임계값 이하가 될 때까지 반복하면 된다.