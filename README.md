# 게이미피케이션을 활용한 주가예측 기반의 종목 위험도 평가와 고객 군집화 및 수익률 랭킹 서비스

### 서비스 개요
본 팀의 서비스는 주식 시장에 본격적으로 입문하고 싶지만 주식에 대한 어려움을 느끼는 일명 '주린이' 고객들을 주요 대상으로 합니다. 메인 서비스는 <위험도 예측>, <고객군집화>이며, 이 서비스들을 활성화하기 위한 방안으로 게이미피케이션을 고안하였습니다.

자동화 코드는 유튜브 및 네이버의 API 제한과 시간이 오래걸린다는 단점이 있어 전처리과정부터 모델링과정까지만 넣어놨습니다. 원하시면 코드에 들어가셔서 수집과정부터 확인 가능합니다.

----API  소개 ----

### 팀 소개
<p>팀명 : 끼리끼리</p>
<p>프로젝트 기간 : 2023/7/1 ~ 2023/09/13</p>

|    소속    |          전공           |  이름  |
| :--------: | :---------------------: | :----: |
| 동국대학교 | 통계학과/융합소프트웨어 | 김동완 |
| 동국대학교 | 통계학과/데이터사이언스 | 이예슬 |
| 동국대학교 | 통계학과/데이터사이언스 | 조유솔 |

## 분석 PIPE LINE
![파이프라인_수정본_1](https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/7bf6002e-c9d5-4210-99d4-6e008badd87a)

## Analysis Map
![analysis_map](https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/a9512a3e-c343-4254-9e92-786ed111a57e)
```
- 데이터 : 폴더 모양으로 되어있는 부분은 데이터를 의미합니다.
- 코드 : 초록색 글씨와 점선으로 된 부분은 실행되는 코드파일명을 의미합니다.
- 순서 : 순서는 화살표로 표시되어 있습니다.

- 사진을 누르시면 보다 큰 화면으로 확인이 가능합니다.
```

## 사용한 모델
### 1. LSTM (Long Short - Term Memory)
- LSTM은 시퀀스 데이터를 다루는 데 효과적인 순환 신경망(RNN) 아키텍처입니다.
- 주식 시계열 데이터를 분석하기 위해 LSTM모델을 사용했습니다.
- 과거 주식 가격 데이터, 트렌드변수, 이벤트변수, 감성변수를 이용하여 미래 가격을 예측하는데 사용하였습니다.

### 2. GRU (Gated Recurrent Unit)
- GRU 모델은 LSTM과 유사한 순환 신경망(RNN) 아키텍처입니다.
- 주식 시계열 데이터를 분석하기 위해 GRU모델을 사용했습니다.
- GRU는 LSTM보다 계산비용이 적은 모델입니다.
- 과거 주식 가격 데이터, 트렌드변수, 이벤트변수, 감성변수를 이용하여 미래 가격을 예측하는데 사용하였습니다.

## 변수 설명
모델의 성능을 높이기 위해서 3가지의 파생변수를 만들어서 진행하였습니다.

### 1. Sentiment (감성지수변수)
감성지수변수는 전반적인 여론의 반응을 의미하는 변수입니다.</br>
여론의 흐름을 파악하기 위해서 뉴스데이터를 기반으로 감성분석을 진행하였습니다.</br>
- 미래에셋증권에서 제공 받은 뉴스 데이터를 가지고 엔터주와 관련된 뉴스들만 분류
- Clova summary 와 Summa 패키지를 이용하여 분류된 뉴스를 요약
- Clova Sentiment를 이용하여 감성분석
- 회사별로 카테고리 분류

### 2. Event (이벤트변수)
엔터주는 실제로 벌어드리는 수익보다 기대가치가 올라갈 때 주가가 상승하는 경향을 보입니다. </br>
이러한 기대가치가 상승 혹은 하락하는 패턴을 파악하기 위해 이벤트 변수를 만들었습니다. </br>
이벤트 변수는 뉴스기사중에서 기대가치와 관련성이 높은 기사만 추출하여 감성분석을 진행한 변수입니다. </br>
- 회사별로 분류된 감성지수변수에서 기대가치와 관련된 키워드를 필터링
- 이벤트 변수 생성

### 3. Trend (트랜드변수)
트랜드변수는 엔터테인먼트와 아티스트에 대한 팬들의 관심도 및 활도 정도를 나타내기 위한 변수입니다.</br>
이러한 패턴을 확인하기 위해 네이버 검색량 키워드 API와 유튜브 API를 사용하여 수식을 만들었습니다.</br>
- 네이버 검색량 키워드를 이용하여 엔터테인먼트, 아티스트, 멤버 검색량 추출
- 유튜브 API를 이용하여 엔터테인먼트와 아티스트의 동영상 좋아요, 조회수 추출
- 이 두가지를 이용하여 트랜드 변수 생성

## 프로젝트 구조
```
- code/Pre-Processing : 데이터를 전처리하는 코드의 파일
- code/merge : 전처리한 데이터를 병합하여주는 코드의 파일
- code/modeling : LSTM, GRU 등 모델링 코드의 파

- result : 모델링 결과를 csv 파일로 저장한 파일

- data/FINALDATA : 엔터테인먼트별로 분류된 모델링 코드에 들어가는 데이터
- data/Naver : 네이버 키워드 검색량으로 추출 및 전처리된 데이터
- data/YouTube : 유튜브 API로 추출 및 전처리된 데이터
- data/Trend : 트렌드변수 데이터
- data/Stock : 주식및 기술적 보조지표 데이터
- data/mirae : 미래에셋증권에서 제동된 뉴스,시장,고객 데이터
- data/News : 전처리된 뉴스데이터
```

## 사용법
해당 프로젝트에서 데이터 수집, 전처리, 모델링 모두 코드로 구현되어있고 실행 가능하나 API 제한과 실행시간이 매우 길어진다는 이슈로 자동화 과정에서는 데이터 수집과정은 제외되었습니다. 허나 원하시면 주피터 노트북을 통해 개별적으로 실행 가능합니다. 

1. VScode 등을 이용하여 해당 레포지토리를 로컬에 받아주세요.
   ```
   git clone https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA.git
   ```
   
2. 패키지 다운을 위해서 관리자권한 cmd(터미널)를 켜주세요.
   
2. requirement.txt를 통한 패키지 다운을 위해서 analysis 디렉토리로 이동해줍니다.
   ```
   cd ./FINAL-CODE-DATA/analysis
   ```
   
3. 필요한 패키지를 설치합니다.
   ```
   pip install -r requirements.txt
   ```
   
4. 자동화 코드를 위해서 analysis가 포함된 최상단 디렉토리(FINAL-CODE-DATA)로 이동해주세요.
   ```
   cd ../
   ```
   
5. 다음 코드를 복사하여서 터미널에 붙여넣어주세요.
   ```
   jupyter nbconvert --to html --execute analysis/code/pre-processing/news/News_Classification.ipynb analysis/code/pre-processing/news/News_Event.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_hybe.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_sm.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_yg.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_jyp.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_hybe.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_sm.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_yg.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_jyp.ipynb analysis/code/pre-processing/trend/TrendVariable.ipynb analysis/code/merge/dataset_creation_hybe.ipynb analysis/code/merge/dataset_creation_sm.ipynb analysis/code/merge/dataset_creation_yg.ipynb analysis/code/merge/dataset_creation_jyp.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_ALL.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_NONE.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_SENTIMENT_EVENT.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_TREND.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_ALL.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_NONE.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_SENTIMENT_EVENT.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_TREND.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_ALL.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_NONE.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_SENTIMENT_EVENT.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_TREND.ipynb analysis/code/modeling/sm/GRU/GRU_SM_ALL.ipynb analysis/code/modeling/sm/GRU/GRU_SM_NONE.ipynb analysis/code/modeling/sm/GRU/GRU_SM_SENTIMENT_EVENT.ipynb analysis/code/modeling/sm/GRU/GRU_SM_TREND.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_ALL.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_NONE.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_SENTIMENT_EVENT.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_TREND.ipynb analysis/code/modeling/yg/GRU/GRU_YG_ALL.ipynb analysis/code/modeling/yg/GRU/GRU_YG_NONE.ipynb analysis/code/modeling/yg/GRU/GRU_YG_SENTIMENT_EVENT.ipynb analysis/code/modeling/yg/GRU/GRU_YG_TREND.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_ALL_EXCEPT_EVENT.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_ALL.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_NONE.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_SENTIMENT.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_TREND.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_ALL_EXCEPT_EVENT.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_ALL.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_NONE.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_SENTIMENT.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_TREND.ipynb
   ```
## 모델링 결과
최종적으로 성능이 가장 좋았던 GRU 모델을 채택하여 서비스를 구성하였습니다. 다음 그래프는 엔터테인먼트 중 주요하게 거래되는 4가지의 대장 주식에 대한 예측 성능그래프 입니다. 아래 그래프의 Y축은 원(WON) 단위의 종가이고 X축은 2023-01 ~ 2023-06 까지 6개월의 DATE-TIME입니다.<br/><br/>
2023-01 ~ 2023-05 까지의 데이터로 학습시켜 2023-06 한달 간의 종가를 예측한 그래프입니다.<br/><br/>
아래 그래프를 해석하는데 필요한 정보는 아래와 같습니다. 
- 주황색선은 예측된 종가를 의미합니다.
- 파란색선은 실제 종가를 의미합니다.
- ALL : 주식데이터 + 기술적 보조지표 + 감성지수 + 이벤트변수 + 트랜드변수
- NONE : 주식데이터 + 기술적 보조지표
- SENTIMENT_EVENT : 주식데이터 + 기술적 보조지표 + 감성지수 + 이벤트변수
- TREND : 주식데이터 + 기술적 보조지표 + 트랜드변수

### [ HYBE ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/26ae1b20-5f4b-4a92-99a8-b8fd5e1eb2b3" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/409a4da7-3b78-4371-b075-11dccb1aba94" width="550" height="430"/></span>
----

### [ JYP ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/415e4cbe-194e-41ef-94c4-61188bbe3921" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/00ae69ee-d647-45ab-bcdd-22036d4942ff" width="550" height="430"/></span>
----

### [ SM ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/90b1b0dc-270d-4f22-9765-cf55913ac305" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/76dbbf04-406f-4641-9071-f96479703455" width="550" height="430"/></span>
----

### [ YG ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/a64eeb4d-1cb5-442b-95ee-ba0ec28f1d02" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/FINAL-CODE-DATA/assets/122766043/6f9d9745-3814-4b34-8ea1-28d46177d5cd" width="550" height="430"/></span>

## 성능 평가
RMSE (Root Mean Square Error)는 원래 데이터와 예측 데이터 사이의 차이의 제곱을 측정한 후, 제곱근을 취한 값이므로 원래 데이터의 단위와 동일한 단위를 가지기 때문에 해석이 용이하다는 장점을 가지고 있습니다. 이러한 이유로 RMSE로 성능을 평가하였습니다. 아래 RMSE의 단위는 원(WON)입니다.

### HYBE
|        |          LSTM           |  GRU  |
| :-------- | :--------------------- | :---- |
| ALL | 1762 | 2529 |
| NONE | 2763 | 3180 |
| SENTIMENT + EVENT | 3024 | 2440 |
| TREND | 2014 | 3086 | 

### JYP
|        |          LSTM           |  GRU  |
| :-------- | :--------------------- | :---- |
| ALL | 2491 | 1823 |
| NONE | 7664 | 6247 |
| SENTIMENT | 5379 | 2358 |
| TREND | 5824 | 3572 |

### SM
|        |          LSTM           |  GRU  |
| :-------- | :--------------------- | :---- |
| ALL | 676 | 745 |
| NONE | 1311 | 1196 |
| SENTIMENT + EVENT | 798 | 911 |
| TREND | 1127 | 947 |

### YG
|        |          LSTM           |  GRU  |
| :-------- | :--------------------- | :---- |
| ALL | 2147 | 1602 |
| NONE | 3744 | 4140 |
| SENTIMENT + EVENT | 3536 | 2061 |
| TREND | 2547 | 2657 |
