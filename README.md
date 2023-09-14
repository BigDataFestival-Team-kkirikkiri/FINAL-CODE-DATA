# 게이미피케이션을 활용한 주가예측 기반의 종목 위험도 평가와 고객 군집화 및 수익률 랭킹 서비스

### 서비스 개요
본 팀의 서비스는 주식 시장에 본격적으로 입문하고 싶지만 주식에 대한 어려움을 느끼는 일명 '주린이' 고객들을 주요 대상으로 합니다. 메인 서비스는 <위험도 예측>, <고객군집화>이며, 이 서비스들을 활성화하기 위한 방안으로 게이미피케이션을 고안하였습니다.

### 팀 소개
<p>팀명 : 끼리끼리</p>
<p>프로젝트 기간 : 2023/7/1 ~ 2023/09/13</p>

|    소속    |          전공           |  이름  |
| :--------: | :---------------------: | :----: |
| 동국대학교 | 통계학과/융합소프트웨어 | 김동완 |
| 동국대학교 | 통계학과/데이터사이언스 | 이예슬 |
| 동국대학교 | 통계학과/데이터사이언스 | 조유솔 |

## 🔶 체크 사항
#### 1. 자동화 코드는 유튜브 및 네이버의 API 제한과 시간이 오래걸린다는 문제가 있어 전처리과정부터 모델링과정까지만 넣어놨습니다. 코드에 들어가셔서 .ipynb를 직접실행하면 수집과정부터 전과정을 확인 할 수 있습니다.
#### 2. 3.9 이상의 파이썬 버전이 요구됩니다. 버전이 낮을시에 보고서와 다른 성능이 나올 수 있습니다.
#### 3. YouTube 데이터 수집 코드에서 API Key 부분은 보안상의 문제로 모두 ‘***’로 마킹 처리하였습니다. 만약 해당 코드를 실행시키고자 한다면, 마킹 처리된 api key 입력 칸에 YouTube_API_key.txt 파일에 적힌 api key 값을 넣으면 됩니다. 키파일은 메일로 제출하였습니다.
- YouTube_accounts.ipynb
- YouTube_accounts_sm.ipynb
- YouTube_videos_hybe.ipynb
- YouTube_videos_jyp.ipynb
- YouTube_videos_sm.ipynb
- YouTube_videos_yg.ipynb

## 분석 PIPE LINE
![파이프라인_수정본_1](https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/18622bc5-d46e-4844-9f0c-d8b8453794f1)

## Analysis Map
![분석MAP 0912_1](https://github.com/BigDataFestival-Team-kkirikkiri/FINAL-CODE-DATA/assets/122766043/b76deab9-5c14-4685-9666-3f8090755610)
![고객 MAP 0912_1](https://github.com/BigDataFestival-Team-kkirikkiri/FINAL-CODE-DATA/assets/122766043/19bce4aa-32a9-4817-b78e-26f9fa9d80ef)
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

### 3. Trend (트렌드변수)
트렌드변수는 엔터테인먼트와 아티스트에 대한 팬들의 관심도 및 활도 정도를 나타내기 위한 변수입니다.</br>
이러한 패턴을 확인하기 위해 네이버 검색량 키워드 API와 유튜브 API를 사용하여 수식을 만들었습니다.</br>
- 네이버 검색량 키워드를 이용하여 엔터테인먼트, 아티스트, 멤버 검색량 추출
- 유튜브 API를 이용하여 엔터테인먼트와 아티스트의 동영상 좋아요, 조회수 추출
- 이 두가지를 이용하여 트렌드 변수 생성

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
해당 프로젝트에서 데이터 수집, 전처리, 모델링 모두 코드로 구현되어있고 실행 가능하나 API 제한과 실행시간이 매우 길어진다는 이슈로 자동화 과정에서는 데이터 수집과정은 제외되었습니다. 허나 원하시면 주피터 노트북을 통해 개별적으로 실행 가능합니다. 자동화가 잘 실행이 안되신다면 아래 시연영상을 참고해주세요. 
### 대략 15분정도의 시간이 소요됩니다.
### result에 _RISK (위험도평가)의 결과값(_RISK.csv)은 주피터로 열게되면 깨지지않습니다.
### 자동화단계에서 Risk_Evaluation에서 오류가 발생하면 개별적으로 주피터나 vsCODE에서 돌려주시면 잘 진행됩니다.
### [☑️ 시연영상 보기](https://www.youtube.com/watch?v=-D2BINYFSgE)

1. VScode 등을 이용하여 해당 레포지토리를 로컬에 받아주세요.
   ```
   git clone https://github.com/BigDataFestival-Team-kkirikkiri/FINAL-CODE-DATA.git
   ```
   
2. 패키지 다운을 위해서 관리자권한 cmd(터미널)를 켜주세요.
   
2. requirements.txt를 통한 패키지 다운을 위해서 analysis 디렉토리로 이동해줍니다.
   ```
   cd ./FINAL-CODE-DATA/analysis
   ```
   
3. 필요한 패키지를 설치합니다. 아래 코드를 터미널에 입력해주세요.
   ```
   pip install -r requirements.txt
   ```
   
4. 자동화 코드를 위해서 analysis가 포함된 최상단 디렉토리(FINAL-CODE-DATA)로 이동해주세요.
   ```
   cd ../
   ```
   
5. 다음 코드를 복사하여서 터미널에 붙여넣어주세요.
   ```
   jupyter nbconvert --to html --execute analysis/code/pre-processing/news/News_Classification.ipynb analysis/code/pre-processing/news/News_Event.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_hybe.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_sm.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_yg.ipynb analysis/code/pre-processing/naver/NaverDataLab_Preprocessing_jyp.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_hybe.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_sm.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_yg.ipynb analysis/code/pre-processing/youtube/YouTube_Preprocessing_jyp.ipynb analysis/code/pre-processing/trend/TrendVariable.ipynb analysis/code/merge/dataset_creation_hybe.ipynb analysis/code/merge/dataset_creation_sm.ipynb analysis/code/merge/dataset_creation_yg.ipynb analysis/code/merge/dataset_creation_jyp.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_ALL.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_NONE.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_SENTIMENT_EVENT.ipynb analysis/code/modeling/hybe/LSTM/LSTM_HYBE_TREND.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_ALL.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_NONE.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_SENTIMENT_EVENT.ipynb analysis/code/modeling/hybe/GRU/GRU_HYBE_TREND.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_ALL.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_NONE.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_SENTIMENT_EVENT.ipynb analysis/code/modeling/sm/LSTM/LSTM_SM_TREND.ipynb analysis/code/modeling/sm/GRU/GRU_SM_ALL.ipynb analysis/code/modeling/sm/GRU/GRU_SM_NONE.ipynb analysis/code/modeling/sm/GRU/GRU_SM_SENTIMENT_EVENT.ipynb analysis/code/modeling/sm/GRU/GRU_SM_TREND.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_ALL.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_NONE.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_SENTIMENT_EVENT.ipynb analysis/code/modeling/yg/LSTM/LSTM_YG_TREND.ipynb analysis/code/modeling/yg/GRU/GRU_YG_ALL.ipynb analysis/code/modeling/yg/GRU/GRU_YG_NONE.ipynb analysis/code/modeling/yg/GRU/GRU_YG_SENTIMENT_EVENT.ipynb analysis/code/modeling/yg/GRU/GRU_YG_TREND.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_ALL_EXCEPT_EVENT.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_ALL.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_NONE.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_SENTIMENT.ipynb analysis/code/modeling/jyp/GRU/GRU_JYP_TREND.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_ALL_EXCEPT_EVENT.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_ALL.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_NONE.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_SENTIMENT.ipynb analysis/code/modeling/jyp/LSTM/LSTM_JYP_TREND.ipynb analysis/code/pre-processing/customer/Customer_Ranking_Clustering.ipynb analysis/code/modeling/Risk_Evaluation.ipynb
   ```
6. 최종 csv파일은 result에 저장되며 모델링결과는 model폴더에서 확인 할 수 있습니다.
   ```
   파이썬의 실행 결과는 ipynb로 저장되는게 아니라 html로 저장되므로 모델링 결과는 .html 파일을 확인해주세요 !
   ```
   
## 모델링 결과
최종적으로 성능이 가장 좋았던 GRU 모델을 채택하여 서비스를 구성하였습니다. 다음 그래프는 엔터테인먼트 중 주요하게 거래되는 4가지의 대장 주식에 대한 예측 성능그래프 입니다. 아래 그래프의 Y축은 원(WON) 단위의 종가이고 X축은 2023-01 ~ 2023-06 까지 6개월의 DATE-TIME입니다.<br/><br/>
2023-01 ~ 2023-05 까지의 데이터로 학습시켜 2023-06 한달 간의 주가(종가)를 예측한 그래프입니다.<br/><br/>

|  CASE  |  변수설명  |  
| :----- | :----- |
| `NONE` | 주식데이터 + 기술적 보조지표 |
| `ALL` | 주식데이터 + 기술적 보조지표 + 감성지수 + 이벤트변수 + 트렌드변수 | 
| `SENTIMENT + EVENT` | 주식데이터 + 기술적 보조지표 + 감성지수변수 + 이벤트변수 | 
| `SENTIMENT` | 주식데이터 + 기술적 보조지표 + 감성지수변수 |
| `TREND` | 주식데이터 + 기술적 보조지표 + 트렌드변수 |  

-----
### [ HYBE ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/1ac17944-cfe5-4ea6-8243-a1b8a264a89b" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/fc3e59e3-904f-45f9-a9ef-83c98d942762" width="550" height="430"/></span>
-----

### [ JYP ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/722b8efe-150e-4f5a-8ee3-35d4ca1cfdf2" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/af92dcd5-7163-4caf-a029-2b113269ea54" width="550" height="430"/></span>
-----

### [ SM ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/1d086619-9cb5-464a-b279-b439245ceb6b" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/d42e3562-0139-4aa0-91fb-de38583e4c01" width="550" height="430"/></span>
-----

### [ YG ]
#### ALL
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/6c49ea1a-187c-4a8e-bb2b-4fecd068a15c" width="550" height="430"/></span>
#### NONE
<span><img src="https://github.com/khlskahd-dasdsad-asdwdw/code-test/assets/122766043/1e7b5ee6-6dc9-4c05-a319-6c222b5b18a3" width="550" height="430"/></span>

## 성능 평가
RMSE (Root Mean Square Error)는 원래 데이터와 예측 데이터 사이의 차이의 제곱을 측정한 후, 제곱근을 취한 값이므로 원래 데이터의 단위와 동일한 단위를 가지기 때문에 해석이 용이하다는 장점을 가지고 있습니다. 이러한 이유로 RMSE로 성능을 평가하였습니다. 아래 RMSE의 단위는 원(WON)입니다.

성능 개선은 RMSE의 하락 비율을 의미합니다.

### GRU
|        |  HYBE  |  JYP  | SM | YG |
| :----- | :-----: | :----: | :----: | :----: |
| `NONE` | **3036** | **6247** | **1207** | **4139** |
| `ALL` | **2608** | **1822** | **745** | **1602** |
| `SENTIMENT + EVENT` | 2437 | - | 910 | 2062 |
| `SENTIMENT` | - | 2358 | - | - |
| `TREND` | 2510 | 3572 | 948 | 2658 | 
| `성능개선` | **14%** | **70%** | **38%** | **61%** | 

### LSTM
|        |  HYBE  |  JYP  | SM | YG |
| :----- | :-----: | :----: | :----: | :----: |
| `NONE` | **2494** | **7664** | **1305** | **3753** |
| `ALL` | **1840** | **2491** | **680** | **2147** |
| `SENTIMENT + EVENT` | 3700 | - | 800 | 3537 |
| `SENTIMENT` | - | 5383 | - | - |
| `TREND` | 2077 | 5826 | 1127 | 2547 | 
| `성능개선` | **26%** | **67%** | **47%** | **42%** | 
