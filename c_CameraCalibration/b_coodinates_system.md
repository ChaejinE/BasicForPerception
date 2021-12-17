# Overview - Coordinate System (좌표계)
- 영상 geometry에서는 크게 4가지 좌표계가 존재한다.
  - 월드 좌표계, 카메라 좌표계, 정규 좌표계, 픽셀 좌표계

![image](https://user-images.githubusercontent.com/69780812/146345519-7683a0bf-e4d7-4b1c-b353-2256157e69f0.png)
- 월드 좌표계, 카메라 좌표계 : 3D 좌표계
- 정규 좌표계, 픽셀 좌표계 : 2D 좌표계
- 이 4가지 좌표계를 명확히 구분하고 이해하는 것이 카메라 geometry를 이해하는 데 있어서 매우 중요하다.

# 1. World Coordinate System
- Object의 위치를 표현할 때 기준으로 삼는 좌표계
- 문제에 따라서 임의로 잡아서 사용할 수 있는 좌표계이다.
- 좌표계는 **일종의 약속:protocol**이기 때문에 (3, 1, -10)이라했을 때, **이 점이 어떤 위치인지 그 문제 내에서 만큼은 유일하게 결정될 수 있으면 되는 것**이 중요하다.

![image](https://user-images.githubusercontent.com/69780812/146483148-37ccae22-564b-40e0-bfda-e9d876cdfb8a.png)
- 설명하는 동안 위의 대문자 표기가 월드 좌표계다.

# 2. Camera Coordinate System
![image](https://user-images.githubusercontent.com/69780812/146483189-b2187b9a-68b8-4447-9ea2-5c0dc122fc72.png)
- World coordinate system이 우리가 있는 공간 중 한 지점을 기준으로한 좌표계라면 카메라 좌표계는 **카메라를 기준**으로한 좌표계이다.
- **카메라의 정면 광학축 방향을 Z-axis, 카메라 아래쪽 방향을 Y-axis, 오른쪽 방향을 X-axis**로 잡는다.
- 월드 좌표계의 단위와 동일하게 하면된다.

![image](https://user-images.githubusercontent.com/69780812/146483478-003facd2-deb3-4625-9430-43aa92c95041.png)
- 카메라 좌표계를 기준으로 한 점의 좌표는 아랫첨자 c를 사용해 대문자로 표기

# 3. Pixel Image Coordinate System
- 보통 영상 좌표계로 불린다. (Image Coordinate System)
- 실제로 눈으로 보는 영상에 대한 좌표계이다.
- **left-top 모서리를 원점으로 오른쪽 방향 X-axis (+), 아래쪽 방향 Y-axis(+)**로한다.
- 픽셀 좌표계의 **x, y축에 의해 결정되는 평면을 이미지 평면, image plane**이라 부른다.
- 기하학적으로 볼 때, 3D 공간상의 한점 P=(X, Y, Z) 카메라의 초점을 지나서 이미지 평면 한점 p_img = (x, y)에 projection 된다.
  - **3D 점 P로부터 p_img는 유일하게 결정될 수 있으나 영상 픽셀 p_img로부터 P를 구하는 것은 부가적 정보없이는 불가능**하다.

![image](https://user-images.githubusercontent.com/69780812/146483932-27eba66e-6677-4fc5-af23-e6161a9a0b83.png)
- 픽셀 좌표계의 **단위는 픽셀**이다.

# 4. Normalized Image Coordinate System : 정규 좌표계
- 편의상 도입된 가상의 좌표계
- 카메라의 내부 파라미터:intrinsic parameter 영향을 제거한 이미지 좌표계다.
- 좌표계의 단위를 없앤 좌표계이다.
  - **카메라 초점과 거리가 1**인 가상의 이미지 평면을 정의하는 좌표계다.
- 정규 좌표계의 원점은 정규 이미지 평면의 중점이다. (광학축 Zc와의 교점)
  - **픽셀 좌표계와 원점 위치가 다름에 주의**한다.

![image](https://user-images.githubusercontent.com/69780812/146484353-36c05316-0492-44d0-95a8-18d78045d8ca.png)
- 정규 좌표계를 위와같이 표기한다.

![image](https://user-images.githubusercontent.com/69780812/146484393-2c447db7-494d-438c-b29f-bc7d1ac1b2e9.png)

![image](https://user-images.githubusercontent.com/69780812/146484427-a016bf50-35c4-46e8-a159-5a7cf5d2f101.png)
- 카메라 내부 파라미터를 알면 위와 같이 픽셀 좌표와 정규 좌표 사이 변환이 가능하다.
- fx, fy : focal length
- cx, cy : principal point (광학 축과 영상 평면이 만나는 픽셀 좌표)
- 3x3 Matrix : camera matrix

![image](https://user-images.githubusercontent.com/69780812/146484543-5b15d112-bf11-473d-a4fc-8ec80f820353.png)
- 이전 사진에 대한 식을 정리하면 위와 같다.

![image](https://user-images.githubusercontent.com/69780812/146484871-0d5ad1f0-643a-4e4b-ba7d-0ae79a4d3e54.png)
- 역으로 이미지 상 픽셀(x, y)에 대응하는 정규 좌표는 위와 같이 계산된다.

## 왜 정규 이미지 평면과 정규 좌표계를 도입한 것인가?
- 동일한 장면을 동일한 위치와 동일 각도에서 찍더라도 사용한 카메라에 따라서 or 카메라 setting에 따라서 서로 다른 영상을 얻게된다. 이러한 카메라간 차이는 어떤 일관된 기하학적인 해석을하는 데 있어 불필요한 요소이다.
- 이러한 요소를 제거한 정규화된 이미지 평면에서 공통된 기하학적 특성을 분석하고, 이론을 수립하는 것이 보다 더 효과적이기 때문이다.


# Reference
- https://darkpgmr.tistory.com/77