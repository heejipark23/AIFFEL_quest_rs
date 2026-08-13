# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희진
- 리뷰어 : 조영근


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - Word2Vec 임베딩 생성 → TF-IDF 기반 target/attribute 추출 → WEAT score 계산 → 전체 장르쌍(21개 장르, 210개 조합) 분석 → Heatmap 시각화까지 문제에서 요구하는 전체 파이프라인이 완성되어 있다.
    - 아래 결과물이 모두 제시되어 있다.
        - Word2Vec 학습 및 유사 단어 확인
        - TF-IDF 기반 target set 구축
        - 장르별 attribute set 구축
        - WEAT score 계산 함수 구현
        - 210개 장르쌍 WEAT score 계산
        - Heatmap 시각화
        - 결과 해석 및 한계 분석
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 가장 핵심적인 부분인 TF-IDF 단어 추출과 WEAT 계산 과정이 함수 단위로 분리되어 있으며 설명도 포함되어 있다.
    - <img width="680" height="345" alt="image" src="https://github.com/user-attachments/assets/a115f62f-6449-48d3-a205-438b14850f34" />
    - WEAT 계산 부분에서 코사인 유사도의 구현 이유를 직접 설명한 주석이 있어 의도를 이해하기 쉽다.
    - <img width="731" height="683" alt="image" src="https://github.com/user-attachments/assets/c1185546-9a27-432a-9c42-69eea5b8a65d" />

        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 단순히 WEAT를 계산하는 데서 끝나지 않고 TF-IDF의 문제점을 발견한 뒤 이를 개선하기 위한 추가 실험을 진행하였다.
      ```
      (1) 문서 단위 변경
      초기: 파일 단위 TF-IDF
      개선: 시놉시스 단위 TF-IDF
      결과: 문서 수 2개 → 49,090개
      로 증가하면서 IDF 변별력이 향상되었다.
      ```
    - <img width="1270" height="168" alt="image" src="https://github.com/user-attachments/assets/88887020-4745-46dd-80ff-4fdbbd7e5045" />

- [x]  **4. 회고를 잘 작성했나요?**
    - 결과를 단순 나열하지 않고 아래 내용을 체계적으로 분석하였다.
    - <img width="1483" height="731" alt="image" src="https://github.com/user-attachments/assets/f8802fd5-ee82-4e0a-9e96-4f6000ca56ee" />

        
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 반복적으로 사용되는 로직을 함수화하여 코드의 재사용성을 높였다.
    - TF-IDF 개선 이후에도 기존 코드 구조를 크게 변경하지 않고 확장 가능한 형태로 작성된 점이 좋다.
    - <img width="805" height="481" alt="image" src="https://github.com/user-attachments/assets/94b03877-3aa0-4022-8e9f-f9880c41681b" />




# 회고(참고 링크 및 코드 개선)
```
# 이번 실험의 가장 큰 강점은 WEAT score를 계산하는 것에서 끝나지 않고, 결과가 왜 그렇게 나왔는지 데이터 관점에서 원인을 분석한 부분이라고 생각한다.
# 단순 구현 과제 수준을 넘어 TF-IDF의 한계, target set 품질 문제, 장르 간 단어 중복 문제 등을 스스로 발견하고 개선 실험을 수행한 점이 인상적이었다.
# 또한 시놉시스 단위 문서 분할과 불용어 제거를 통해 장르 대표 단어의 품질을 높인 과정이 프로젝트의 완성도를 크게 높였다고 판단된다.
```

