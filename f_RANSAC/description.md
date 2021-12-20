# Overview
- 너무 유명해서 모르면 간첩이란다.
- 특정 분야에 국한되지 않는 일반적인 방법론이다.

# 1. 필요성
![image](https://user-images.githubusercontent.com/69780812/146725445-6162eb35-d6b5-4659-9d53-7e65d12b9f42.png)
- 왼쪽 아래 그림과 같은 관측 데이터들을 치소자승법을 이용해 fitting하여 포물선 근사시키면 오른쪽과 같이 된다.
  - 최소 자승법 : sum(residual^2)

![image](https://user-images.githubusercontent.com/69780812/146725601-f565a156-3f39-41e8-9490-bac7aa42a4d5.png)
- 현실에서는 이전 그림처럼 깨끗한 관측데이터는 얻기 어렵다.
- 그래도 위 같은 관측 데이터는 최소자승법을 적용하면 훌륭한 결과를 얻을 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146725683-830da40e-d867-43b0-a325-d419445fdb17.png)
- 하지만, 약간의 노이즈가 아닌 데이터 자체가 완전히 틀어져있는 경우도 있다.
- 정상적인 분포에서 벗어난 이상한 데이터들을 **outlier**라고 부른다.
- outlier가 끼어있으면 최소 자승법은 엉망이 되어 버린다.

![image](https://user-images.githubusercontent.com/69780812/146725782-65771674-a1ef-4455-9160-fc820469a26b.png)
- RANSAC을 사용해서 근사 시키면 위와 같은 깨끗한 결과를 얻을 수 있다.

# 2. 이해
- RANSAC : RANdom SAmple Consensus)의 약자다.
  - 무작위로 샘플을 뽑아서 최대로 컨센서스가 형성된 녀석을 선택한다는 의미다.
- 최소 자승법은 sum(residual^2)의 최소화하도록 모델을 찾지만 RANSACdms **컨센서스가 최대인 즉, 가장 많은 수의 데이터들로 부터 지지 받는 모델을 선택하는 방법이다.**
- RANSAC과 치소 자승법의 차이는 무엇을 기준으로 모델의 파라미터를 찾는가의 차이다.
  - 관측 데이터에 이상한 outlier가 많더라도 데이터 근사가 가능하다는 점이다.

# 3. Inlier와 Outlier
- RANSAC 알고리즘을 알기 전에 위 두 개념을 확실히 잡아야한다.
- RANSAC과 관련된 여러 미묘한 문제들은 결국 inlier아 outlier의 구분 문제이기 때문이다.
- outlier는 데이터 분포에서 현저히 벗어나있는 것이다. 그렇다면 오차가 크면 outlier, 그렇지 않으면 inlier라는 것인가 ?
  - No, 편의상으로, 별다른 방법이 없어서 그렇게 할 뿐이다.
  - inlier의 데이터라 할지라도 조금씩 차이가 있으므로 어떤 데이터는 편차가 클 것이고 어떤 것은 편차가 작을 것이다. 그렇다해도 이들은 inlier이다.
  - inlier 더라도 outlier의 데이터와 매우 유사한 값을 가질 수 있다. 아무리 유사하더라도 outiler는 여전히 outlier다.

# 4. RANSAC 알고리즘
- 컨센서스가 최대인 모델을 뽑기 위한 절차적 방법을 말한다.
- 일단 무작위로 sample 데이터를 뽑아서 이 샘플 데이터를 만족하는 모델 파라미터를 구한다.
- 이렇게 구한 모델과 가까이 있는 데이터들의 개수를 세서 그 개수가 크면 이 모델을 기억해둔다.
  - 위의 과정을 N번 반복해서 가장 지지하는 데이터의 개수가 많았던 모델을 최종 결과로 반환한다.
- 포물선 근사 문제를 RANSAC으로 풀어보도록 하자.
  - 관측 데이터 값들은 (x1,y1), ..., (xn, yn) 포물선의 방정식은 f(x) = ax^2 + bx +c 포물선을 결정하기 위해 뽑아야할 샘플의 개수는 최소 3개다.

## Sequence
1. c_max = 0으로 초기화
2. 무작위로 세 점 p1, p2, p3를 뽑는다.
3. 세 점을 지나는 포물선 f(x)를 구한다.
4. 이렇게 구한 f(x)와의 거리 r_i = |y_i - f(x_i)|가 T 이하인 데이터 개수 c를 구한다.
5. 만일 c가 c_max보다 크다면 현재 f(x)를 저장한다. (과거 저장된 값은 버린다.)
6. 2 ~ 5 과정을 N번 반복 후 최종 저장되어 있는 f(x)를 반환한다.
7. 최종 f(x)를 지지하는 데이터들에 대해 최소 자승법을 적용해 결과를 refine (선택사항)

# 5. 활용 예
![image](https://user-images.githubusercontent.com/69780812/146727558-9dcb4568-ffdf-4794-981e-03a7d2bfea4a.png)
- local feature matching을 이용해 영상에서 특정 물체를 찾을 때

![image](https://user-images.githubusercontent.com/69780812/146727647-67534575-c43c-45e0-9d70-11402043cd6b.png)
- Visual Odometry를 통해 인접한 영상프레ㅣㅁ에서 카메라 모션을 추정할 때

![image](https://user-images.githubusercontent.com/69780812/146727763-2d285de4-12b4-47b7-9d9a-c6a53ec2a199.png)
- scene matching을 수행할 때

![image](https://user-images.githubusercontent.com/69780812/146727877-c6d845f0-8e4e-4657-a5b7-a31eb303db57.png)
- 물체 추적을 위해 인접한 영상프레임에서 이동체 모션을 추정할 때

# 6. RANSAC 알고리즘의 파라미터