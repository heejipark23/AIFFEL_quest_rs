# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박희지
- 리뷰어 : 이민서


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**

    <img width="655" height="614" alt="image" src="https://github.com/user-attachments/assets/f1e76ed5-a15e-46ab-9987-18b7daf6e4fe" />

    입력 이미지 경로를 받아 사람 또는 일정 크기 이상의 차량이 탐지되면 Stop, 그렇지 않으면 Go를 반환하는 자율주행 보조 함수를 구현했습니다. COCO 사전학습 RetinaNet과 직접 학습한 KITTI RetinaNet을 각각 적용해 비교했고, 직접 학습한 모델이 10개 테스트 이미지에서 90점을 기록하여 요구된 정확도 기준을 충족했습니다.


- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**

    <img width="1161" height="227" alt="image" src="https://github.com/user-attachments/assets/7d6179d8-2619-40dc-a925-530eb2d0fc45" />

    self_drive_assist_kitti() 함수는 직접 학습한 KITTI RetinaNet의 탐지 결과를 자율주행 보조 규칙으로 변환하는 핵심 코드입니다. 함수 docstring에 사람 탐지 시 정지, 차량의 가로 또는 세로 길이가 300px 이상이면 정지한다는 판정 기준이 명확히 작성되어 있어 코드의 목적과 작동 방식을 이해하기 좋았습니다.
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**

    <img width="1257" height="144" alt="image" src="https://github.com/user-attachments/assets/b99183f3-a479-4c2b-900d-e4d7b929de25" />

    COCO 사전학습 모델과 직접 학습한 KITTI 모델을 동일한 규칙과 테스트셋에서 비교하는 추가 실험을 수행했습니다. 그 결과 KITTI 모델은 80점에서 90점으로 향상되었으며, go_3.png의 COCO 모델 오정지와 stop_3.png의 미정지 원인을 탐지 결과와 bounding box 크기를 근거로 구체적으로 분석했습니다.
        
- [x]  **4. 회고를 잘 작성했나요?**

    <img width="1248" height="202" alt="image" src="https://github.com/user-attachments/assets/5072db95-aa0e-49bd-9783-696b13e332fb" />

    COCO 사전학습 모델보다 KITTI 도로 주행 데이터로 직접 학습한 모델이 같은 조건에서 더 높은 성능을 보였고, 이는 도메인 적합성이 중요하다는 점을 보여 주었습니다. 또한 stop_3.png 사례를 통해 bounding box의 화면상 크기만으로 실제 차량의 위험도를 판단하는 규칙에는 한계가 있음을 확인했습니다.
        
- [x]  **5. 코드가 간결하고 효율적인가요?**
      
    <img width="854" height="321" alt="image" src="https://github.com/user-attachments/assets/13399d5b-1355-46a1-a235-4f67529c49f1" />

    self_drive_assist_kitti() 함수는 이미지 로드, 객체 탐지, 위험 조건 확인, Stop 또는 Go 반환 과정을 간결하게 구성했습니다. 특히 기존 COCO 모델의 판정 규칙을 유지한 채 모델과 클래스 체계만 KITTI에 맞게 교체하여, 공정한 모델 비교 실험이 가능하도록 작성한 점이 좋았습니다.


# 회고(참고 링크 및 코드 개선)
```
이번 리뷰를 통해 자율주행 보조 시스템에서는 객체 탐지 모델의 정확도뿐 아니라, 탐지 결과를 Stop과 Go로 변환하는 판정 규칙이 최종 성능에 큰 영향을 준다는 점을 확인했다. 동일한 사람 탐지 및 차량 크기 300px 기준을 유지한 상태에서 COCO 사전학습 RetinaNet과 직접 학습한 KITTI RetinaNet을 비교한 결과, KITTI 모델이 80점에서 90점으로 향상된 점이 인상적이었다.

특히 go_3.png에서 COCO 모델은 원거리의 작은 보행자를 탐지해 불필요하게 Stop을 반환했지만, KITTI 모델은 이를 탐지하지 않아 정답인 Go를 반환했다. 반면 stop_3.png는 두 모델 모두 차량 bounding box의 화면상 크기가 300px에 미치지 않아 Go를 반환했다. 이를 통해 모델 성능만 개선하는 것보다, 화면에 잘린 차량이나 실제 거리 정보를 고려할 수 있도록 차량 크기 기반 규칙을 보완하는 것이 필요하다고 생각했다.

코드 측면에서는 COCO와 KITTI의 클래스 체계를 분리하고, 동일한 test_system()으로 두 모델을 평가하여 비교 조건을 통제한 점이 좋았다. 앞으로는 NMS가 적용된 예측 이미지 시각화, mAP·precision·recall 같은 객체 탐지 지표, 거리 또는 프레임 경계 정보를 반영한 위험 판단 규칙을 추가하면 더 신뢰도 높은 자율주행 보조 시스템으로 발전할 수 있을 것이다.
```

