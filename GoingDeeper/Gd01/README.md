# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 성명준
- 리뷰어 : 박세희


# PRT(Peer Review Template)
- [V]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
        - 중요! 해당 조건을 만족하는 부분을 캡쳐해 근거로 첨부
        - 전처리, corpus 분석, 토크나이저 구현 등 전과정 정상적으로 수행됨
        - SP 토큰 사용 시, Accuracy level 84.64%로 평가 기준 80%을 넘음
        - SentencePiece의 Vocab 사이즈를 변경하거나, 다양한 형태소 분석기를 사용하는 등 다각화하여 실험이 수행됨
          <img width="793" alt="image" src="https://github.com/user-attachments/assets/0d46b438-d353-4692-90fd-6952c9439406" />
          <img width="804" alt="image" src="https://github.com/user-attachments/assets/e6a58a80-ee42-4bff-ad8f-94c59d02df44" />

    
- [V]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭을 왜 핵심적이라고 생각하는지 확인
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드의 기능, 존재 이유, 작동 원리 등을 기술했는지 확인
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - docstring을 통해 형태소 분석기별 로드 시간 비교 내용을 확인할 수 있음
          <img width="807" alt="image" src="https://github.com/user-attachments/assets/7400644f-8ead-43e9-a729-9816d36dae8a" />

        
- [V]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 프로젝트 평가 기준에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - SentencePiece 외, Mecab, Komoran, Okt 등 다양한 형태소 분석기로 모델 성능을 평가함
        - ![image](https://github.com/user-attachments/assets/97d19763-802e-4e54-a0f3-d5f449809e8c)

        
- [V]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - vocab_size를 변경하며 실험한 부분에 대해 고민한 부분이 잘 느껴집니다!
        <img width="777" alt="image" src="https://github.com/user-attachments/assets/be4ab638-18db-4973-80d1-607245137a49" />
        - 형태소 분석기의 정확도가 낮은 이유에 대한 분석을 확인할 수 있었습니다.
        - <img width="780" alt="image" src="https://github.com/user-attachments/assets/90ee20d0-20e5-4ba4-ba50-08b7bab0cda5" />


        
- [V]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화/모듈화했는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        - 특정 길이 문장을 찾는 함수를 정의하고 다양한 분포의 문장 길이에 대한 개수를 파악함
        - <img width="782" alt="image" src="https://github.com/user-attachments/assets/22761eaf-8c75-485d-b24a-7705f15f1244" />
        - <img width="870" alt="image" src="https://github.com/user-attachments/assets/e1c5d91e-1a90-4bc9-a383-2b5af2a1f882" />




# 회고(참고 링크 및 코드 개선)
```
# 리뷰어의 회고를 작성합니다.
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
짧은 시간 내에 다양한 형태소 분석기 사용 + SentencePiece vocab_size 변경을 하며 다양한 실험을 해내신게 대단하신 것 같습니다!
명준님의 회고 내용을 보면서 데이터에 대해 좀 더 잘 이해할 수 있는 시간이었고, 형태소 분석기 vs SP 토크나이저의 성능 차이에 대해 분석하신 내용이 인상깊었습니다. 😁
