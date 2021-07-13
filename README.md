# PaperReview_Bag-Of-Tricks-For-ImageClassification

# Introduction

사소한 Trick을 적절히 모아 사용하면 큰 성능 향상을 이끌어 낼 수 있다.
<img src = 'https://user-images.githubusercontent.com/77375223/125416293-2b924bc2-c7d0-46b3-8776-8eb4c3e1464f.png'>
- FLOPs는 조금 증가하였지만(필요한 컴퓨팅 파워) 성능이 크게 향상 되었다.

### Base Line
<img src = 'https://user-images.githubusercontent.com/77375223/125416300-54e6d068-ba3e-40b1-8d9b-da99ab6b3b32.png'>
보편적으로 사용하는 학습 방법을 BaseLine으로 잡았습니다(성능을 비교하기 위해)<br>
① model을 선언한다. <br>
② input image를 Batch 단위로 나눈다. <br>
③ Batch 단위로 나눈 이미지에 전처리를 적용하여 모델에 넣는다. <br>
④ forward연산을 통해 가중치를 정하고 loss를 구한다. <br>
⑤ backward연산을 통해 기울기를 구하고 기울기에 맞게 가중치를 업데이트 한다. <br>

# Method

### Efficient Training
저자는 Efficient Training이라는 기법을 통해 성능을 향상시킬 수 있다고 주장합니다. 본 논문에서 제시하는 Efficient Training이란 Large Batch Training + low-precision을 모두 사용하는 것을 Efficient Training이라고 설명하고 있습니다.
