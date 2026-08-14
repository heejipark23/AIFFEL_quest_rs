# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희지
- 리뷰어 : 김나연


# PRT(Peer Review Template)
- [X]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 정제단계, 정규화와 불용어 제거, 데이터셋 분리, 인코딩 과정이 빠짐없이 체계적으로 진행되었다.
        - <img width="1502" height="752" alt="image" src="https://github.com/user-attachments/assets/197d6fc4-b3b7-4045-b9c7-dfc6c8736a6c" />
        - <img width="675" height="755" alt="image" src="https://github.com/user-attachments/assets/085cdb8a-231a-46ee-8f2a-dd5aff53faa2" />
        - <img width="929" height="749" alt="image" src="https://github.com/user-attachments/assets/617c1f7a-4138-4a9a-8f95-54a62bfaa835" />
    - 모델 학습이 진행되면서 train loss와 validation loss가 감소하는 경향을 그래프를 통해 확인했으며, 실제 요약문에 있는 핵심 단어들이 요약 문장 안에 포함되었다.
        - <img width="820" height="749" alt="image" src="https://github.com/user-attachments/assets/26e0639d-c002-47ac-ad30-65962c6729e5" />
        - <img width="1699" height="740" alt="image" src="https://github.com/user-attachments/assets/9cfb638f-f333-4208-b40b-5bbbbd10572e" />
    - 추상적 요약과 추출적 요약 두 가지를 문법완성도 측면과 핵심단어 포함 측면으로 나누어 비교하고 분석 결과를 표로 정리하여 제시하였다.
        - <img width="1694" height="746" alt="image" src="https://github.com/user-attachments/assets/359a0f6a-4b08-4c46-895f-5922c0147270" />

- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - Encoder -> Decoder -> Attention 이라는 전체 흐름을 도식도를 이용해 이해를 돕고 있다.
        - <img width="641" height="742" alt="image" src="https://github.com/user-attachments/assets/59631dec-26b9-4e54-9597-fb64b2f1d837" />
        
- [X]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - num_layer = 3 -> 2 번경, train / val / test 70/10/20 -> 80/10/10 등의 추가적인 실험을 수행하였다.
        - <img width="1023" height="745" alt="image" src="https://github.com/user-attachments/assets/f00a0751-39ac-4262-90a6-5b745c486ccb" />
        - <img width="1039" height="737" alt="image" src="https://github.com/user-attachments/assets/b9dae26b-916d-47b0-ba34-6cadca94800d" />

- [X]  **4. 회고를 잘 작성했나요?**
    - <img width="1678" height="307" alt="image" src="https://github.com/user-attachments/assets/11bd14cd-bd18-4d17-8741-b91d977e2b97" />

- [X]  **5. 코드가 간결하고 효율적인가요?**
    - vocab 생성, 패딩, Encoder, Decoder, Attention, Seq2SeqWithAttention 으로 모듈화와 함수화를 적절히 수행하였다.
        - <img width="952" height="741" alt="image" src="https://github.com/user-attachments/assets/4265b46b-6bc7-4beb-a885-895cfc98018f" />



# 회고(참고 링크 및 코드 개선)
```
# 전체 text 데이터에 대한 전처리
from tqdm import tqdm
clean_text = []

for sentence in tqdm(data['text']):
    clean_text.append(preprocess_sentence(sentence))

# 전처리 후 출력
print("Text 전처리 후 결과: ", clean_text[:5])
```
저 같은 경우에는 위 코드에서 append 함수 대신에 apply 함수를 이용하니 더 빠르게 진행이 되어서 다음에 코드 작성하실 때 희지님도 한 번 참고 해보시면 좋을 것 같습니다.
아래에 제가 작성한 코드 첨부 해두겠습니다.
```
# Train
train['text'] = train['text'].apply(preprocess_sentence)
train['headlines'] = train['headlines'].apply(lambda x: preprocess_sentence(x, remove_stopwords=False))


# Validation
val['text'] = val['text'].apply(preprocess_sentence)
val['headlines'] = val['headlines'].apply(lambda x: preprocess_sentence(x, remove_stopwords=False))


# Test
test['text'] = test['text'].apply(preprocess_sentence)
test['headlines'] = test['headlines'].apply(lambda x: preprocess_sentence(x, remove_stopwords=False))
```
