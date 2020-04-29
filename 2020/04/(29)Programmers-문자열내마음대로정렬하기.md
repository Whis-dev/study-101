# 문자열 내 마음대로 정렬하기

문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 [sun, bed, car]이고 n이 1이면 각 단어의 인덱스 1의 문자 u, e, a로 strings를 정렬합니다.<br/>
<br/>

**제한 조건**

- strings는 길이 1 이상, 50이하인 배열입니다.
- strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
- strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
- 모든 strings의 원소의 길이는 n보다 큽니다.
- 인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

**입출력 예**

| strings | n | return |
| ["sun", "bed", "car"] | 1 | ["car", "bed", "sun"] |
| ["abce", "abcd", "cdx"] | 2 | ["abcd", "abce", "cdx"] |

입출력 예 설명<br/>
<br/>
입출력 예 1<br/>
sun, bed, car의 1번째 인덱스 값은 각각 u, e, a 입니다. 이를 기준으로 strings를 정렬하면 ["car", "bed", "sun"] 입니다.<br/>
<br/>
입출력 예 2<br/>
abce와 abcd, cdx의 2번째 인덱스 값은 c, c, x입니다. 따라서 정렬 후에는 cdx가 가장 뒤에 위치합니다. abce와 abcd는 사전순으로 정렬하면 abcd가 우선하므로, 답은 ["abcd", "abce", "cdx"] 입니다.<br/>

## Problem-solving process

이번 문제를 풀면서 배운 것은 python의 sorted()함수에 줄 수 있는 옵션 값들의 종류다.<br/>
처음 sorted함수를 쓸때는 정렬하고 싶은 list만 넘겨 줬었는데, 정렬하고 싶은 list 이외에도 정렬 기준이 되는 key값과, 오름차순으로 정렬할지, 내림차순으로 정렬할지를 정하는 reverse 값 (boolean)을 줄 수 있다고 한다. 따라서, 내가 처음에 생각한 해답은

```python
def solution(strings, n):
    return sorted(strings, key=lambda string: string[n])
```

이었다.이렇게 하면 n번째 값을 기준으로 정렬을 해준다. 하지만, 이 함수를 쓰면 2번째 예의 값이 기대하던 답인 `["abcd", "abce", "cdx"]`가 아니라 `["abce", "abcd", "cdx"]`를 던져준다. 단순히 원소들의 n번째 값으로 나열할 뿐 마지막 제한조건인 `인덱스 n의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다`를 적용시켜주지는 않는다.<br/>
단순히 생각해서 위의 코드를 아래와 같이 고쳐보았다.

```python
def solution(strings, n):
    return sorted(strings.sort(), key lambda string: string[n])
```

하지만 `NoneType Error`가 뜨며 안되었는데, sort() 함수를 이용하지 않고 sorted()를 이용하니 제대로 조건을 만족했다. 한번 사전순으로 정렬시킨뒤, 정렬된 list를 다시 조건에 맞춰 정렬한 방버인데 sorted를 중복으로 사용하여 썩 맘에 들지는 않았다. 추후에 sort() 함수와 sorted()에 대한 자세한 알고리즘을 파악해봐야할 것 같다(return 값도)

## Problem answer

```javascript
function solution(strings, n) {
    return strings.sort((a,b) => a[n] === b[n] ? a.localeCompare(b) : a[n].localeCompare(b[n]));
}
```

```python
def solution(strings, n):
    return sorted(sorted(strings), key=lambda string: string[n])
```
