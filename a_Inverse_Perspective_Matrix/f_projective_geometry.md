# 사형 기하학
- Projective transformations에 대해 불변인 기하학적 특성을 연구하는 것
- 사영 기하학은 projection을 다루는 기하학이다. homogeneous(Projective) 좌표계를 사용한다.
- 다양한 차원에서 정의돌 수 있으며 1차원 사영기하학은 2차원 평면에서 선으로의 투영관계를, 2차원 사영 기하학은 3D 공간에서 평면으로 투영을, 3차원 사영 기하학은 4차원 공간에서 3차원 공간으로 투영 관계를 설명하는 기하학이다.

# 2차원 사영 기하학
- 사영 기하학에서 길이(length), 각도(angle), 평행성(parallelism)이 보존되지 않는다.
- 유클리디언 기하학에서 알고 있는 사실은 평행한 두 선은 결코 만나지 않는다는 것이다.
- 사영 기하학에서는 평행한 두 선의 교점을 구할 수 있다.
  - 이미지의 vanishing point가 바로 그 교점이다.
- 사영 기하학에서 보존되는 것은 type이다.
  - 직선은 직선으로, 곡선은 곡선으로 투영되는 것이다.

# Tip
- 직선의 방정식 ax + by + c = 0을 homogeneous 형태로 변환하면 ax + by + cw = 0이 된다. (x=x/w, y=y/w로 치환)
- ax + by + cw = 0 은 직선 ax + by + c = 0 상의 점으로 투영되는 homogeneous 좌표 (x, y, w)들이 만족해야하는 식을 나타낸다. 즉, ax + by + c = 0에 대응 되는 homogeneous 좌표계 상에서의 방정식이다.
- ax + by + cw = 0은 homogeneous 좌표계 상에서 평면의 방정식이지만 결과적으로 직선으로 projection되기 때문에 직선의 방정식이라 치는 것이다.
- 직선의 방정식을 u^T*p = 0 과 같은 형태로 표현하면 여러 해석이 가능해진다.
- 두 직선 u1, u2의 교점은 p = u1xu2가 된다. (cross product)
  - u1^T*(u1xu2) = 0, u2^T*(u1xu2) = 0 이기 때문에 cross product
- a1\*x + b1\*y + c1\*w = 0 과 a2\*x + b2\*y + c2\*w = 0 의 교점은 u1xu2 = (b1c2-b2c1, a2c1-a1c2, a1b2-a2b1)이 된다.
  - 따라서 유클리디언 직선에서 교점은 (b1c2-b2c1)/(a1b2-a2b1), (a2c1-a1c2)/(a1b2-a2b1)) 이라는 것을 알 수 있다.
- 즉, **homogeneous 표현을 이용하면 두 직선의 교점 및 두 점을 지나는 직선의 방정식을 일반적으로 구할 수 있게된다.**
- 직선 u를 변수로 두고, 점 p를 상수로 두면 u^T*p=0은 점 p를 지나는 모든 가능한 직선에 대한 식이 된다.

# Reference
- https://darkpgmr.tistory.com/78?category=460965