# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 성명준
- 리뷰어 : 김영민


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
        - 중요! 해당 조건을 만족하는 부분을 캡쳐해 근거로 첨부
        - 한국어 데이터셋을 공백제거, 특수문자 제거, 소문자화 등을 통해 잘 전처리 되었습니다.
        - 트랜스포머 모델이 에포크에 따라 학습을 진행하며 개선되는 것을 잘 보여주고 있습니다.
        - 트랜스포머 모델이 한국어를 입력받아 한국어로 잘 대답하고 있습니다.
        ![ex0701](https://github.com/user-attachments/assets/a7b48ec8-8b0f-4477-9119-f10f5b21e36a)
        ![ex0702](https://github.com/user-attachments/assets/29f3e3eb-21c2-4acb-867f-642ba184b0c7)
        ![ex0703](https://github.com/user-attachments/assets/04500dd6-b009-4e65-b397-f47cbb2a028e)
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭을 왜 핵심적이라고 생각하는지 확인
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드의 기능, 존재 이유, 작동 원리 등을 기술했는지 확인
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - 마스크드 멀티헤드 어텐션과 드롭아웃등을 잘 사용해 모델이 잘 학습하도록 구성했고 주석이 꼼꼼히 작성되어 있습니다.
        ![ex0704](https://github.com/user-attachments/assets/2709c163-f0ce-476a-91cb-111715a5afec)
```
# 디코더 하나의 레이어를 함수로 구현.
# 이 하나의 레이어 안에는 세 개의 서브 레이어가 존재합니다.
def decoder_layer(units, d_model, num_heads, dropout, name="decoder_layer"):
  inputs = tf.keras.Input(shape=(None, d_model), name="inputs")
  enc_outputs = tf.keras.Input(shape=(None, d_model), name="encoder_outputs")
  look_ahead_mask = tf.keras.Input(
      shape=(1, None, None), name="look_ahead_mask")
  padding_mask = tf.keras.Input(shape=(1, 1, None), name='padding_mask')

  # 첫 번째 서브 레이어 : 멀티 헤드 어텐션 수행 (셀프 어텐션)
  attention1 = MultiHeadAttention(
      d_model, num_heads, name="attention_1")(inputs={
          'query': inputs,
          'key': inputs,
          'value': inputs,
          'mask': look_ahead_mask
      })

  # 멀티 헤드 어텐션의 결과는 LayerNormalization이라는 훈련을 돕는 테크닉을 수행
  attention1 = tf.keras.layers.LayerNormalization(
      epsilon=1e-6)(attention1 + inputs)

  # 두 번째 서브 레이어 : 마스크드 멀티 헤드 어텐션 수행 (인코더-디코더 어텐션)
  attention2 = MultiHeadAttention(
      d_model, num_heads, name="attention_2")(inputs={
          'query': attention1,
          'key': enc_outputs,
          'value': enc_outputs,
          'mask': padding_mask
      })

  # 마스크드 멀티 헤드 어텐션의 결과는
  # Dropout과 LayerNormalization이라는 훈련을 돕는 테크닉을 수행
  attention2 = tf.keras.layers.Dropout(rate=dropout)(attention2)
  attention2 = tf.keras.layers.LayerNormalization(
      epsilon=1e-6)(attention2 + attention1)

  # 세 번째 서브 레이어 : 2개의 완전연결층
  outputs = tf.keras.layers.Dense(units=units, activation='relu')(attention2)
  outputs = tf.keras.layers.Dense(units=d_model)(outputs)

  # 완전연결층의 결과는 Dropout과 LayerNormalization 수행
  outputs = tf.keras.layers.Dropout(rate=dropout)(outputs)
  outputs = tf.keras.layers.LayerNormalization(
      epsilon=1e-6)(outputs + attention2)

  return tf.keras.Model(
      inputs=[inputs, enc_outputs, look_ahead_mask, padding_mask],
      outputs=outputs,
      name=name)
```
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 프로젝트 평가 기준에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - 더 작은 모델을 직접 만들어 실행해 보는등 다양한 시도가 있었습니다.
        ![ex0705](https://github.com/user-attachments/assets/3665af7d-70fc-48a6-90cf-3b7ccac6dde8)
        
- [x]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - 블루 스코어 등 측정할 다양한 부분을 회고를 통해 고려하였음
        - validation셋을 사용해서 loss를 측정한 것 등 다양한 시도들에 대한 후기 및 보완점이 잘 담겨 있음
        ![ex0706](https://github.com/user-attachments/assets/145569ca-142d-44e4-a116-3fabdf7b39ec)
        
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화/모듈화했는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - 더 작은 모델 부분을 파일을 따로 빼서 간결하게 실행할 수 있고 복잡한 부분들도 모두 주석처리가 잘 되어있어서 가독성이 좋고 효율적인 코드를 구성함
        ![ex0707](https://github.com/user-attachments/assets/cd050fac-9fe4-43bf-a10b-db373f771c50)


# 회고(참고 링크 및 코드 개선)
```
# 리뷰어의 회고를 작성합니다.
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
- 더 작은 모델을 만들어 실험해본것이 인상적이었습니다.
- 모델에 다양한것을 추가하여 결과가 다양하게 나온 부분이 인상적이었습니다.
- 데이터셋이 많이 작고 단순했는데 어느정도 대화가 가능한 챗봇을 구성했다는 부분이 인상깊었습니다.