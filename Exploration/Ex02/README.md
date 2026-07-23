# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희지
- 리뷰어 : 김나연


# PRT(Peer Review Template)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 인물 사진에 대한 Semantic Segmentation, 배경 합성에 대한 문제는 해결 되었으나 동물 사진에 대한 Semantic Segmentation 결과는 확인되지 않음
        - <img width="646" height="683" alt="image" src="https://github.com/user-attachments/assets/ab12bb8b-648c-4530-801f-cff5acec7cdb" />
        - <img width="847" height="653" alt="image" src="https://github.com/user-attachments/assets/38da6af3-9ef1-4c55-bc11-2ded8c4e00f7" />


    
- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 문제 원인을 파악하고 해결하는 과정이 가장 핵심적이라 생각합니다.
    - 클래스 분류 과정에서 argmax를 이용하는 것이 아닌 threshold를 사용하여 문제를 해결 하였으며 이 과정에서 Softmax를 통한 threshold 적용이 인상 깊었다.
        - <img width="1681" height="277" alt="image" src="https://github.com/user-attachments/assets/e06d932a-3b93-4abc-8b81-f32fadce9cb3" />
        - <img width="842" height="747" alt="image" src="https://github.com/user-attachments/assets/642e9136-82b9-4ff0-a67b-f05c505ceaf1" />
        - <img width="930" height="506" alt="image" src="https://github.com/user-attachments/assets/1292cd96-4ff1-4c6e-8838-fafefaf27056" />


        
- [X]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 인물 사진에 Semantic Segmentation 모델을 적용 했을 때 의자까지 인물로 선택된 부분에 대한 문제를 기록하고 해결 하였다.
        - <img width="646" height="566" alt="image" src="https://github.com/user-attachments/assets/3c73265e-5b66-444b-9401-cb5cdb9bda30" />
        - <img width="1051" height="577" alt="image" src="https://github.com/user-attachments/assets/c0ff3fc9-2401-4fd7-9a98-f1cd7645680e" />
        
- [X]  **4. 회고를 잘 작성했나요?**
    - 인물 사진에 대해 threshold 값을 조정하여 해결하는 과정이 충분히 드러났으며 사용된 모델의 한계로 인한 문제점까지 지적하였다.
        - <img width="1427" height="647" alt="image" src="https://github.com/user-attachments/assets/8e8ee0c5-4b3c-42f5-8e99-833af8298334" />

    - 코드 실행 과정을 이미지와 그래프를 통해 적절히 시각화 하였다.
        - <img width="632" height="463" alt="image" src="https://github.com/user-attachments/assets/661d6315-3648-48c4-b87f-4159c23ebcb1" />
        
- [X]  **5. 코드가 간결하고 효율적인가요?**
    - 각 함수와 코드마다 적절한 주석이 달려있다.
    - 코드 중복을 최소화하고 모듈화 하였다.


# 회고(참고 링크 및 코드 개선)
```
저도 이번 노드를 수행하면서 느꼈지만 DeepLabV3는 객체의 전체 영역은 잘 분할하지만 동물 털과 같이 작은 경계는 잘 못잡는 것 같습니다.
여기서 더 또렷한 경계를 찾아 낼려면 더 세밀한 경계 추출에 강한 모델을 사용하는 방법이 있을 것 같아요.
현재 과제에서 사용 가능한 DeepLabV3을 사용해서 최선의 성능을 뽑아 내신 것 같습니다!

```

