# Inverting Gradients – 연합학습에서 프라이버시를 깨는 것이 얼마나 쉬운가?

## 소개

이 저장소는 아래 논문에서 제안된 **gradient 기반 이미지 재구성 알고리즘**의 구현입니다:

**Jonas Geiping, Hartmut Bauermeister, Hannah Dröge, Michael Moeller**  
*Inverting Gradients -- How Easy Is It to Break Privacy in Federated Learning?*  
(2020.03.31)  
https://arxiv.org/abs/2003.14053v1  

논문 원문: https://arxiv.org/abs/2003.14053
깃허브 원문: https://github.com/JonasGeiping/invertinggradients

---

## 입력 이미지 및 재구성 개요

- Model: ResNet18 (ImageNet으로 학습)  
- Input: ImageNet validation 이미지  
- Output: gradient 정보만으로 재구성된 이미지

---

## Abstract 

연합학습(Federated Learning)은 사용자 디바이스에서 생성된 **gradient 업데이트만**을 서버로 보내 모델을 학습하는 방식입니다.  
데이터는 디바이스에 남아 있어 프라이버시가 보호된다고 여겨져 왔습니다.

그러나 본 논문은 다음을 보여줍니다:

### Gradient만 공유해도 프라이버시가 쉽게 노출될 수 있음
- 코사인 유사도 기반 손실 함수와 적대적 최적화 기법을 이용하면  
  gradient 정보만으로 **입력 이미지를 고해상도로 복원할 수 있음**  
- 이미 학습된 네트워크에서도 재구성 가능

### 추가 분석
- 네트워크 구조와 파라미터는 재구성 난이도에 영향을 줌  
- 완전연결층(Fully Connected Layer)의 입력은 아키텍처와 무관하게 **분석적으로 복원 가능**  
- 여러 gradient를 평균하여 전송해도 **프라이버시 보호 효과가 부족함**

**결론:** 연합학습에서 gradient 공유는 본질적으로 안전하지 않다.
