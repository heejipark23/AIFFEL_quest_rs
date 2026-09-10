# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희지
- 리뷰어 : 조영근
  

# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - `korean-english-park` 병렬 말뭉치를 불러오고, 한국어-영어 문장 쌍을 정제한 뒤 토큰화·텐서화하여 학습 가능한 데이터셋을 구성했다.
    - Encoder-Decoder 구조와 Bahdanau Attention을 구현했으며, 학습용 모델과 추론용 디코더 경로가 모두 포함되어 있다.
    - 최종 모델의 번역 결과와 Attention Map까지 출력하여 요구된 산출물을 확인할 수 있다.
    - 원본 94,123쌍을 확인하고 중복 제거, 노이즈 제거, 길이 필터를 거쳐 학습 데이터로 변환했으며, 최종적으로 `A_256_512 / best.pt` 체크포인트를 사용해 번역을 수행했다.
    - <img width="1067" height="586" alt="image" src="https://github.com/user-attachments/assets/2e929f21-d8ec-44a1-9499-e4e520c0c303" />


- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 핵심 모델 구성요소인 `BahdanauAttention`, `Encoder`, `Decoder`, `Seq2SeqAttention`의 역할과 데이터 흐름이 단계별로 설명되어 있다.
    - Attention에서 `<pad>` 위치를 `-inf`로 마스킹하고, Encoder에서 `pack_padded_sequence`를 사용하는 이유를 구체적으로 설명했다. 특히 소스 토큰의 약 35%가 패딩이라는 점을 근거로 마스킹의 필요성을 제시한 점이 좋다.
    - Decoder 입력에 임베딩과 context vector를 함께 사용하는 input feeding, 학습 시 teacher forcing, 추론 시 자기회귀 생성의 차이도 주석과 마크다운으로 설명되어 있다.
    - `get_ko_tokenizer()`, `train_step()`, `run_experiment()`, `translate_sentence()` 등 주요 함수에 docstring 또는 사용 목적에 대한 설명이 있다.
    - <img width="882" height="605" alt="image" src="https://github.com/user-attachments/assets/61f07ccf-aae2-44da-a6da-a5a2057f8e29" />


- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
    - `konlpy.tag.Mecab`을 사용할 수 없는 환경에서 `mecab_ko.Tagger`로 대체하는 fallback을 구현하고, 실제 형태소 분석 결과까지 검증했다.
    - 전역 `model`, `optimizer`, `history`를 사용하는 방식에서 발생할 수 있는 실험 간 상태 혼합과 체크포인트 덮어쓰기 문제를 확인하고, `run_experiment()` 내부에서 시드·모델·기록·체크포인트를 실행별로 분리했다.
    - 임베딩·은닉 차원을 키운 B 구성과 dropout 0.3 구성도 비교 실험했다. B는 train loss가 더 낮았지만 번역 품질이 악화되었고, dropout도 정성 평가상 개선되지 않아 A 구성을 채택한 판단이 기록되어 있다.
    - 학습 중 11번째 epoch에서 `KeyboardInterrupt`가 발생했지만, 10 epoch까지 저장된 `best.pt`와 `history`를 복구하여 최종 결과를 이어서 확인했다.
    - <img width="753" height="318" alt="image" src="https://github.com/user-attachments/assets/47fb1602-3316-427c-bde8-cfc93b51099c" />

        
- [x]  **4. 회고를 잘 작성했나요?**
    - 중복 제거 시 병렬 문장 쌍을 유지하는 방법, 데이터 노이즈를 실측 기반으로 제거한 과정, SentencePiece의 `character_coverage` 선택 근거를 회고에 기록했다.
    - 패딩을 Attention에 포함하면 확률 질량이 무의미한 위치로 분산되고 Encoder의 hidden state도 오염될 수 있다는 핵심 학습 내용을 구체적으로 설명했다.
    - 실행 플로우를 원본 데이터부터 전처리, 토큰화, 모델, 학습, 평가까지 ASCII 흐름도로 정리하여 전체 구조를 이해하기 쉽다.
    - 검증셋 부재, teacher forcing 100%와 greedy decoding으로 인한 반복, beam search·repetition penalty·scheduled sampling 미적용 등 한계도 솔직하게 제시했다.
    - <img width="1106" height="404" alt="image" src="https://github.com/user-attachments/assets/87ab3e7b-275e-42a0-8886-0f4c0b04799b" />

        
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 전처리, 토크나이저 확보, 모델 구성, 학습, 실험 실행, 번역 및 시각화 기능을 함수로 분리해 재사용성과 실험 편의성을 높였다.
    - 배치별 동적 패딩 절단, `pack_padded_sequence`, `CrossEntropyLoss(ignore_index=PAD_ID)`, gradient clipping을 적용하여 패딩과 학습 안정성을 고려했다.
    - 실행별 설정과 결과를 별도 경로에 저장하여 여러 모델 구성을 비교하기 쉽도록 구성했다.
    - 다만 한 epoch당 4개 예문을 매번 greedy decoding하고, 검증셋 없이 train loss와 정성 평가만으로 모델을 선택하므로 실행 시간이 길고 객관적인 일반화 평가는 제한적이다. 향후 validation loss와 BLEU 또는 SacreBLEU를 추가하면 효율성과 평가 신뢰도가 개선될 것이다.
    - <img width="775" height="319" alt="image" src="https://github.com/user-attachments/assets/5e533d63-f307-4205-b489-3bead40811f0" />



# 회고(참고 링크 및 코드 개선)
```
# 리뷰어의 회고를 작성합니다.
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

