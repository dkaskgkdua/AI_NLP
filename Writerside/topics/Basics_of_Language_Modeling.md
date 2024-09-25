# Language Modeling
언어 모델링은 다음에 어떤 단어가 올지 예측하는 작업이다.
(context가 있을 때 다음에 나오는 단어를 종합적으로 고려하여 예측)<br>


- DDA(Data Driven Approach) 기반이기 때문에 정답이 되는 데이터를 가지고 있다.
- 특정 도메인을 학습시키면 해당 도메인의 관련 용어가 많이 나온다.
- 공식(formal)으로 접근하면 아래와 같다.(words sequence가 주어지면 다음 단어의 확률분포를 계산)
![language_model_formal.png](language_model_formal.png)
- 공식에 대한 예시로서 어떤 문장이 완성되는 확률을 표현하면 아래와 같다.
![language_model_formal2.png](language_model_formal2.png)
- 예시로 문자 자동완성, 교정(구글 검색, 스마트폰 키보드), Chatbot System(gpt, claude, gemini), 음성 인식, 번역이 있다.

## N-gram Language Models
N-gram 언어 모델은 LM을 구현하는 기본적이고 고전적인 방법이다.<br>
n은 context length를 의미한다.

- 종류는 Unigrams(1개), Bigrams(2개), Trigrams(3개), Four-grams(4개)가 있다.
- 수학적 표현으로 Markov 가정으로 쓰며 아래와 같다.
![Markov_assumption.png](Markov_assumption.png)
- 4개를 기준으로 확률을 어떻게 구하는지 알아보자.
>1. 문장에서 4개를 제외한 부분은 날리고, 아래와 같이 카운팅한다.
>![ngram_example.png](ngram_example.png)
>2. 분모가 100, 분자가 5라고 가정하면, 지금까지 학습한 데이터에서 분모는 100번, 분자는 5번 나왔다는 뜻이다.
>3. 그렇게 w가 나올 확률(P)은 0.05가 되며 확률이 가장 높은 단어가 예측된다.
>4. **한계**는 길이에 제한이 있어 앞에 내용을 날려서 추론이 어려워지고 비합리적인 결과가 나올 가능성이 있다.
>5. 길이를 늘리게 되면 희소성 문제가 악화되고 모델 크기가 늘어난다.


## Fixed-window Neural Language model
신경망을 이용해 단어 임베딩 벡터의 의미적 관계를 학습하며, **희소성 문제를 극복**할 수 있지만 **고정된 길이의 한계**가 있다.

## RNN
