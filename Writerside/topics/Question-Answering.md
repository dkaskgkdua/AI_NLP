# Question Answering(4)
질문을 입력받아 해당 질문에 대한 적절한 답변을 자동으로 생성하는 기술을 말한다.
시스템 구축을 위해서 필요한 소스는 아주 다양하다.(텍스트, 웹문서, 이미지 등)

* Question type으로 사실관계여부, 오픈도메인-클로즈드도메인 등이 있다.
* Answer type으로는 짧은 단어 답변, 문장, 리스트, 예/아니요 등이 있다.
* 구글에 질문하면 정리한 내용이나 이미지가 나오는 것과 같은 것이다.
* BERT와 같은 대부분의 최신 시스템들은 end-to-end 훈련이나 사전훈련 언어모델로 만들어진다.

시간이 흘러서는 text 뿐만이 아닌 다양한 모달을 결합하려는 시도가 있었다.(GPT처럼 통합되어간다...)

## Reading Comprehension(읽어서 이해 => 기계독해)
텍스트 내용을 읽고, 텍스트에 기반한 질문에 정확하게 답하는 AI 기술이다.

> SQuAD(Stanford Question Answering Dataset)은 Question Answering 시스템을 평가(표준 벤치마크)하고 학습시키기 위한 대규모 데이터셋이다.
> 10만개의 데이터셋이 있고 구성요소로 Passage(문서), Question(질문), Answer(정답)으로 이루어져 있다. 문서는 주로 위키피디아에서 가져온거고,
> 정답은 문서의 특정 부분에 존재하는 텍스트 스팬이다.
> 평가 지표로는 2가지가 있다.
> 1. EM(Exact Match): 생성한 답이 실제 정답과 정확히 일치하는지를 평가한다. 딱 들어맞아야 한다.
> 2. F1 : 모델의 답과 실제 정답이 얼마나 겹치는지를 평가하는 지표다. 겹치는 비율을 계산해 측정해서 좀 더 유연하다.
> <br>
> 그 외 dataset으로 TriviaQA, Natural Questions, HotpotQA 가 있다.


### 적용된 신경망 모델들
1. LSTM-based models with attention(2016~2018) : index만 맞추는 컨셉
2. Fine-tuning BERT-like models(2019+) : 사전 훈련으로 LSTM보다 잘된다.
3. 성능이 더 좋아진 SpanBERT도 있다.

### 그렇다면 Reading Comprehension은 완벽한가?
물론 아니다. 현재까지 소개된 시스템들도 여전히 다른 도메인 분야에서는 성능이 좋지 않다. 그리고 한 데이터셋으로 훈련된 건 다른 데이터셋으로 일반화할 수 없다.

## Open-Domain QA
Reading Comprehension과 차이점은 Passage(문서)가 없다고 생각한다. 대신 위키피디아 같은 거대한 문서덩어리에만 접근한다고 가정한다.
또한 답변도 어디에 있는지 모르며 목표는 어떤 질문이든 답하는 것이다. 훨씬 더 도전적이고 실용적인 문제다. closed-domain과는 대조적이다.

### Retriever-Reader Framework
기본적으로 Retriever가 위키피디아 같은 소스에서 유의미한 데이터를 찾고 Reader가 Reading Comprehension 역할을 하여 index를 찾아준다.
![Retriever_Reader.png](./images/QUestion Answering/Retriever_Reader.jpg)
* 각 텍스트 지문은 BERT를 이용하여 벡터로 인코딩할 수 있고, Retriever 점수는 질문과 문서의 내적으로 측정 가능하다.
* 하지만 문서가 많아 모델링하기가 쉽지는 않다.
* 대표적으로 DPR(Dense Passage Retrieval)이 있다. 딥러닝 기반으로 주어진 쿼리에 관련성이 높은 문서를 빠르고 정확하게 찾는데 장점이 있다.
Question과 Passage를 쌍으로 해서 벡터 간의 비슷한 공간에 있게 하여 학습을 시킴.

### Dense Retrieval + Generative Models (RAG의 초기 형태와 유사)
좀 더 일반화된 형태이고 성능도 괜찮았다. answer을 추출하는 방법이 아닌 생성하는 방식이다.

### GPT4(LLM based QA with Search)
최근은 질문을 하면 LLM이 스스로 검색을 하여 답변을 해준다. 물론 완벽하지는 않지만 어느정도는 괜찮다.
