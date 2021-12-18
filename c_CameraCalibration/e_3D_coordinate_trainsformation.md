# 월드 좌표계(3D) - 카메라 좌표계 (2D)
- 월드 좌표계에서 점 (X, Y, Z)로부터 카메라 좌표계에서 봤을 때 좌표 (Xc, Yc, Zc)를 구하는게 목적이다.

![image](https://user-images.githubusercontent.com/69780812/146498378-f163e0fb-2ef6-4173-9df3-cd382667161d.png)
- 월드 좌표계 : 위쪽이 Z, 지면 X-Y
- 카메라 좌표계 : 광학축이 Zc, 오른쪽 Xc, 아래쪽 Yc
- 월드 좌표계 내에서 카메라의 위치 및 방향을 다음과 같이 정의해보자.
  - 카메라 위치 : 월드 좌표계 내에서 카메라 좌표축 원점 위치 (X1, Y1, Z1)
  - pan : 카메라 좌우 회전각, 광학축이 **월드 좌표계 Y축과 평행 시 0도, 왼쪽이 +, 오른쪽 -**
  - tilt : 카메라 상하 회전각, 광학축이 **월드 좌표계 Y축과 평행할 때 0도, 위쪽이 +, 아래쪽 -**
  - Zc가 Y축 방향일 때 pan, tilit가 0이고 카메라를 위로 들면 tilt 증가, 왼쪽으로 돌리면 pan 증가이다.
- pan angle:p (rad), tilt angle:t (rad) 일 때 임의의 월드 좌표 (X, Y, Z)를 카메라 좌표 상 (Xc, Yc, Zc)로 변환하는 관계식을 구해보자.

# 1. 회전변환을 조합하는 방법
![image](https://user-images.githubusercontent.com/69780812/146498890-863a7954-33d2-4fb3-9329-d7ba71fbdf08.png)
- R : 월드 좌표축을 카메라 좌표축과 방향이 일치되도록 하는 회전 변환행렬 을 구하는 식이다.

![image](https://user-images.githubusercontent.com/69780812/146499140-eada8f1e-465b-48cf-8b20-369772b1aacd.png)
- 따라서 월드 좌표를 카메라 좌표로 변환시키는 변환 식은 위와 같이 구해진다.
- 좌표축 변환은 일반적인 변환 과정을 역으로 적용함에 주의
- R^-1은 R(T) 이므로 이를 구하면 된다.

![image](https://user-images.githubusercontent.com/69780812/146512575-0b122a3d-2088-4d8e-ac84-44ca969008e5.png)
- 즉 이전의 식은 위와같이 될 수 있다.
- R은 월드 좌표를 카메라 좌표로 변환시키는 행렬이 아니다. **좌표축을 변환시키는 행렬**이다. 즉, R은 월드좌표축 -> 카메라 좌표축 변환행렬인 것에 주의하자.

# 2. 변환행렬을 직접 구하는 방법
![image](https://user-images.githubusercontent.com/69780812/146631501-b03471cc-84d7-42ac-8a39-8850e8af50f4.png)
- 어떤 선형변환 행렬 T가 있을 때, 각각의 좌표축 단위벡터들이 변환 T에 의해 어디로 가는지만 알면된다.
- 만일 T에 의해 X축 단위 벡터 (1, 0, 0)이 (a1, a2, a3)로 가고, Y축 단위 벡터 (0, 1, 0)이 (b1, b2, b3), Z축 단위 벡터 (0, 0, 1)이 (c1, c2, c3)가 된다면 변환행렬은 위와 같다.

![image](https://user-images.githubusercontent.com/69780812/146631547-8095b6e7-f72e-48fe-8ae3-0fab52eb883e.png)

![image](https://user-images.githubusercontent.com/69780812/146631561-e5cc1264-3ad9-4f28-b9e7-9c3a2a8bd8c6.png)

![image](https://user-images.githubusercontent.com/69780812/146631570-c30e947f-4fd1-43c1-82fe-790439845013.png)

- 첫번째 사진을 참조하여 단위 벡터가 어디로 이동해야하는지 구해보면 두번째 사진과 같다.
- 따라서 변환행렬 R은 마지막 사진과 같이 구해진다.
- 이전의 방법과 동일한 결과가 나옴을 확인할 수 있다.
- 나머지 과정은 방법1과 동일하다.

# Reference
- https://darkpgmr.tistory.com/84