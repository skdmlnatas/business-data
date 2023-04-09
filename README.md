# business-data
* Dense : fully connected
* soft max : 확률값을 나타내는 함수. 모두 더하면 1
* Stochastic Gradient Descent(SGD) : 확률적 gd
### 이진분류 (binary classification)
리뷰 데이터 5만개 중 25000개는 train_data, 25000개는 test_data이고, 각각 50%는 긍정(1), 50%는 부정(0)이다. 리뷰에 자주 나오는 단어 10000개를 설정해서, 단어들이 어떻게 나왔을 때 리뷰가 긍정일 확률이 높은지, 부정일 확률이 높은지 판단한다. 마지막에 sigmoid 함수 사용하였다.
* relu 함수는 왜 사용하나요? -> relu 함수는 활성화 함수인데, 선형적인 분류만으로는 아무리 층을 깊게 쌓아도 선형연산이라는 한계(구체화 필요)를 벗어날 수 없기 때문에 비선형 분류를 해주기 위해서 사용한다. (케라스 창시자 p.110)<br>
train_data[][]의 1차원 데이터 하나의 인덱스는 0부터 9999까지라서 10000개의 각각의 단어들이 등장할 때마다 그 단어에 해당하는 숫자로 변환되어 저장되어있다. train_data를 batch=512개씩 묶어서 epoch=5번을 돌린다. 동시에 test_data를 이용해서 얼마나 잘 분류되고있는지 판단한다. test_data에 대해서는 back propagation을 하지 않을 것이다.
### 다중분류 (multiclass classification)
뉴스 기사 분류
특정 단어가 있으면 그 단어에 해당하는 번호의 인덱스에 1을 넣는다. 예를 들어서, '사진'(3)이라는 단어가 등장하면 [0, 0, 0, 1, 0, ....]이렇게 된다. (그럼 같은 단어가 여러번 나왔더라도 한 번 나온거랑 다름 없게 판단하겠?)
### 회기 (regression)
주택 가격
* 이진: 둘 중 하나 / 다중: 여럿 중 하나 / 회기: 주관식<br>
여러 특징들을 기반으로 주택 가격을 예측할텐데, 특징들 간의 weight에 너무 큰 차이가 나면 바람직하지 않기 때문에(구체화 필요) 정규화 과정을 거친다. (특성-평균)/표준편차 하면 1보다 작아진다고 한다(구체화 필요).
***
학습 데이터가 적을 때, "K-겹 검증 사용"<br>
batch 단위로 묶었더니 k 묶음이 나왔다. 각각의 묶음을 모두 한 번씩 돌아가면서 validation_data로 사용하고 나중에 평균 내서 학습을 완료한다. epoch 수가 엄청 늘어난다.
* train data: 훈련을 시키기 위해 사용하는 데이터 / validation data: epoch 한 번 돌 때마다 피팅 정도를 테스트하기 위해 하용하여 적절한 epoch 수를 잡는데 사용 /  test data: 훈련 다 끝난 후에 마지막 테스트 하기위해 사용하는 데이
* 여기서도 epoch를 몇으로 잡을지 loss function을 보고 찾아야 하는데, 초반에는 에러가 확 줄어들 것이고, 그 뒷부분부터 확인하며 어디서 자르는 것이 좋을지 판단한다.<br>
* 분류문제에서는 crossentropy, 회귀문제에서는 meansquererror를 loss function으로 사용한다.
`#0969DA`
