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
저자는 Efficient Training이라는 기법을 통해 성능을 향상시킬 수 있다고 주장합니다. 본 논문에서 제시하는 Efficient Training이란 Large Batch Training + Low-Precision Training을 모두 사용하는 것을 Efficient Training이라고 설명하고 있습니다.

### Large Batch Training
<img src = 'https://user-images.githubusercontent.com/77375223/125417698-a3584099-4575-49e3-a376-e33e69d1100a.JPG'>

Batch size가 증가하면 수렴률이 감소하는 문제가 발생할 수 있다. 따라서 해당 문제를 Learning Rate를 선형적으로 증가 시킴으로써 해결 할 수 있다고 주장합니다.<br>
본 논문에선 1e-1 * batch size/256 으로 설정하여 진행했습니다.

### Low precision training

<img src = 'https://user-images.githubusercontent.com/77375223/125418981-dd4e3fe2-00bd-40c9-8076-55c98fa795a9.png'>
CNN 연산을 할 때 보통 32-bit floating point를 사용합니다. floating point란 부동 소수점의 표현 방식을 말하는데, bit 숫자가 클 수록 표현할 수 있는 소수점의 범위가 넓어진다는 것으로 생각하면 편리하다. 즉 CNN연산에서 보편적으로 사용하는 FP32 방식을 사용하지 말고, FP16을 사용하면 학습 속도는 2~3배 가량 빨라질 수 있고, FP32에 비해 성능의 차이가 크지않고, 해당 논문에선 오히려 성능이 소폭 상승했다고 서술했습니다.

