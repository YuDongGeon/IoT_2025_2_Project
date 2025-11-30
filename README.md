# Inverting Gradients – 연합학습에서 프라이버시를 깨는 것이 얼마나 쉬운가?

### 📌 Update (Feb 2022)
최신 프레임워크에는 본 공격뿐 아니라 여러 최신 프라이버시 공격 구현이 포함되어 있습니다.  
👉 https://github.com/JonasGeiping/breaching

---

## 📄 소개

이 저장소는 다음 논문에서 제안된 **그래디언트 기반 이미지 재구성 알고리즘**을 구현한 것입니다:

> **Jonas Geiping, Hartmut Bauermeister, Hannah Dröge, Michael Moeller**  
> *Inverting Gradients -- How Easy Is It to Break Privacy in Federated Learning?*  
> (2020.03.31)  
> https://arxiv.org/abs/2003.14053v1  

논문 원문: https://arxiv.org/abs/2003.14053

---

## 📸 입력 이미지 & 재구성 개요

- **Model:** ResNet18 (ImageNet 학습됨)  
- **Input:** ImageNet validation 이미지  
- **Output:** gradient 정보만으로 재구성된 이미지

---

## 📝 Abstract 요약

연합학습(FL)은 서버가 사용자 디바이스로부터 **gradient 업데이트만** 받아서 모델을 학습하는 방식입니다.  
이는 데이터를 서버로 직접 보내지 않기 때문에 **프라이버시 보호가 가능하다**고 여겨졌습니다.

하지만 본 논문에서는 다음을 입증합니다:

### ❗ Gradient 공유만으로도 프라이버시가 깨진다
- 코사인 유사도 손실 + adversarial attack 기반 최적화로  
  **입력 이미지를 고해상도로 재구성 가능**
- 학습된 네트워크에서도 재구성 성공

### 📌 추가 발견  
- 네트워크 구조/파라미터가 재구성 난이도에 영향을 미침  
- 완전연결층 입력은 아키텍처와 무관하게 **분석적으로 복원 가능**  
- Gradient를 여러 iteration 또는 여러 이미지로 **평균내도 보호불가능**  

➡ 결론: **FL에서 gradient 공유는 본질적으로 안전하지 않다.**
