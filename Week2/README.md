# CIFAR-10 Neural Network 과제 안내

## 과제 개요

CIFAR-10 데이터셋을 활용하여 CNN(합성곱 신경망)을 구축하고, 다양한 정규화(Regularization) 기법의 효과를 실험적으로 비교/분석하는 과제입니다.

---

## !! 반드시 읽어주세요 !!

> **모델 학습에는 상당한 시간이 소요됩니다. 절대로 마감 직전에 시작하지 마세요.**
>
> - Task 1~3: 각각 20 epoch 학습 (Colab GPU 기준 약 3~5분, **CPU 기준 약 30분~1시간**)
> - Task 4 (Best Model): 30 epoch 이상 학습 + 하이퍼파라미터 튜닝을 여러 번 반복해야 합니다
> - Task 5: 시각화 실행 및 분석
> - Task 6: 결과 분석 및 서술형 답변 작성
>
> 코드를 한 번 실행하는 것만으로도 **Colab GPU 기준 최소 30분~1시간**, **CPU 기준 2~3시간 이상** 걸립니다.
> 여기에 코드 작성, 디버깅, 하이퍼파라미터 실험 시간까지 고려하면 **마감 최소 3~4일 전에는 시작**하시기 바랍니다.
>
> 특히 Task 4에서 높은 성적(A 이상)을 목표로 한다면, 다양한 아키텍처와 하이퍼파라미터 조합을 시도해야 하므로 시간이 훨씬 더 필요합니다.

---

## 실행 환경: Google Colab (권장)

이 과제는 **Google Colab** 환경에서 실행하는 것을 권장합니다. Colab은 무료 GPU를 제공하므로 학습 시간을 크게 단축할 수 있습니다.

### Colab 설정 방법

1. [Google Colab](https://colab.research.google.com/)에 접속합니다.
2. `파일` > `노트 업로드`를 클릭하여 `CIFAR10_NN_Assignment.ipynb` 파일을 업로드합니다.
3. **GPU 런타임을 반드시 설정합니다:**
   - 메뉴에서 `런타임` > `런타임 유형 변경` 클릭
   - 하드웨어 가속기를 **T4 GPU**로 변경
   - `저장` 클릭
4. 첫 번째 셀(Setup)을 실행하여 `Using device: cuda`가 출력되는지 확인합니다.

### Colab 사용 시 주의사항

- **세션 시간 제한**: Colab 무료 버전은 약 90분간 미사용 시 또는 최대 12시간 후 세션이 종료됩니다. 세션이 끊기면 **학습된 모델이 모두 사라지므로**, 중간중간 결과를 저장하거나 셀을 다시 실행해야 합니다.
- **런타임 연결 유지**: 학습 중에는 브라우저 탭을 닫지 마세요.
- 이미 PyTorch가 설치되어 있으므로 별도 설치가 필요 없습니다.

### 로컬 환경 사용 시

로컬에서 실행하려면 Python 3.8+ 환경에서 아래 패키지를 설치하세요:

```bash
pip install torch torchvision matplotlib numpy
```

Apple Silicon Mac의 경우 MPS 가속이 자동으로 적용됩니다.

---

## 과제 구성 (총 6개 Task)

### Task 1: Baseline CNN (정규화 없음)
- 2~3개의 Conv 블록(Conv2d → ReLU → MaxPool2d)과 1~2개의 FC 레이어로 구성된 기본 CNN을 구현합니다.
- Dropout, BatchNorm, Weight Decay 없이 순수한 CNN 성능을 측정합니다.
- `# TODO` 부분을 채워 넣으세요.

### Task 2: Dropout 정규화
- Task 1의 구조를 복사한 뒤 **Dropout 레이어**를 추가합니다.
- dropout rate(예: 0.25, 0.5)를 바꿔가며 실험해 보세요.

### Task 3: Batch Normalization
- Task 1의 구조를 복사한 뒤 **BatchNorm2d / BatchNorm1d**를 추가합니다.
- Conv 레이어 뒤에 BatchNorm2d, FC 레이어 뒤에 BatchNorm1d를 넣습니다.

### Task 4: Best Model (모든 기법 조합)
- Task 1~3에서 배운 기법들을 **조합**하여 최고 성능의 모델을 만듭니다.
- 사용 가능한 기법들:
  - BatchNorm + Dropout 조합
  - Weight Decay (optimizer의 `weight_decay` 파라미터)
  - Data Augmentation (`RandomHorizontalFlip`, `RandomCrop` 등)
  - 더 깊거나 넓은 아키텍처
  - Learning Rate Scheduling
  - 더 많은 epoch
- **최종 성적은 이 모델의 Test Accuracy로 결정됩니다.**

### Task 5: CNN 시각화
- 제공된 헬퍼 함수를 사용하여 다음을 시각화합니다:
  - 첫 번째 Conv 레이어의 필터
  - 각 레이어의 Feature Map
  - Grad-CAM 히트맵
- Baseline 모델과 BatchNorm 모델을 **비교**합니다.
- 서로 다른 클래스의 이미지 최소 **3장**에 대해 비교 분석합니다.
- 관찰 결과를 **서술형**으로 작성합니다.

### Task 6: 결과 분석
- 4개 모델(Baseline, Dropout, BatchNorm, Best Model)의 최종 Test Accuracy를 비교합니다.
- Training Curve를 분석합니다.
- 서술형 질문 3개에 답변합니다.

---

## 채점 기준

### 최종 성적 (Task 4 - Best Model의 Test Accuracy 기준)

| 등급 | Test Accuracy | 설명 |
|------|--------------|------|
| **A+** | >= 85% | 우수한 아키텍처 + 잘 조율된 정규화 |
| **A** | >= 82% | 좋은 기법 조합 |
| **B+** | >= 79% | 양호 - 최적화 여지 있음 |
| **B** | >= 76% | 보통 - 일부 기법을 효과적으로 사용 |
| **C** | >= 70% | 최소한의 노력 |
| **F** | < 70% | 미흡 |

### 각 Task별 최소 통과 기준 (모두 충족해야 함)

| Task | 최소 Accuracy |
|------|-------------|
| Task 1 (Baseline) | >= 65% |
| Task 2 (Dropout) | >= 65% |
| Task 3 (BatchNorm) | >= 70% |
| Task 4 (Best Model) | >= 70% |
| Task 5 (시각화) | 모든 시각화 완료 + 질문 답변 |
| Task 6 (분석) | 모든 질문에 성실히 답변 |

---

## 제출 방법

1. `CIFAR10_NN_Assignment.ipynb` 파일의 모든 `# TODO` 부분을 완성합니다.
2. **모든 셀을 위에서 아래로 순서대로 실행**하여 출력 결과가 포함된 상태로 제출합니다.
3. Task 5의 관찰 결과와 Task 6의 분석 답변이 모두 작성되어 있는지 확인합니다.
4. Colab 사용 시: `파일` > `노트북 다운로드 (.ipynb)`로 저장한 뒤 제출합니다.

---

## 주의사항

- **사전학습 모델(Pretrained Model) 사용 금지** — 모든 모델은 처음부터 학습해야 합니다.
- `model.train()`과 `model.eval()`의 차이를 이해하세요. Dropout과 BatchNorm은 학습/평가 시 다르게 동작합니다.
- Validation set으로 하이퍼파라미터를 조정하고, **Test set은 Task 6에서 최종 평가 시에만 한 번 사용**합니다.
- 노트북의 출력 결과(그래프, 정확도 등)가 **모두 포함된 상태**로 제출해야 합니다.

---

## 힌트

- Task 4에서 높은 성적을 받으려면:
  - Data Augmentation을 적극 활용해 보세요. 어떤 augmentation이 CIFAR-10에 적합할지 생각해 보세요.
  - 네트워크를 더 깊게 또는 넓게 만들어 보세요. 단, 너무 크면 overfitting될 수 있습니다.
  - Task 2와 Task 3에서 효과가 좋았던 기법을 함께 사용해 보세요.
  - Learning rate scheduler를 사용하면 후반 학습이 안정됩니다.
- Dropout rate를 너무 높게 설정하면 얕은 네트워크에서는 오히려 성능이 떨어질 수 있습니다. 이것 자체가 유용한 관찰이니 분석에 활용하세요.
- 학습 중간중간 Validation Accuracy를 확인하면서 overfitting 여부를 판단하세요.
- Colab 세션이 끊길 수 있으므로 **Task별로 완성하는 즉시 결과를 확인**하는 습관을 들이세요.
