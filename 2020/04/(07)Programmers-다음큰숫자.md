# 다음 큰 숫자

자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.<br/>
- 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
- 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
- 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.
예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.<br/>
<br/>
자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.<br/>
<br/>
**제한 사항**
- n은 1,000,000 이하의 자연수 입니다.

입출력 예

| n | result|
|:---:|:---:|
| 78 | 83 |
| 15 | 23 |

**입출력 예 설명**<br/>
입출력 예#1<br/>
문제 예시와 같습니다.<br/>
<br/>
입출력 예#2<br/>
15(1111)의 다음 큰 숫자는 23(10111)입니다.<br/>

## Problem-solving process

하나의 변수를 선언하고 해당 변수의 최초의 수를 input보다 1 더 큰 수로 한다.<br/>
선언된 변수, 그리고 input 수를 각각 2진수로 변환한 뒤 각각의 2진수가 가진 1의 갯수가 다르면 계속 loop를 돌도록 한다. (1의 갯수가 같으면 loop가 멈추도록)

## Problem answer

```javascript
function solution(n) {
    let answer = n + 1;
    
    while (n.toString(2).match(/1/g).length !== answer.toString(2).match(/1/g).length) {
        answer++;
    };
    
    return answer;
}
```