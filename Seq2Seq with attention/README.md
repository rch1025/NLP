# :books: Seq2Seq with Badanau attention
- 고정된 길이의 context vector를 반환하는 `기존 인코더-디코더 구조(seq2seq)는 문장의 길이에 따라 성능의 저하가 발생함`
- 기존과 같이 단일 context vector로 만들지 않고, 입력 문장을 일련의 벡터로 인코딩 한 뒤에 `번역을 디코딩하는 동안 적응적으로 인코딩 벡터의 하위 집합을 찾음`
- 제안 방법론은 인코더-디코더 구조에 attention을 사용하는 방법론(RNN Search)으로 본 방법론을 사용하여 번역을 수행할 때, `가장 관련된 부분이 어디인지 찾고 이를 반영함`
---

## :bulb: Badanau Attention
- Context vector $c_i$는 hidden states $h_j$값과 attention score $a_ij$의 가중합을 통해 구해짐
$$c_i = \sum_{j=1}^n a_{ij}h_{j.} $$
- `Attention energy(alignment model)`은 $j$번째 input 값이 $i$번째 output값과 얼마나 관련이 있는가를 나타냄
$$a_{ij} = \frac{exp(e_{ij})}{\sum_{k=1}^T exp(e_{ik})}$$
$$e_{ij}= a(s_{i-1}, h_j)$$
$a_{ij}$ : 대상 단어 $y_i$가 소스 단어 $x_i$에 의해 
정렬되거나 번역될 확률</br>
$c_{i}$ : 확률 $a_{ij}$를 갖는 모든 주석에 대한 예상 주석</br>
- Alignment model $a$은 feedforward network로 구성된다.

---
## :bulb: Contribution
1. 전체 입력 문장을 완벽하게 인코딩할 필요없이 `특정 단어를 둘러싸는 입력 문장의 부분만 정확하게 인코딩` 하기에 `긴 문장 번역에 더 효과적이다.` => 기존 고정된 context vector로부터 오는 문제 해결
2. 다음 대상 단어 생성과 관련된 정보에만 집중이 가능하며 가중치 $a_{ij}$를 시각화하여 타겟 단어를 생성할 때, `알고리즘이 소스 문장의 어느 부분에 집중하였는지 확인`할 수 있음 => 시각화 가능
3. 비교 방법론들 보다 성능이 더 우수함

---
### :postbox: Reference
- Paper link: https://arxiv.org/abs/1409.0473
- Original code link: https://github.com/ndb796/Deep-Learning-Paper-Review-and-Practice/blob/master/code_practices/Sequence_to_Sequence_with_Attention_Tutorial.ipynb