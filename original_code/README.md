## 깃허브 원문
https://github.com/JonasGeiping/invertinggradients  

## 코드 재현 성공/불가 요약
- **`Recovery from Gradient Information.ipynb` - 재현 성공**
    - **[가장 기본적인 실험]** 이것이 논문의 핵심 아이디어를 보여주는 기본 실험 코드일 가능성이 높습니다. 단일 이미지의 **기울기(gradient) 정보**로부터 원본 이미지를 복원하는 과정을 구현한 것으로 보입니다.
- **`Recovery from Weight Updates.ipynb` - 재현 성공**
    - **[가중치 업데이트 실험]** 기울기(gradient)가 아닌, 여러 번의 로컬 업데이트 후의 **가중치(weight) 업데이트** 정보로부터 이미지를 복원하는 실험으로 보입니다. 이는 논문에서 다루는 'Federated Averaging' 시나리오와 관련이 깊습니다.
- **`ResNet18 - trained on ImageNet.ipynb` - 재현 불가(ImageNet 데이터 셋은 코랩에서 학습 불가)**
    - **[ImageNet 학습된 ResNet-18 실험]** ImageNet 데이터셋으로 **미리 학습된(trained)** ResNet-18이라는 깊은 모델을 대상으로 공격을 시도하는 노트북입니다. 논문에서도 이 모델을 사용한 결과를 보여줍니다.
- **`ResNet152 - trained on ImageNet.ipynb` - 재현 불가(ImageNet 데이터 셋은 코랩에서 학습 불가)**
    - **[ImageNet 학습된 ResNet-152 실험]** ResNet-18보다 훨씬 더 깊은 ResNet-152 모델을 사용한 실험입니다.  더 복잡한 모델에서도 공격이 성공하는지 보여주기 위한 코드입니다.
- **`ResNet18 - untrained (ImageNet version).ipynb` - 재현 불가(ImageNet 데이터 셋은 코랩에서 학습 불가)**
    - **[학습되지 않은 ResNet-18 실험]** 위와 반대로, **학습되지 않은(untrained)** ResNet-18 모델을 사용한 실험입니다. 모델이 학습되었는지 여부가 복원 품질에 어떤 영향을 미치는지 비교하기 위한 것입니다.
- **`Multiple images and multiple local update steps (ConvNet).ipynb` - 재현 성공**
    - **[다중 이미지 및 다중 스텝 실험]** 단일 이미지가 아닌 **여러 이미지(batch)**의 기울기를 평균내고, **여러 번의 로컬 업데이트(epoch)**를 수행하는, 더 현실적인 연합 학습 환경(Federated Averaging)을 가정한 실험입니다.
- **`ResNet32-10 - Recovering 100 CIFAR-100 images.ipynb` - 재현 성공**
    - **[CIFAR-100 100장 복원 실험]** CIFAR-100 데이터셋의 이미지 **100장**의 기울기를 평균 낸 값으로부터 개별 이미지를 복원하려는, 논문의 "multi-image setting"에 대한 핵심 실험 중 하나입니다. (shark, snail, apple, aquarium fish)
