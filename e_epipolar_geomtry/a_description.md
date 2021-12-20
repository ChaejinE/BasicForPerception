# Epipolar geometry
- Stereo Vision, 2-View 비전에서의 기하라고 생각하면 된다.

![image](https://user-images.githubusercontent.com/69780812/146715592-e3cd17d9-8999-4b2e-ab40-1c66d18790a4.png)
- 동일한 사물 또는 장면에 대한 영상을 서로 다른 두 지점에서 획득 했을 때, 영상 A와 B의 매칭쌍들 사이 기하학적 관계를 다루는 것이다.

# Basic
![image](https://user-images.githubusercontent.com/69780812/146715592-e3cd17d9-8999-4b2e-ab40-1c66d18790a4.png)
- 3차원 공간상 한 점 P가 영상 A에서는 p에 투영되고 B에서는 p'에 투영된다.
- 두 카메라 원점을 이는 선과 이미지 평면이 만나는 점을 e, e' : epipole이라고 부른다.
- 투영점과 epipole을 잇는 직선 l, l' : epiline이라 부른다. (epipolar line)
- 두 카메라 위치 사이 기하학적 관계 [R|t]를 알고 있고, 영상 A에서 영상 좌표 p를 알고 있을 때, 영상 B에서 대응되는 점 p'의 좌표를 구하는 문제를 생각해보자.
  - P까지의 depth 정보를 ㅁ른다면 p에서 투영되기전의 3차원 좌표 P로 복원할 수 없다.
  - 따라서 P가 영상 B에 표현된 좌표 p' 또한 유일하게 결정할 수 없다. 하지만 P는 A카메라의 원점과 p를 잇는 직선상에 존재하므로 이 직선을 영상 B에 투영시키면 점 p'이 투영된 직선 위에 있음은 알 수 있게 된다.
    - 이때 투영된 직선 : l', epiline
- A 영상 좌표 p로부터 대응되는 B의 대응 좌표 p'을 유일하게 결정할 수는 없지만 p'이 지나는 직선인 epiline l은 유일하게 결정할 수 있다는 것이 결론이다.
- Fundamental Matrix, Essential Matrix : 한 영상좌표로 부터 다른 영상에서 대응되는 epiline을 계산해주는 행렬
  - 서로 다른 시점에서 찍은 영상좌표들 사이에는 Fundamental Matrix, Essential Matrix를 매개로 하는 어떤 변환 관계가 성립하는데 이를 통해 기하학적 문제를 풀게 된다.

# Essential Matrix
![image](https://user-images.githubusercontent.com/69780812/146715592-e3cd17d9-8999-4b2e-ab40-1c66d18790a4.png)

![image](https://user-images.githubusercontent.com/69780812/146716254-3d742107-a25e-40a0-a591-41ab39580e0f.png)
- **한 점 P가 영상 A에서 p에 투영, B에서는 p'에 투영됐다고 한다면 두 영상 좌표 p, p' 사이 위의 관계를 만족하는 행렬이 항상 존재한다**는 것이 epipolar geometry의 핵심이다.
- 임의의 두 지점에서 찍은 영상의 매칭점들은 항상 식(1)을 통해 관계지을 수 있다.
  - 식 (1)을 epipolar constraint 라한다.
  - E : **Essential Matrix**

## Essential Matrix가 항상 존재하는 이유
![image](https://user-images.githubusercontent.com/69780812/146716499-a72b1c84-62ed-45a3-880c-f57c99399780.png)
- 임의의 두 카메라 좌표축 사이 관계는 회전, 평행이동에 의해 관계 지을 수 있어 3x3행렬을 R, 3x1 평행이독 벡터를 t라하면 외부 공간 상 한점을 두 카메라 좌표계에서 봤을 때 관계를 위와같이 잡을 수 있다.
  - P : 외부 공간상 점을 A 카메라 좌표계에서 봤을 때, 3차원 좌표
  - P' : B 카메라 좌표계에서 봤을 때 3차원 좌표

![image](https://user-images.githubusercontent.com/69780812/146716605-c87680f3-d215-4432-9646-07e9820ce4b8.png)
- 이 때, essential matrix E를 위오 ㅏ같이 잡으면 

![image](https://user-images.githubusercontent.com/69780812/146716781-771a656d-94ee-45a6-acb4-43fe75975ace.png)
- 식 (5)가 만족됨을 알 수 있다.
  - \[t]x : 벡터 t와 벡터 외적을 의미한다.
  - 먼저 R로 회전을 시킨 후 t와 이적을 시키는 일련의 변환을 의미한다.
  - Ep = \[t]xRp = tx(Rp)

![image](https://user-images.githubusercontent.com/69780812/146716930-8a2e0bb5-262c-406a-b944-9bf88d0f2721.png)
- 실제 식(5)의 좌변에 E=\[t]xR을 대입하면 위와 같이 항상 0이 나옴을 알 수 있다

![image](https://user-images.githubusercontent.com/69780812/146717004-7792dd4c-c253-4303-a4f0-49500ab0bf09.png)
- 식(5)의 카메라 좌표를 정규 이미지 좌표로 바꾸면 p'TEp = 0이 성립함을 알 수 있다.

# Fundamental Matrix
- Essential Matrix는 정규화된 이미지 평면에서의 매칭 쌍들 사이 기하학적 관계를 설명하는 행렬이다.
  - 즉 카메라 내부 파라미터 행렬인 K가 제거된 좌표계에서의 변환고나계이다.
- 반면, Fundamental Matrix는 **카메라 파라미터까지 포함한 두 이미지 실제 픽셀 좌표 사이의 기하학적 관계**다.

![image](https://user-images.githubusercontent.com/69780812/146717135-872108a0-9d83-4053-929a-0645d3f0ee20.png)
- 임의의 두 이미지 A, B에 대해 p_img, p_img' 사이에는 항상 위오 ㅏ같은 고나계를 만족하는 F가 존재하고 이러한 행렬을 fundamental Matrix라 한다.

![image](https://user-images.githubusercontent.com/69780812/146717225-917d7cdb-0b11-4f7d-a30f-68d3de0be3c7.png)
- A 카메라에 대한 내부 파라미터 행렬을 K, 이미지 B에 대한 카메라 행렬을 K'라하고, A, B 사이 essential matrix를 E라하면 Fundamental Matrix는 위와같이 주어진다.

![image](https://user-images.githubusercontent.com/69780812/146717334-89988344-cb66-46c9-a00c-43789ab534d1.png)
- 만일 A, B 동일 카메라로 촬영했다면 카메라 행렬이 동일하여 식(11), 식(12)는 위와같이 좀 더 단순화 된다.

![image](https://user-images.githubusercontent.com/69780812/146723972-3c311265-df6d-429d-8e0d-034cd81ee3ac.png)
- Computer Vision에서 이미지 픽셀좌표 p_img와 normalized 좌표 p 사이에는 camera matrix K에 대해 위아 같은 변환 관계를 가진다.

![image](https://user-images.githubusercontent.com/69780812/146724088-633eca1f-3432-4cff-a7a2-56782fc1f330.png)
- 따라서 이미지 A의 카메라 파라미터 행렬을 X, 이미지 B의 카메라 행렬을 K'이라 놓으면 위와 같은 관계가 성립한다.

![image](https://user-images.githubusercontent.com/69780812/146724201-3d76a6d4-6afb-4a1c-b8f9-867a6c2a3874.png)
- 식(17)을 식(1)에 대입하면 위와 같이 fundamental matrix가 구해진다.
  - 존재함을 알 수 있다.

## epipolar constraint
- 두 이미지 평면 사이 기하학적 관계에 따른 constraint이다.

![image](https://user-images.githubusercontent.com/69780812/146724329-e290da15-4992-4644-b3e2-6aeefa8f6513.png)
- 바로 이 식이 epipolar constraint를 나타낸다.

![image](https://user-images.githubusercontent.com/69780812/146724381-67f98bac-ad44-4e6a-bb4e-9bd74d1ae390.png)
- 두 이미지가 주어지고 대응되는 매칭쌍을 알고 있으면, 카메라 파라미터를 모른다면 fundamental matrix F를 직접구해야한다.
- F를 구하기 위해서는 최소 7쌍의 매칭점들을 필요로 한다.
- 단, 여기서 주의해야할 점은 F의 scale 까지는 결정할 수 없다는 것이다. (E도 마찬가지)
  - scale을 결정할 수 없다는 것은 위 그림 처럼 물체와 카메라가 존재하는 공간 전체를 확대하거나 축소해도 동일한 이미지를 얻기 때문에 이미지만 가직는 스케일을 알 수 없다는 것을 의미한다.
  - 가까이 있는 작은 물체를 찍거나 멀리 있는 큰 물체를 찍어도 같은 영상을 얻을 수 있음을 상기하자.
- 만일, 카메라 파라미터를 알고 있다면 Essential matrix E만 구하면 된다.
  - E를 구하기 위해 보통 5쌍의 매칭점을 필요로한다. 알고리즘에따라 8상이 필요한 경우도 있고 3, 2, 1쌍의 매칭점을 필요로하는 경우도있다.
    - E는 R, t로 구성되어 회전 변환 R이 3자유도, 스케일을 무시한 평행이동 t가 2자유도, 도합 5자유도여서 5ㅏㅇ의 매칭점을 필요로한다.
- Epipolar geometry에서 essential이 중요한 이유는 E를 알면 두 카메라 A, B 사이 또는 두 시점 사이의 회전, 평행이동 관계를 파악할 수 있기 때문이다.

## triangulation
- 삼각측량법이라 하는 것은 두 이미지 평면 사이의 기하학적 관계가 주어지고, (E or F) 두 이미지 평면상의 매칭쌍 p, p'이 주어지면 이로 부터 원래의 3D 공간좌표 P를 결정할 수 있다는 것을 말한다.
- 스테렝 비전에서 depth를 구할 때 하는 일이다.

# Reference
- https://darkpgmr.tistory.com/83?category=460965