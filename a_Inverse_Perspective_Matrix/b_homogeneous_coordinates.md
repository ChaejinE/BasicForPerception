# What is Homogeneous Coordinates ?
- Homogeneous Space라고도 하는 동차 좌표계는 무엇을 의미하는가 ?
- **"N차원 사영 공간을 N+1개의 좌표로 나타내는 좌표계"**
  - 위 정의로 단순히 숫자 3을 대입하면 3차원 공간을 4개의 좌표로 나타낸다고 볼 수 있다.
  - 간단히 (x, y)를 (x, y, 1)로 표현하는 것이다.
- 3차원 사영 공간을 4개의 좌표로 나타내보자. (x, y, z, w)
  - w : 0 이라면 선(vector), 1 이라면 점(point)를 의미한다.
- homogeneous coordinates 에서 **(1, 2, 2, 0)은 (1, 2, 2)의 vector를 의미**하고, **(1, 2, 2, 1)은 (1, 2, 2)의 점(Point)를 의미**하는 것이다.
- w는 기하학적으로 **원금감을 조절하는 역할**을 하게 된다고 한다.
  - w = 1 이면 아무런 크기의 변화가 없게된다.
- Homogeneous coordinate에서 scale은 무시되고 (x, y)에 대한 homogeneous 좌표 표현은 무한히 많이 존재하게 된다.
  - (x, y, z)를 (x, y, z, 1) or (wx, wy, wz, w)로 표현
- (1, 2, 3)의 homogeneous coordinate 표현 : (1w, 2w, 3w, w) = (1, 2, 3, 1) = (2, 4, 6, 2) 전부 3차원의 (1, 2, 3) 좌표와 동치인 것이다.
- 역으로 homogeneous 좌표에서 원래 좌표를 구하려면 끝자리가 1이 되도록 scale을 바꾼 후 1을 때내면 된다.
  - (x, y, w)는 (x/w, y/w, 1)과 같으며 실제 2D 좌표는 (x/w, y/w)이 된다.

# Why use it ?
- 3차원을 나타내기 위해 3개의 element만 사용했다고 하면, (x, y, z)가 vector인지 point인지 알 수 없다.
  - Homogeneous Coordniates로 나타내서 w를 통해 이를 표현할 수 있게 되는 것이다.
- Homogeneous coordinate이 활용되는 곳은 3D Vision 쪽이다.
  - homogeneous 좌표계를 사용하면 Affine 변환, Perspective 변환을 하나의 Single Matrix(단일 행렬)로 표현할 수 있기 때문이다.
  - 동차 좌표계는 수학적, 물리적 의미가 확실하나 현재는 계산 편의를 위해 사용하는 것이라고 이해해도 좋다.

![image](https://user-images.githubusercontent.com/69780812/146290365-ec8d756f-0651-4532-a819-cf8ecc2f5f69.png)
![image](https://user-images.githubusercontent.com/69780812/146290380-052b8129-6fab-42a2-bcc1-586dba886f69.png)
![image](https://user-images.githubusercontent.com/69780812/146290395-386a06ec-a3fc-4b1c-95c9-bd41bca54581.png)
![image](https://user-images.githubusercontent.com/69780812/146290405-2d6b1d8b-2217-41da-8ff3-4058e0583b91.png)
![image](https://user-images.githubusercontent.com/69780812/146290412-1e8df817-be79-4846-9db4-e1299f517d24.png)
- 추가적으로 vector, point의 이동 및 회전 등을 matrix 곱으로 나타낼 수 있다는 장점이 있다.

## Matrix 곱셈으로는 모든 Transformation을 표현할 수 없다.
- Translation : 보통 vector의 덧셈으로 표현
- Rotation Transformation처럼 Matrix만으로 표현할 수 없는가 ?

![image](https://user-images.githubusercontent.com/69780812/146291219-707122c3-f0fe-4476-9728-c7850c2b1451.png)
- Affine Matrix (Transformation + Translation)은 위와 같이 표현할 수 있겠다.
- Translation을 하나의 Matrix로 표현하지 못해 Vector T로의 Vector 덧셈으로 표현된다.

![image](https://user-images.githubusercontent.com/69780812/146291286-9f09e78a-aac5-4781-98df-05d0acd177b9.png)
- Homogeneous Coordinate를 사용하면 Translation을 위한 Vector 덧셈을 위와 같이 하나의 Matrix 곱셈으로 표현할 수 있게 된다.
- 즉, Homogeneous Coordinate를 사용하면 모든 Transformation을 하나의 Matrix 곱셈으로 표현할 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146291389-a578c98f-c384-4523-8221-26e8748eab02.png)
- Affine Matrix를 Homogeneous Coordinate로 표현하면 위와 같다.

## W의 용도
![image](https://user-images.githubusercontent.com/69780812/146291524-fff146dc-c61b-4e65-9213-2cbd577df46e.png)
- w = 0이면 Translation을 하지 않는 용도다.
- 위 그림에서는 (1,2,3,0) vector A에 Translate 하는 Matrix T를 곱하는 것이다.
- w가 0이므로 (a,b,c)를 이동하는 Translate Matrix를 무시하게 되는 것이다.

![image](https://user-images.githubusercontent.com/69780812/146291709-ff12f852-6781-4b7d-8f8d-9b99e4bfcc33.png)
- w = 1이면 Translate를 한다는 것이다.
- (1, 2, 3, 1) vector B에 Translate Matrix T를 곱해본 것이다.
- w가 1이므로 1 x (a,b,c) 만큼 Translate 한다.
- w가 1이면 같은 비율을 유지하는 것을 확인할 수 있다. 그래서 주로 w를 1로 사용한다.
  - **position** : 주로 w=1을 사용
  - w를 크게 바꾸면 이동시키는 영향을 크게 주는 것이다.

![image](https://user-images.githubusercontent.com/69780812/146291898-c609003a-dd30-46ea-a77f-adb68c927c22.png)
- w = z이면 원근감을 적용하는 용도다.
  - Homogeneous Coordinate 사용 시 원금감을 표현하기 쉽다.
- 위 그림은 Pure Perspective Project에 대한 그림이다.
- Matrix M의 3번째 vector의 W요소는 1이다.
  - 3번 째 Vector의 w 요소 값을 1로 설정하면 곱해주는 Vector w 요소를 z로 만들어준다.
  - 그래서 Vector P에 Matrix M을 곱해주면 원래 0이었던 P의 w요소가 z가 되는 것이다.
  - MP 처럼 w 요소가 1이 아닐 때 **Clip Space**에 있다고 한다.

![image](https://user-images.githubusercontent.com/69780812/146292499-9424bbf0-e1d4-48db-bb4d-4a7cdf909112.png)
- Clip Space에 있는 MP를 흔히 사용하는 평면인 w=1인 곳으로 가져와서 해석해보자.
- z가 1보다 크면 x, y가 나눠져서 z가 클 수록 값이 더 작아진다는 사실을 알 수 있다.
  - w 요소값을 조정해서 원근감을 표현할 수 있게되는 것이다.

# Homogeneous 좌표 - Projection 과 무슨관계가 있는가 ?
- p'=(u, v)라는 정규 이미지 평면(normalized image plane)상의 한 점에 대해 생각해 보자.
- p'=(u, v)에 대한 homogeneous 좌표 표현은 (u, v, 1)이다. 잘 살펴보면 p'을 카메라 좌표로 봤을 때 3D 좌표도 (u, v, 1)이다.
- 카메라 좌표계 입장에서 보면 투영선 상에 있는 점들은 3D 좌표는 일반적으로 w(u, v, 1) = (wu, wv, w)이 된다.
  - (u, v)의 일반적인 homogeneous coordinate 표현과 정확히 일치한다.
- 위의 관점으로 보면 homogeneous 좌표 (x, y, z)에서 (x/z, y/z)를 구하는 것은 projection, 반대로 (u, v)를 homogeneous 좌표 (wu, wv, w)로 표현하는 것은 inverse projection 과정으로 볼 수 있다.
- Homogeneous 좌표 표현의 다른 장점은 무한대의 점을 유한 좌표로 표현할 수 있다는 것이다.
  - (u, v) 방향으로 무한대의 점은 homogeneous 좌표로 (u, v, 0)으로 표현된다.

# Reference
- 1. https://artiiicy.tistory.com/54
- 2. https://coding-groot.tistory.com/89