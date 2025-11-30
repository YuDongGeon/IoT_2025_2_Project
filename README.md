Inverting Gradients – 연합학습에서 프라이버시를 깨는 것이 얼마나 쉬운가?

업데이트 2022년 2월:
최신 프레임워크에서는 이 공격뿐만 아니라 다른 많은 공격의 현대적 구현이 포함되어 있습니다.
https://github.com/JonasGeiping/breaching

이 저장소는 다음 논문에서 논의된 재구성 알고리즘(reconstruction algorithm) 구현입니다.

Jonas Geiping, Hartmut Bauermeister, Hannah Dröge, Michael Moeller.
Inverting Gradients -- How Easy Is It to Break Privacy in Federated Learning?
2020년 3월 31일
https://arxiv.org/abs/2003.14053v1

논문 원문 링크: https://arxiv.org/abs/2003.14053

입력 이미지와 그래디언트 기반 재구성

모델: 표준 ResNet18, ImageNet 데이터로 학습

이미지: 검증(validation) 세트에서 선택

초록(Abstract)

연합학습(Federated Learning, FL)의 기본 아이디어는 서버에서 신경망을 공동으로 학습하는 것입니다.
각 사용자는 네트워크의 현재 가중치를 받고, 자신의 로컬 데이터를 기반으로 **파라미터 업데이트(gradient)**를 서버로 전송합니다.

이 프로토콜은 효율적인 학습뿐만 아니라 사용자 프라이버시 보호 목적도 포함하고 있습니다.
사용자의 데이터는 디바이스에 남아 있고, 서버에는 gradient 정보만 공유되기 때문입니다.

하지만 본 논문에서는 gradient 공유가 안전하지 않다는 것을 보여줍니다.

코사인 유사도 손실(cosine similarity loss)과 적대적 공격(adversarial attack) 기법을 이용하면,

gradient 정보만으로도 고해상도 이미지를 충실하게 재구성할 수 있습니다.

또한 다음을 분석합니다:

네트워크 아키텍처와 파라미터가 입력 이미지 재구성 난이도에 미치는 영향

완전 연결층(Fully Connected Layer)에 입력되는 어떤 값도 나머지 아키텍처와 무관하게 분석적으로 재구성 가능

여러 iteration이나 여러 이미지를 대상으로 gradient를 평균내어도 사용자의 프라이버시는 보호되지 않음

→ 즉, 컴퓨터 비전 기반 연합학습에서 gradient만으로도 프라이버시가 쉽게 깨질 수 있음을 실험적으로 증명합니다.

코드(Code)

중심 파일: inversefed/reconstruction_algorithms.py

재구성 알고리즘 구현

다른 폴더와 파일들은 모델 정의 및 학습용이며, 재구성과 직접적 관계 없음

환경 설정(Setup)
Requirements
pytorch=1.4.0
torchvision=0.5.0


Anaconda 사용 시:

conda env create -f environment.yml
conda activate iv


ImageNet 실험을 수행하려면 ImageNet 다운로드 필요

또는 직접 이미지 사용 가능 → inversefed.construct_dataloaders 단계는 건너뜀

빠른 시작(Quick Start)
노트북 예제

ResNet-152 + ImageNet 예제 포함

Gradient 재구성 사용 예:

rec_machine = inversefed.GradientReconstructor(model, (dm, ds), config, num_images=1)
output, stats = rec_machine.reconstruct(input_gradient, None, img_shape=(3,32,32))


여기서 dm, ds는 데이터셋 평균/표준편차

input_gradient는 torch.autograd.grad로 계산된 gradient

CLI 사용 예제
python reconstruct_image.py --model ResNet20-4 --dataset CIFAR10 --trained_model --cost_fn sim --indices def --restarts 32 --save_image --target_id -1


모델, 데이터셋, cost function, 반복 횟수 등을 옵션으로 지정 가능

지정한 target 이미지 재구성 후 저장

핵심 요약

연합학습의 gradient 공유는 프라이버시를 완전히 보장하지 못함

Gradient만으로도 입력 이미지를 재구성 가능

네트워크 아키텍처와 gradient 평균화는 프라이버시 보호에 충분하지 않음

코드와 노트북으로 실제 gradient 재구성 실험 가능
