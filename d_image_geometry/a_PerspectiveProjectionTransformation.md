# Perspective Projection Transformation) 원근 투영 변환
![image](https://user-images.githubusercontent.com/69780812/146714243-87bd4104-10d8-4a10-a54e-c7eb71c0062a.png)
- 투영 변환은 3차원 공간에 있는 점을 이미지 평면에 투영시키는 변환이다.
- 모델링하는 방법에는 크게 2가지 있다.
  - 1. projection reference point(투영 기준점)을 좌표계의 원점으로 잡고 이미지 평면을 전방 Zc = d에 둔다.
  - 2. 투영시킬 이미지 평면을 좌표계 원점에 위치시키고 투영 기준점을 Zc = -d에 잡는다.

# 1 번 방식
![image](https://user-images.githubusercontent.com/69780812/146714212-84460eb7-f050-4788-aedb-cf72adf16b0b.png)
- 3차원 상 점 P를 p'으로 투영시키는 변환 행렬은 위와 같이 주어진다.
- Zc = d인 경우 (Xc, Yc, Zc, 1)은 (Xc, Yc, Zc/d) = (d\*Xc/Zc, d*Yc/Zc, 1)로 투영된다.
  - s : homogeneous 좌표 표현의 sclae Factor (P의 depth에 해당)

# 2 번 방식
![image](https://user-images.githubusercontent.com/69780812/146714780-2dd8c688-b4e8-4d7e-ae4a-64481d460db4.png)
- (Xc, Yc, Zc, 1)은 (Xc, Yc, 1+Zc/d) = (d*Xc/(Zc+d), d\*Yc/(Zc_d), 1)로 투영된다.
---
![image](https://user-images.githubusercontent.com/69780812/146714873-42ec2f7b-31fc-4322-90ba-191738dca9a2.png)
- 1번 방식을 기준으로 Zc = d로 투영변환은 위와 같이 표현할 수 있다.

# Image 투영 model
![image](https://user-images.githubusercontent.com/69780812/146714938-4296c213-8e72-4be6-8f88-80c54d516655.png)
- 월드 좌표계 (X, Y, Z)를 이미지 평면(픽셀 좌표계) 상 점 (x, y)로 변환시키는 행렬을 H라 하면 관계식은 위와 같다.

![image](https://user-images.githubusercontent.com/69780812/146714989-fe09c807-3451-44ff-b4e5-cbb8e1653f62.png)

![image](https://user-images.githubusercontent.com/69780812/146715016-603e9016-1641-403f-bcfd-726967648a04.png)
- H는 3x4 행렬로 위와 같이 분해하여 표현할 수 있다.

- \[R|t] : 월드 좌표계를 카메라 좌표계로 바꾸는 rigid 변환 행렬
- Tpers(1) : 카메라 좌표계 상 3D 좌표를 정ㄱ 이미지 평면에 투영시키는 projection 행렬
- K : 카메라 내부 파라미터 행렬로 정규 이미지 좌표를 픽셀 좌표로 바꿔준다.
- Tpers(1)은 d=1 즉, Zc=1인 평면으로 투영변환을 말한다.
  - normalized image plane으로 투영

![image](https://user-images.githubusercontent.com/69780812/146715214-debb177a-1dfa-487f-93e3-fa13c71bf3c7.png)
- 투영변환 Tpers(1)과 rigid 변환 \[R|t]를 하나로 합치면 좀 더 간단한 표현식이 된다.
- K : 카메라 내부 파라미터 행렬
- 뒷 부분은 \[R|t] : extrinsic parameter를 나타낸다.
- s : homogeneous 좌표 표현의 scale factor로 점 (X, Y, Z)의 depth에 해당한다.