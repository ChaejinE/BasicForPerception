# 3D 변환
- 3D 변환은 회전과 평행이동만이 관심있는 변환이다. (rigid 변환)

# 1. 변환 행렬
![image](https://user-images.githubusercontent.com/69780812/146499824-71d20389-0401-4bc6-adab-f83f7ea1c209.png)
- 3차원 공간의 점 (X, Y, Z)를 X축, Y축, Z축 중심으로 rad 회전 시키는 행렬을 정의하면 위와 같다.

![image](https://user-images.githubusercontent.com/69780812/146499882-50b2a1b8-2584-4811-bf63-f022fb654b71.png)
- 회전 방향은 위와 같이 축에 대해 **반시계 방향**이다.
- 오른손 주먹을 말아쥐고 엄지를 들었을 때 엄지 방향이 회전축, 말아쥔 손가락 방향이 회전방향이다.

![image](https://user-images.githubusercontent.com/69780812/146499979-ab8ecdcc-12ce-4919-9136-15cd05394ecc.png)
- 3개의 기본 회전 변환을 조합하면 임의의 3D회전을 표현할 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146500025-c431be5a-3176-40e8-ac5a-736c113123be.png)
- 좌표축이 아닌 임의의 단위 벡터 u = (ux, uy, uz)를 회전축으로 한 회전변환 행렬은 위와 같다.
  - 단, ux^2 + uy^2 + uz^2 = 1

![image](https://user-images.githubusercontent.com/69780812/146500149-55560cfd-9666-4f3b-b297-3b507ee76b9a.png)
- 회전변환 R, 평행이동 t를 이용한 일반적인 3D 변환은 위와 같다.

![image](https://user-images.githubusercontent.com/69780812/146500185-8927014e-b812-4b2f-9b7d-1c27c5ad109e.png)
- 3D 변환에서 homogeneous 좌표를 사용하면 위와 같이 회전변환과 평행이동을 하나의 변환행렬로 선형변환 형태로 표현할 수 있다.
  - 어떤 행렬 R이 회전변환이 되기 위한 충분 조건 : R^T = R^-1, det(R) = 1

## 2. 변환관계
![image](https://user-images.githubusercontent.com/69780812/146500418-866dc94f-f142-499f-b080-0d0b782389de.png)
- 크기가 같은 임의의 두벡터 u, u'이 있을 때 u를 u'을 이동시키는 회전변환은 위와 가티 구할 수 있다.
- theta는 u, u' 사이 사잇각이며 벡터의 내적을 이용하면 손쉽게 구할 수 있다.
- 회전축은 u, u'에 의해 결정되는 평면에 수직인 벡터 즉, 외적을 이용하면 된다.

![image](https://user-images.githubusercontent.com/69780812/146500614-6060a983-1a77-4699-8ca4-81ff9204191f.png)
- 이렇게 구한 theta, 단위 벡터 v를 위의 식에 대입하면 원하는 회전 변환행렬을 구할 수 있다.

## 3. Rigid 변환
- 회전 뿐만 아니라 평행이동 까지 고려한 문제로 학대된다.

![image](https://user-images.githubusercontent.com/69780812/146500871-3633e680-9160-4e2c-8ff5-b71d708c800b.png)
- **3차원 공간**에서 어떤 물체의 **위치 및 방향을 유일하게 결정**하기 위해서는 **최소 3개의 점이 필요**하다.
  - 마찬가지로 **움직이는 물체의 위치관계**를 표현하기 위해서는 **3개의 매칭쌍이 필요**하다.
- 과정은 p1이 원점이 되도록 A를 평행이동 시킨 후 A'의 방향과 일치됟록 회전시켜 p1'까지 평행이동 시킨다.

![image](https://user-images.githubusercontent.com/69780812/146501184-8b43d3bf-6f30-4b68-a22c-73b07b52e235.png)
- 여기서 두 물체를 일치 시키기 위해선느 총 2번의 회전이 필요하다.
  - p1p2가 p1'p2'이 되도록 회전(R1) 시킨 후 p3, p3'이 일치되도록 한번 더 회전(R2) 시킨다.
  - R1은 회전변환 구하기 방법을 사용하면 된다. 문제는 R2다.
  - Reference한 작성자는 R1\*p1p2 & R1*p1'p3'에 의해 결정되는 평면에 수직인 법선 벡터를 구해 두 법선 벡터가 일치되도록 회전시켰다. 즉, R2는 (R1\*p1p2)x(R1\*p1p3)를 (R1\*p1p2)x(p1'p3')으로 회전시키는 행렬이다.

## 4. 좌표축 변환
- 월드 좌표계와 카메라 좌표계 사이 변환이 좌표축 변환이다.

![image](https://user-images.githubusercontent.com/69780812/146510722-813e3176-03c1-4846-b95a-2fc71f9752d9.png)
- 월드 좌표계 상에서 카메라 초점(카메라 좌표계 원점)의 좌표를 (Fx, Fy, Fz), 월드 좌표계의 좌표축을 카메라 좌표계 좌표축으로 회전 시키는 행렬을 R이라 하자.
- 월드 좌표계 X, Y, Z를 카메라 좌표계로 봤을 때 좌표 Xc, Yc, Zc는 위와 같이 구해진다.

![image](https://user-images.githubusercontent.com/69780812/146510840-14bee729-fcbc-441c-9c02-eb3c39b180c0.png)
- R(T)R = 1, R^-1=R(T) 가 성립하므로 위 처럼 쓸 수 있다.
- 카메라 좌표계 상 점을 월드 좌표계로 바꿀 때에도 이 식을 역으로 이용하면 된다.

# Reference 
- https://darkpgmr.tistory.com/81