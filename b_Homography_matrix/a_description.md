# Homography Matrix - Computer Vision 관점
- 동일한 물체에 대해 다른 위치에서 찍힌 두 이미지 사이 관계를 구하는 간단한 방법이다.
- Homography Matrix가 이 관계를 설명하는 수단이 된다.

![image](https://user-images.githubusercontent.com/69780812/146319673-551d961b-570c-413a-9a85-3da63926ad69.png)
- constraint : 두 이미지의 관계를 나타내기 위해서는 **H를 통해 Mapping될 pair point들이 모두 같은 plane**에 있어야한다.

## How to estimation
![image](https://user-images.githubusercontent.com/69780812/146320251-09f3778b-3d19-49bd-9d17-25a134de6ae2.png)
- 두 점이 pair를 이룬다고 가정해보자.
  - pair들은 colinear 하면 안된다.
  - 즉, 사용되는 3개의 점들이 선 하나 위에 있으면 안된다.

![image](https://user-images.githubusercontent.com/69780812/146320395-6af2b268-ceef-4ea0-9da0-0683505379da.png)
- Homography Matrix H에 의해서 하나의 pair에서 두개의 equation을 얻을 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146320459-12fef3b1-391f-4b44-9ea1-3adbd5e55e3a.png)
- 이 전의 equation을 Matrix로 나타내면 위와 같다.
- 총 9개의 parameter지만 Homogeneous Coordinate System에서는 Scale에 대해서는 상관하지 않아도 되므로 9개의 parameter중 8개만 estimation하면된다.
- 하나의 pair에서 2개의 equation을 얻을 수 있어 총 4개의 pair를 사용하면된다.
  - **no colinear pair**

![image](https://user-images.githubusercontent.com/69780812/146320618-a709b999-0c2d-4dfd-9d84-72a46384c98a.png)
- A와 h 행렬로 벡터를 나타내면 위와같은 objective function이 나오게되고 Least Square Method를 사용하면 답을 구할 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146332033-f647ca49-69e6-4bcb-80de-2426969af3dd.png)
- Homography matrix H를 추정하기 전 A matrix를 Normalize할 필요가 있다.
  - x_i * x'_i와 같은 곱셈 연산과 x_i 사이의 scale이 다르기 때문이다. 다른 Scale로 인해 eigen decomposition을 구할 때 unstable한 성질을 갖게되어 정학한 h를 추정하기 어렵다.
  - 따라서 **Isotropic Scaling Transform**을 해야한다. Points 중심을 Origin으로 Origin에서 각 Point의 평균 거리가 2의 제곱근이 되도록 Scaling한다. (Scale Transformation))

![image](https://user-images.githubusercontent.com/69780812/146332408-8edf5e22-5904-4c35-b02d-24e2229a4cd0.png)
- 따라서 위와 같은 최종적인 Homography Matrix H를 구할 수 있다.
- T는 x_i의 scale transformation matrix이다.

## Epipolar Geometry
![image](https://user-images.githubusercontent.com/69780812/146332838-3c4bb71b-51f0-497a-8395-0122beb8264e.png)
- 두 카메라가 하나의 물체를 서로 다른 위치에서 찍는다고 가정해보자.
  - 첫번째 카메라에서보는 이미지와 두번째 카메라에서 보는 이미지 사이에는 특정한 관계가 있다.
  - 정확히는 첫번째 카메라가 두번째 카메라를 보는 이미지 내에서의 point는 두번째 카메라에서 첫번째 카메라를 보는 이미지 내에서 line과 연관이 있다는 것이다.

![image](https://user-images.githubusercontent.com/69780812/146333080-5eb63fac-fcac-400d-8b12-199e8011183c.png)
- E : Essential Matrix
- x : camera의 view의 특정 물체가 projection되는 point
- l' : 이에 해당하는 두번째 카메라의 view의 line or 동일 물체가 카메라의 view에 projection되는 point candidates
  - candidates : 정확한 위치를 알 수 없기 때문에 이렇게 부른다.

![image](https://user-images.githubusercontent.com/69780812/146333308-87c9899e-2228-4f8e-a24b-9b1e9e2e6de0.png)
- 이전의 식은 위와 같은 특징을 갖는다.
- x' : 두번째카메라 view의 특정 물체가 projection되는 point
  - 이 point는 항상 point candidates 혹은 line l'에 있으므로 0이된다.

![image](https://user-images.githubusercontent.com/69780812/146333436-0e0c553c-3d24-4737-9691-4dee65f4cfe1.png)
- 이전의 개념을 확장시키면 위와같은 부수적 특징을 얻는다.
- l : 두번째 카메라 view의 특정 물체가 projection되는 point x'에 대응디는 첫번째 카메라 view의 point candidates or line
- e': 두번째 카메라 view에 첫번째 카메라가 projection 되는 point
- e : 첫번째 카메라 view에 두번째 카메라가 projection 되는 point
- line위에 점이 있다면 그 점가 line 사이 inner product이 0이된다는 점에서 쉽게 끌어낼 수 있는 관계다.

![image](https://user-images.githubusercontent.com/69780812/146333855-57c626ec-c0a0-4917-9e64-c6bb242ff78b.png)
- Camera의 Instrinsic parameter를 알고 있다면, Essential Matrix를 쓰지만, 사실 그렇지 않아 더 general한 개념은 **Fundamental Matrix**를 사용해야한다.
- K : camera instrinsic parameter matrix
- Fundamental Matrix 는 3x3 matrix로 총 9개 pram을 estimation 해야한다. 하지만 Homography와 마찬가지로 Homogeneous Coordinate System에서는 Scale에대한 부분은 무시가 되므로 총 8개의 parameter를 추정하면되고, 다음 행렬 식으로 하나의 pair에 대해 1개의 equation을 얻을 수 있게 된다.

![image](https://user-images.githubusercontent.com/69780812/146334093-368c0d87-ebaf-40f3-a957-803b6daa562f.png)
- 총 8개의 parameter를 추정해야하고, 하나의 pair에서 하나의 equation을 얻을 수 있어 총 8개의 point가 필요하다.

![image](https://user-images.githubusercontent.com/69780812/146334214-cd665698-1ae7-462c-85e2-ebbef6578235.png)
- Homography와 마찬가지로 다른 sclae로 인한 eigen decomposition의 unstability 해결을 위해 scale transformation이 필요하다.

![image](https://user-images.githubusercontent.com/69780812/146334305-89c70696-4b44-4734-90ee-67fc2d43af21.png)
- Fundamental matrix와 Essential matrix는 full rank matrix가 아닌 rank가 2인 matrix다.
  - 반면 이전의 식을 푼 결과로 얻은 f는 full rank = 3이므로 rank의 수를 위와 같은 방법으로 줄인다.

# Homograhy Matrix - 개발관점
![image](https://user-images.githubusercontent.com/69780812/146317599-1b9d200b-f423-492e-a84f-c422794d3a2f.png)
- 3x3 matrix 변환 행렬에 해당하는 H는 위아 같이 표현이 된다.
- H를 사용하면 image A, image B를 정합시켜줄 수 있다.
- image A를 image B에 겹치게 변환시켜줄 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146318499-00a8dd1e-9dd7-4cbf-8e25-76625f0aa93e.png)
- H와 자표계를 행렬곱 연산을 해주면 된다.

![image](https://user-images.githubusercontent.com/69780812/146318559-309841c5-ec16-45ce-83d6-42e2e0f1d364.png)
- 중요한 점은 위 식으로 계산하여 개발하는 경우가 많다.
- x'을 정확히 구하려면 위 그림의 분모로 나눠줘야 올바른 결과를 얻을 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146318713-2364ad7e-4a24-4212-8e70-03abad37b49f.png)

![image](https://user-images.githubusercontent.com/69780812/146318809-c89bbb09-2673-4c83-83f0-e820b9cc1f01.png)

- 합쳐주면 위와 같은 이미지가 변환된 결과이다.
- hole 현상이 발생한다.

![image](https://user-images.githubusercontent.com/69780812/146318946-2c7251aa-a8d5-4c95-a790-de8a73a81c97.png)
- 참고한 글에 의하면 interpolation으로 보강해주면된다고 한다.

![image](https://user-images.githubusercontent.com/69780812/146319037-4b771c1c-822e-48a8-93bd-032d72e929fd.png)
- backward mapping 방식을 적용한 것이다.

![image](https://user-images.githubusercontent.com/69780812/146319131-3b7c0621-8152-4350-a30b-d21c712b1b1e.png)
- cv2.warpPerspective()를 적용했을 때의 영상이다.

# Reference
- https://ballentain.tistory.com/38
- https://wewinserv.tistory.com/89
- https://www.youtube.com/watch?v=tWHcHC2n0Mg