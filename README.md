# DL_ML-Recommendation-System-Speech-Data

# <u>음성 상담 데이터 분석 및 추천 시스템</u>

## [<u>Introduction</u>]

- 사실적이고 직접적인 인사이트를 낼 수 있는 것이 무엇이 있을까 생각하였고 현실적으로 많은 곳에서 음성으로 상담을 하고 그것을 녹음하는 경우를 생각해 보았습니다. 

- 음성 데이터를 텍스트로 변환하고 텍스트로 변환된 데이터를 분석하여 고객들의 피드백을 반영한다.

- 음성 상담 데이터들을 활용해 분석을 하여 사람들의 직접적인 피드백을 반영한다면 좀더 빠르고 정확하게 문제들을 해결할 수 있지 않을까 생각하게 되었습니다. 

- 또한 그 사용처가 기업이라면 고객들의 불만사항이나 요구사항을 반영하여 이익을 낼 수 있는 방향으로 더 나아갈 수 있을 것이라 생각했습니다.

## [<u>DATA</u>]

![image](https://user-images.githubusercontent.com/89772868/162251817-b623884b-2f26-45c8-b213-f84c13f14c69.png)

- 사용 데이터로는 AI Hub의 상담 음성데이터를 선정.

- 해당 데이터는 교육, 금융, 통신판매 도메인의 음성 데이터로 사람들에게 많은 이슈에 해당할  수 있는 도메인을 포함 하여 데이터를 선정.
 
- 데이터는 총 3000시간이라는 많은 양의 시간이고 음원 데이터와 그에 해당하는 텍스트 데이터로 나누어져 있어  효과적으로 모델을 구축할 수 있을 것.

## [<u>hypothesis</u>]

- 상담 음성 데이터를 음성인식 모델을 구축하여 모델을 통해 높은 정확도로 텍스트화할 수 있을 것이다.

- 텍스트화 한 데이터를 감정 분류 모델을 통해 긍정적인 측면과 부정적인 측면으로 분류할 수 있을 것이다.

- 긍정과 부정으로 분류 된 데이터를 분석하여 해당 데이터를 활용할 수 있는 집단에서 직접적인 피드백으로 사용하여 이슈화 되고 있는 것들을 개선하여 좋은 서비스와 이익을 창출할 수 있을 것이다.

- 데이터를 분석한 결과로 상품을 추천할 수 있는 시스템을 만들 수 있을 것이다.


## [<u>Project process</u>]

- 사전 학습 음성인식 모델인 wav2vec2를 활용하고 fine-tuning을 진행하여 한국어 음성인식 모델을 구축한다. 

- 한국어 음성인식 모델을 활용하여 텍스화된 음성데이터를 감정 분류 모델을 통해 긍정과 부정적인 측면으로 라벨링 한다.

- 라벨링 된 텍스트 데이터를 분석하여 인사이트를 도출한다.

- 데이터를 분석한 결과로 추천 시스템을 구축한다.


## [<u>wav2vec2</u>]
![image](https://user-images.githubusercontent.com/89772868/162252397-e7d8ed13-cfc7-4c11-91c0-5bfb38d214b3.png)

- Wav2Vec2는 Bert와 비슷한 사전학습 모델로 음성의 특징을 추출하는 CNN 계 층을 이용해 스펙트로그램과 같은 기존 음성 특징 추출기법을 사용하지 않고 원본 음성 파일을 입력으로 사용할 수 있다. 이 후 Transformer  인코더 구조를 이용해 음성 특징을 인코딩하여 CTC Projection 계층을 통해 인식 결과를 출력한다. Wav2Vec2는 전사정보가 없는(Unlabeled) 음성파일을 이용 해 Self-Supervised Learning 을 통한 사전학습이 가능하다.


## [<u>모델 선정 이유</u>]
![image](https://user-images.githubusercontent.com/89772868/162252588-595bf1f1-c3cc-4ccd-b67c-b9e01466edbd.png)

- 사전학습 된 wav2vec2를 활용하여 라벨링된 데이터를 fine-tuning 한 결과 음성인식에 대해 좋은 결과를 낼 수 있다는 점을 설명한 자료로 한국어로도 우수한 성능을 낼 수 있을 것이라 생각하여 결정하게 되었습니다.

- Wav2vec2에 라벨링된 데이터를 10분 정도만 훈련시켜도 높은 성능 나타내는 것을 볼 수 있습니다. 

## [<u>preprocessing</u>]

![image](https://user-images.githubusercontent.com/89772868/162252802-97491e88-02fb-4279-882e-0ec62906475f.png)

- 총 데이터의 개수는 17198개를 활용

- 그림과 같이 다른 이름의 폴더에 같은 이름의 파일들을 전처리 하여 진행 하였습니다. 

---

![image](https://user-images.githubusercontent.com/89772868/162253003-72ea44d5-bac7-4a9c-8756-cfc570fe06e9.png)

- 위의 그림과 같이 라벨링된 음원 데이터와 텍스트를 같은 이름의 키 값으로 맞춰준다.

- 같은 키 값으로 맞춘 음원과 텍스트 데이터를 mapping하고 음원 데이터는 함수를 사용하여 배열로 변환한다. 

---

![image](https://user-images.githubusercontent.com/89772868/162253155-2254babc-c65f-4b34-b5e0-da4b8a2c4ca5.png)

- 텍스트 문장을 전처리 하여 vocab.json 파일을 만들어 추후 모델 구축에 사용할 Wav2Vec2CTCTokenizer의 Tokenizer로 활용한다. 


## [<u>모델 구축</u>]

![image](https://user-images.githubusercontent.com/89772868/162253365-3d3c7718-b64e-4715-819b-b17626c482ab.png)

- 전체적으로 fine-tuning을 위해 Wav2Vec2 구조 위에 한 층을 쌓고 그 위에 CTC 와 인코딩으로 Spec-Agument 사용하는 구조로 모델을 구축 합니다.

- 모델의 BATCH SIZE는 2, epochs는 50, LEARNING_RATE는 5e-5(0.00005), CTCLoss의 optimizer는 adam을 사용 하였습니다. 

- 텍스트 데이터의 최대길이는 256, 음원의 최대길이는 246000으로 정하였습니다. 

## [<u>감정 모델 구축</u>]

![image](https://user-images.githubusercontent.com/89772868/162253643-9151a307-a109-41bf-8101-b0537f871afe.png)

- 감정 분류 모델은 긍정과 부정으로 라벨링된 데이터를 활용하여 감정 분류 모델을 구축하였습니다.

- 구축한 감정 모델을 통해 음성인식 모델을 통한 텍스트화 된 데이터(가정)의 감정 분류를 하여 라벨링 하였습니다.


## [<u>데이터 분석</u>]

- 음성인식 모델을 통해 텍스트화 된 데이터(가정)를 전처리 하기 위해 불용어(stop_words)를 txt파일로 만들어 가져온다. (불용는 해당 사이트를 이용하여 만들었습니다. https://www.ranks.nl/stopwords/Korean)

- 감정 분류를 통해 라벨링된 텍스트 데이터를 긍정과 부정적인 측면으로 전처리 한다.

- 불용어를 활용하여 텍스트를 전처리하여 리스트 형태로 만든다.

- 전처리된 텍스트를 시각적으로 표현하여 인사이트를 도출합니다.

---

![image](https://user-images.githubusercontent.com/89772868/162253912-0abb1bc7-2a67-47a7-ab9e-816f04e3ac91.png)


- 감정 분류된 텍스트 데이터를 시각화하여 살펴 보면 긍정적인 측면(1.0)이 부정적인 측면(0.0)보다 많은 것을 확인할 수 있습니다. 

- 이는 고객들이 상담에 대부분 만족하는 결과를 볼 수 있습니다.

## [<u>데이터 분석 시각화</u>]
![image](https://user-images.githubusercontent.com/89772868/162254076-58285a20-db76-44a4-9bce-941a9d1b57d9.png)

- 부정적인 데이터의 시각화를 살펴보면 카드와 카드의 한도, 기간에 대한 단어들이 자주 나오는 것을 볼 수 있습니다. 이는 고객들이 카드의 한도와 기간에 대한 부정적인 이슈가 많은 것을 확인 할 수 있습니다. 또한 다른것으로 기업에서의 정보확인을 부정적인 측면으로 볼 수 있는 것을 확인할 수 있습니다.

- 긍적적인 데이터의 시각화를 살펴보면 쉐어링 은행과 쉐어링 카드를 볼 수 있습니다. 이는 쉐어링 증권, 은행, 카드에 대한 만족도를 확인해 볼 수 있습니다. 


## [<u>추천 시스템 구축</u>]
![image](https://user-images.githubusercontent.com/89772868/162254193-215bfe5e-b706-4e19-a627-023eaade9376.png)

- 전처리된 데이터를 sklearn에서 제공하는 TfidfVectorizer를 사용하여 텍스트 데이터를 수치 자료형 벡터로 변환하여 추천 시스템을 위한 전처리를 수행한다.

- 데이터를 train과 validation으로 나누어 머신러닝 모델에 학습한다. 기본 분류 모델은 의사결정나무를 사용한다.

- 여러 모델을 사용하여 테스트한 후 가장 우수한 성능의 XGB모델을 사용한다.

## [<u>Feature Importance</u>]

![image](https://user-images.githubusercontent.com/89772868/162254333-7270bf38-e24f-48c4-8a31-51694ccd040a.png)

- XGB 모델의 변수 중요도를 출력하여 시각화

---

![image](https://user-images.githubusercontent.com/89772868/162254688-81af9270-9015-4468-86d7-261c02e20af3.png)

- XGBClassifier 모델에서 feature importance가 30번째인 토큰을 문자열 형태로 시각화하면 다음과 같이 나타난다.

- 시각화한 결과를 보면 쉐어링 ,카드, 포인트, 증권계좌의 상품에 집중하여 정확한 서비스를 제공한다면 고객들의 피드백에 만족할 만한 결과를 도출할 수 있을 것을 예상합니다.

- 또한 한도와 할부에 관한 자세한 설명과 보기 쉬운 서비스를 제공한다면 고객들의 만족도가 올라갈 수 있을 것이라 예상한다. 

## [<u>References</u>]
- https://tensorflow.google.cn/hub/tutorials/wav2vec2_saved_model_finetuning

- https://www.youtube.com/watch?v=Pw9BUgCf6a8

- https://huggingface.co/blog/fine-tune-xlsr-wav2vec2

- https://smilegate.ai/2020/08/05/wav2vec-2/

- https://github.com/vasudevgupta7/gsoc-wav2vec2

- https://huggingface.co/


