# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희지
- 리뷰어 : 김나연


# PRT(Peer Review Template)
- [X]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 한국어 전처리를 통해 학습 데이터셋을 구축하였다.
        - <img width="1373" height="659" alt="image" src="https://github.com/user-attachments/assets/94a4257d-164c-4c10-a6f0-6598acab3fc8" />
    - 트랜스포머 모델을 구현하여 한국어 챗봇 모델 학습을 정상적으로 진행하였다.
        - <img width="898" height="747" alt="image" src="https://github.com/user-attachments/assets/1634356c-cf27-425f-8349-1be41db91dd6" />
    - 한국어 입력문장에 대해 한국어로 답변하는 함수를 구현하였다.
        - <img width="427" height="672" alt="image" src="https://github.com/user-attachments/assets/5a4b3f16-1e6d-4e02-8e65-1380cc47bef1" />
    
- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 트랜스포머 모델 전체에 대한 도식도 그림을 통해 코드의 이해를 돕고 있다.
        - <img width="1201" height="744" alt="image" src="https://github.com/user-attachments/assets/77c4c0e6-9aed-47cf-96b3-0bcab95a0540" />

- [X]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - Early Stopping 기준과 실제 개선 방향의 불일치, 과적합, 생성 품질에 대한 문제점을 인식하고 아래와 같이 해결하였다.
        - Early Stopping 판정 기준을 val_acc 최대값으로 변경 -> 추가 학습 여지 확보
        - 임베딩 가중치 공유 (인코더 = 디코더 = 출력층) -> 파라미터 감소 및 과적합 완화
        - CrossEntropyLoss에 label_smoothing 추가 ->과적합 완화 및 일반화 성능 향상
    - vocab size = 4000, 8000 두 가지로 실험한 결과를 보여줬다.
        - <img width="667" height="702" alt="image" src="https://github.com/user-attachments/assets/9ac1d4ec-1629-4f85-a849-b486710d88b2" />

- [X]  **4. 회고를 잘 작성했나요?**
    - <img width="1706" height="751" alt="image" src="https://github.com/user-attachments/assets/fd090df3-9802-46c2-8b2d-6e9014ac5788" />

- [X]  **5. 코드가 간결하고 효율적인가요?**
    - PositionalEncoding, scaled_dot_product_attention, MultiHeadAttention, Encoder, Decoder, Transformer 클래스들을 통해 중복을 최소화하고 효율적으로 작성했다.


# 회고(참고 링크 및 코드 개선)
```
프로젝트에 정성이 가득 담긴 것 같아서 너무 멋져요!
```

