# 기상 데이터 이상치 탐지 자동화 프로그램

#### 기간 : 2020년 9월~12월 (약 3.5개월) <br/>목적 : 캡스톤<br/>인원/역할 : 3인/데이터 전처리 및 프론트 전체<br/>의의 : 인공지능 모델을 사용한 프로젝트<br/>한계 : 직접 모델 탐색 및 개발을 하지 않고, 이해하여 사용하는 것에 그침


#### 사용 언어 : Python <br/>

## Detail

* Data : 기상자료개방포털의 종관기상관측(ASOS) 자료
* 1D convolution 모델 이용
* KNN 구현으로 데이터 전처리


### 목적
기상 이상치 탐지 자동화 프로그램은 환경과학원 직원이 일일이 지방자치단체에서 보낸 데이터를 확인하고 어떤 사유로 인한 이상치라고 판단하는 작업을 자동화하는 프로그램이다. 해당 작업을 자동화하여 인적 자원을 완전히 대체하기보다는 일부 인적 작업을 자동화로 대체하여 생산성과 일관성, 효율성을 증대시킬 수 있다. 

### 인공지능 모델과의 접목
환경과학원에서 이상치라고 판단하는 규칙 5개 중 4개는 간단한 코드로 구현이 가능하지만, <br/>하나의 규칙은 인공지능 모델 학습이 필요하다.
> 동일 값의 지속이 5시간 이상 연속 될 경우
> 

### 결측치 - KNN 알고리즘 사용
0이나 999999의 결측치는 주로 측정소가 점검 중이거나 센서 오작동이 발생할 경우 입력되는 값이다.<br/> 인공지능 모델 학습 시 bias에 영향을 미칠 수 있어서 따로 처리해주었다.<br/>
* KNN 알고리즘
 > 가장 가까운 K개의 정보들로 새로운 데이터를 예측하는 방법
다른 기체들과의 유클리드 거리를 구하여 가장 가까운 몇몇 측정소들의 평균 값으로 결측치를 대체했다.<br/>
![Alt text](/20210304204528.png)

### 학습 데이터 제작 : 최대 최소 변환(Minmax scaler)을 통한 데이터 스케일링
### 딥러닝 모델
* 입력 : 1시간 간격의 데이터 총 두 달치 (9,1440row)
* 출력 : 최근 한달 동안의 데이터와 이상/정상 판별 데이터, 이상 시 발생하는 증상 값
* 모델 설계 : Resnet 기반 1D convolution 연산을 진행하는 레이어
* 정확도 : 0.83~0.93
