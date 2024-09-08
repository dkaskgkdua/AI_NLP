# Natural Language Processing

## NLP란 무엇인가? {id="nlp_1"}
- 자연어처리는(NLP)는 자연어를 통한 컴퓨터와 인간의 상호작용에 초점을 맞춘 인공지능 분야이다.
- 궁극적인 목적은 인간의 언어를 이해하고 해석하며 생성하는 것이다.

### NLP의 카테고리 {id="nlp_1_1"}
- Natural Language Understanding(NLU): 텍스트에 대한 깊은 이해가 필요한 문제를 해결한다.
  ( Encoder / 선제적인 연구 필요 / ex. 감정연구, 추천)
- Natural Language Generation(NLG): 우리와 대화하는 시스템을 개발(챗봇, 기계번역, 요약 등)
  ( Decoder / 사람처럼 된지 얼마 안됨)

### NLP의 도전과제 {id="nlp_1_2"}
자연어는 규칙적이면서도 불규칙적이다. 맥락에 기반한 의미와 밈이나 신조어 같은 언어들도 있다.
언어학, 통계학, 심리학 등 많은 학문과의 관련성도 존재한다.(고로 쉽지 않다.)


### Word Vector {id="nlp_1_3"}
#### 철학
"Distributional semantics"<br/>
실제 데이터 상에서 단어가 유사한곳에서 많이 나타나면 벡터로 나타냈을 떄 벡터공간에 비슷한 곳에서 나타나야 한다.(근묵자흑)
#### 변환 방법
단어가 언어를 다루는 방법은 아래와 같다.
- 컴퓨터는 숫자만 처리가 가능해서, 자연어를 숫자 형태(벡터)로 변환해야 한다.
- 자연어의 기본 단위는 Word이다. 문장, 단락, 문서와 같은 개념을 구축하기 위해 다른 단어들을 결합한다.

![Word 분포도](word_poisition.png){ width=290 }{border-effect=line}

#### 변환 방법들
1. 정수 인코딩(Integer Encoding)
주어진 단어들에 번호를 각각 고유하게 부여한다. 연관성 파악이 어렵다.

2. One Hot Encoding
벡터 차원에서 단어에 숫자를 부여한다. Sparse Vector라고도 불리며 메모리 부족, 연관성 파악 어려움이 있다.
ex) motel = [0 0 0 0 1 0 0]
   hotel = [0 0 0 0 0 0 1]
<br/>
```  만약 Seoul motel을 검색하면 Seoul hotel도 나오길 기대하지만 유사함을 유추하기가 어렵다. 두 벡터는 수직이다.(orthogonal)```

3. Dense Word Vectors
각 단어를 dense vector로 만들고, 유사한 맥락에서 나타나는 단어들의 벡터와 유사하도록 한다.
![Dense Vector](dense_vector.png){ width=290 }{border-effect=line}

#### Word2Vec
Word2vec은 Word Vector를 학습시키기 위한 프레임워크이다.
변환 과정은 아래와 같다.
1. 말뭉치로부터 각 단어들을 고차원 실수 벡터로 변환합니다.
(자연어 처리용 단어 임베딩 생성)

2. center word와 context word의 벡터값 연산을 통해 단어들간의 의미가 유사한지 확인합니다.
(의미적 관계, 유사도 파악)
3. 확률을 최대화하기 위해 단어 벡터를 조정합니다.

즉, `말뭉치의 근접성(Data likelihood)`을 `word vector의 유사도(Dot Product)`와 연결한다!

1. Data likelihood(사건이 일어날 확률)
   ![likelihood1](likelihood1.png){ width=350 }{border-effect=line}
풀이
   ![likelihood2](likelihood2.png){border-effect=line}
   ![likelihood2](likelihood3.png){border-effect=line}
   ![vector1](vector1.png){border-effect=line}
2. More details
- CBOW, Skip-gram 모델이 있는데 window 크기를 기준으로 CBOW는 context word로부터 center word를 예측합니다. 반면 Skip-gram은 center word로부터 context word를 예측합니다.
Skip-gram이 상대적으로 느리지만 더 다양한 학습을할 수 있어 효과적입니다.(위 정리 기준도 skip-gram)
- 손실함수를 최소화하기 위해 경사하강법 알고리즘이 사용됨. 최소한 local minimum이라도 찾자.

#### Word Vector에 대한 평가는 어떻게 하는가?
이론적으로 만들어진 것을 평가하는건 평가하기도 어렵다. 실생활에 얼마나 도움이 되는가로 평가한다. 혹은 성능적인 개선?
약간 개발 테스트에서 단위테스트인지 통합테스트인지 차이인듯.
1. 내재적 평가: 특정/중간 하위 작업에 대한 평가
- 특정/중간 하위 작업에 대한 평가
- 계산이 빠르다.
- 그 시스템을 이해하는데 도움이 된다.
- 실생활에 도움이 되는 상관관계가 확립되지 않는 한 정말 도움이 되는지 모른다.
2. 외재적 평가
- 실제 작업에 대한 평가.
- 정확도를 계산하는데 오래 걸릴 수 있다.
- subsystem이 문제인지 상호작용이 문제인지 알 수가 없다.




------------------------------------------------------------------------------------------------------

What is the definition of language modeling?
Describe at least two cases where language models can be utilized.
언어 모델링의 정의는 무엇입니까?
언어 모델을 활용할 수 있는 사례를 최소한 두 가지 이상 설명하세요.

언어 모델링은 다음에 어떤 단어가 올지 예측하는 작업입니다.

Data-Driven Approach 기법을 사용하기에 학습된 도메인 내용에 따라 관련 용어가 나올 수 있습니다.

공식처럼 나타낸다면 P(x^(t+1) | x^t, ... , x^1) 입니다.




언어 모델링의 활용 사례는 실생활에 정말 많이 찾아볼 수 있습니다.

- 문자 자동완성, 교정(구글 검색, 스마트폰 키보드)

- Chatbot System(Chatgpt, Claude, Gemini 등..)

- 음성 인식(음성 신호 -> 텍스트 변환 시 자연스러운 순서 예측)

- 번역

---------------------------------------------------------------------------
What are the strong points of RNN-based language models
compared to n-gram and feed-forward network-based language models?
n-gram 및 피드포워드 네트워크 기반 언어 모델과 비교하여 RNN 기반 언어 모델의 장점은 무엇입니까?

n-gram과 feed-forward network 기반 언어 모델에 비해 RNN 기반 언어의 강점은 아래와 같습니다.

1. Ablility to process long sequences 

RNN은 순환 구조를 가지고 있습니다. 이전 상태의 정보를 현재 상태에 반영할 수 있는데 n-gram의 경우 고정된 크기의 문맥만 고려하기 때문에, 긴 문맥에서의 정보 상실이 발생합니다.

2. Dynamic context handling

RNN은 문장의 길이 따라 동적으로 문맥을 업데이트할 수 있습니다. 반면 feed-forward network는 고정된 입력 길이만 처리 가능하여 유연하게 대처가 안됩니다.

3. Efficiency in number of parameters

n-gram 모델은 고정된 n개의 단어에 대해 학습하고 크기가 거질수록 파라미터 수가 기하급수적으로 증가하지만 .RNN의 경우 같은 파라미터를 반복적으로 사용하므로 효율적인 학습이 가능합니다.

--------------------------------------------------------------------------------------------------------------------------
Explain the several variants of RNNs. Maybe you can introduce upgraded architectures,
the way of better using RNNs, etc.
RNN의 여러 변형을 설명하세요. 아마도 업그레이드된 아키텍처, RNN을 더 잘 사용하는 방법 등을 도입할 수 있을 것입니다

RNN의 변형 케이스들은 아래와 같습니다.

1. LSTM(Long Short Term Memory)

LSTM은 장기의존성(long-term dependencies) 문제를 해결하기 위해 설계되었습니다. 기본 RNN은 짧은 시퀀스에서만 효과적이고, 긴 시퀀스를 처리할 때는 기울기 소실 문제(vanishing gradient problem) 때문에 학습이 잘 되지 않는 문제가 있었습니다.  이러한 문제를 해결하기 위해 memory cell과 gates 개념을 도입하여 정보를 선택적으로 기억하거나 잊는 구조로 동작합니다.

- input gate : 새로운 정보를 얼마나 받아들일지

- forget gate : 이전 정보를 얼마나 잊을지

- output gate : 현재 상태에서 어떤 정보를 출력으로 내보낼지

- cell state: 정보를 저장하는 장기 기억 역할
