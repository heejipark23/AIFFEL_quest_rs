# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희지
- 리뷰어 : 김나연


# PRT(Peer Review Template)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - PlainNet50에서 shortcut용 1×1 Conv가 제거되어 ResNet50과 파라미터 수가 다르다.
        - <img width="682" height="277" alt="image" src="https://github.com/user-attachments/assets/90710e56-e1bd-413a-b8bc-d9563e8d8ff0" />

    - torchvision에서 제공하는 데이터셋으로 학습 진행 시 loss가 감소하는 것이 확인되었다.
        - <img width="1696" height="466" alt="image" src="https://github.com/user-attachments/assets/24693972-fefe-4b1b-80fe-b415c9cc1f2e" />

    - validation accuracy 기준으로 Ablation Study 결과표가 작성되었다.
        - <img width="1705" height="701" alt="image" src="https://github.com/user-attachments/assets/fea6bfda-b743-43d1-bcd7-f41b78be21b1" />

    
- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - ResNet의 구현 방식이 텍스트로 상세히 설명이 되어있다.
        - <img width="733" height="262" alt="image" src="https://github.com/user-attachments/assets/d1b71630-206e-4eee-bce2-99b1c1cb589c" />

        
- [X]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - Overfitting이 발생함을 인지하고 해결 방안으로 데이터 증강을 적용하였다.
        - <img width="658" height="330" alt="image" src="https://github.com/user-attachments/assets/dd43215d-0931-47f5-8813-d13ad5a45d79" />
        - <img width="1151" height="712" alt="image" src="https://github.com/user-attachments/assets/01e7e75f-b6d2-4f32-a48e-77a504993284" />

    - 매 에포크마다 학습률을 다르게 설정하여 학습을 안정화 시켰다.
        - <img width="705" height="90" alt="image" src="https://github.com/user-attachments/assets/3c0c7d13-cc4b-4ab1-8ae5-25a225662c1b" />
        - <img width="1271" height="608" alt="image" src="https://github.com/user-attachments/assets/bc7dd8d0-6326-4f75-9b77-6c6801bf4c0b" />


- [X]  **4. 회고를 잘 작성했나요?**
    - 모델 별로 실험한 결과를 그래프와 표로 보기 쉽게 정리하였다.
        - <img width="1705" height="701" alt="image" src="https://github.com/user-attachments/assets/fea6bfda-b743-43d1-bcd7-f41b78be21b1" />
        - <img width="1696" height="466" alt="image" src="https://github.com/user-attachments/assets/24693972-fefe-4b1b-80fe-b415c9cc1f2e" />

        
- [X]  **5. 코드가 간결하고 효율적인가요?**
    - 구현 해야하는 모델에서 공통적으로 적용할 수 있는 부분과 각각 구현해야 하는 부분을 클래스로써 구현하였다.
        - <img width="447" height="80" alt="image" src="https://github.com/user-attachments/assets/bec8941a-a54d-4d45-809c-bd8b308b6b12" />
        - <img width="600" height="72" alt="image" src="https://github.com/user-attachments/assets/9ba99ff0-f6f7-4639-a90b-342f74bd8a7e" />
        - <img width="902" height="490" alt="image" src="https://github.com/user-attachments/assets/6bdb4e51-b62c-4388-b244-1b71c8e28f5e" />



# 회고(참고 링크 및 코드 개선)
```
`use_residual=False`일 때 1×1 Conv까지 함께 제거되어 PlainNet50이 제대로 구현되지 않은게 아쉽습니다.
해당 부분만 수정한다면 Ablation Study가 좀 더 공정해질 것 같습니다.

모델 학습 과정에서 학습률을 조정하고 데이터 증강을 통한 성능 향상이 인상 깊었습니다.
또한 Seed 고정으로 학습을 고정 시킬 수도 있다는 점을 배웠습니다.
```

