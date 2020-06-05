# 자릿수 더하기

자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.<br/>
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.<br/>
<br/>

**제한사항**

- N의 범위 : 100,000,000 이하의 자연수

**입출력 예**
| N | answer |
|:---:|:---:|
| 123 | 6 |
| 987 |	24 |

입출력 예 설명<br/>
입출력 예 #1<br/>
문제의 예시와 같습니다.<br/>
<br/>
입출력 예 #2<br/>
9 + 8 + 7 = 24이므로 24를 return 하면 됩니다.<br/>

## Problem-solving process

이번 문제를 파이썬으로 풀때, 고려했던 부분은 for loop를 쓰지 않고, python 내장함수로만 문제를 해결하는 것이었다.<br/>
<br/>
문제 자체는, 숫자 형식으로 들어온 input을 string형식으로 전환한뒤, 해당 문자열을 순차적으로 loop를 돌며 int형식으로 전환함과 동시에 합계를 구하면 되는데. 합계를 구하는 부분은 python에서 기본적으로 제공해주는 내장함수인 `sum()`을 사용하였다.<br/>
<br/>
풀이 이후 다른 사람들이 푼 답을 보는데, 재귀함수로 접근하여 푼 사람들도 있었고, 나와 비슷하지만, 나는 함수에 대한 이해가 짧아서 구구절절 푼 부분을 간결하게 푼 사람들도 있었다.

## Problem answer

```javascript
function solution(n) {
    // First Solution
    // let temp = [...n.toString()];
    // let answer = temp.reduce((sum,value)=>{
    //                 sum += Number(value);
    //             return sum;
    //             }, 0);
    // return answer;
    
    //Seconde Solution
    return [...n.toString()].reduce((sum,value)=>{return sum += Number(value)}, 0);
}
```

```python
def solution(n):
    return sum(list(map(lambda x: int(x), str(n))))
```