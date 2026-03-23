### 5-1. Observation Questions

1. Describe the patterns you see in the first-layer filters. Do they resemble edge detectors, color detectors, or something else?
2. How do feature maps change from the first conv layer to the last? What does this suggest about hierarchical feature learning?
3. Compare the Grad-CAM heatmaps of the Baseline and BatchNorm models. Does one focus on more relevant image regions?
4. Did you find any images where one model's attention (Grad-CAM) was clearly better than the other's? Describe what you found.


#### 1. 단순히 edge-detector만 있는 것이 아닌 color-sensitive edge detector의 느낌이 강하게 난다. 

#### 2. conv1에서는 원본의 느낌과 경계가 남아있고, edge/texture가 남아있다. conv2에서는 패턴이 더 흐릿해지고, 특정 구조가 강조되어 보인다. conv3에서는 거의 추상화되고, 인간의 눈에서는 거의 의미 없어 보인다.
이러한 것은, 계층적 학습 구조를 보여주는데, conv1에서는 저수준의 edge와 color를 남겨두고, conv2에서는 중간수준의 추상화를, conv3에서는 아예 의미로의 고수준의 추상화가 일어난다.

#### 3. Grad-CAM Heatmaps (Baseline vs. BatchNorm)
##### Baseline
- cat의 경우 아예 heatmap이 나오지 않고, ship에서는 이상한 위치에 찍혔다.
- 전반적으로 불안정하다.

##### BatchNorm
- 훨씬 넓고 의미있는 영역을 커버한다. cat의 경우 얼굴/몸, plane의 경우 기체 전체의 모양에 맞게 잘 경계를 뒀다.
- heatmap이 살아있다.
###### BatchNorm이 feature를 더 안정적으로 학습해서 heatmap이 훨씬 더 잘 잡힌다.

#### 4. cat의 경우 압도적으로 BatchNorm에서 attention이 훨씬 더 잘 잡혔다. plane의 경우도 비행기 전체 구조를 따라 BatchNorm에서 잘 잡혔다. ship의 경우, 둘 다 애매하다고 말할 수 있다.
