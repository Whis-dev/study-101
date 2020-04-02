# 최대공약수와 최소공배수

두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다.<br/>
예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.<br/>

**제한 사항**
- 두 수는 1이상 1000000이하의 자연수입니다.

입출력 예

| n | m | return |
|:---:|:---:|:---:|
| 3 | 12 | [3, 12] |
| 2 | 5 | [1, 10] |

입출력 예 설명 <br/>

입출력 예 #1<br/>
위의 설명과 같습니다. <br/>
<br/>
입출력 예 #2<br/>
자연수 2와 5의 최대공약수는 1, 최소공배수는 10이므로 [1, 10]을 리턴해야 합니다.

## Problem-solving process

최대공약수를 먼저 구해야 최소공배수를 구할 수 있기 때문에, 최대공약수를 구할 수 있는 방법을 먼저 고민을 했다. 
수학적으로는 최대공약수를 구하는 법을 알고 있지만, 알고리즘 적으로는 알고 있는 지식이 적어서 인터넷에서 최대공약수와 관련된 알고리즘이 있는지 확인해 보았다.<br/>
<br/>
찾아보니 해당 알고리즘은 `유클리드 호제법` 이라는 알고리즘인데, [위키피디아](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)에 따르면 `유클리드 호제법(-互除法, Euclidean algorithm) 또는 유클리드 알고리즘은 2개의 자연수 또는 정식(整式)의 최대공약수를 구하는 알고리즘의 하나이다. 호제법이란 말은 두 수가 서로(互) 상대방 수를 나누어(除)서 결국 원하는 수를 얻는 알고리즘을 나타낸다. 2개의 자연수(또는 정식) a, b에 대해서 a를 b로 나눈 나머지를 r이라 하면(단, a>b), a와 b의 최대공약수는 b와 r의 최대공약수와 같다. 이 성질에 따라, b를 r로 나눈 나머지 r'를 구하고, 다시 r을 r'로 나눈 나머지를 구하는 과정을 반복하여 나머지가 0이 되었을 때 나누는 수가 a와 b의 최대공약수이다. ` 라고 한다.<br/>
<br/>
해당 해법에 따른 구현은 재귀함수를 이용하였다.

```javascript
function greatestCommonFactor (a,b) {
    const max = Math.max(a,b);
    const min = Math.min(a,b);
    const remains = max % min;

    return remains === 0 ? min : greatestCommonFactor(min, remains);
}
```

나머지가 0이면 해당 함수의 최소값을 리턴해주는 재귀함수를 구현하였고, 이를 이용하여 최소공배수까지 구하여 해답을 구하는 solution 함수를 추가적으로 구현하였다.

## Problem answer

```javascript
function greatestCommonFactor (a,b) {
    const max = Math.max(a,b);
    const min = Math.min(a,b);
    const remains = max % min;

    return remains === 0 ? min : greatestCommonFactor(min, remains);
}

function solution(a,b) {
    const gcf = greatestCommonFactor(a,b);
    const lcf = (a * b) / gcf;

    return [ gcf,lcf ];
}
```