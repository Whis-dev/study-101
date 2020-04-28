# 같은 숫자는 싫어

배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. <br/>
<br/>
예를 들면,<br/>
<br/>
arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.<br/>
arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.<br/>
배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.<br/>
<br/>

**제한사항**

- 배열 arr의 크기 : 1,000,000 이하의 자연수
- 배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수

**입출력 예**
| arr | answer |
|:---:|:---:|
| [1,1,3,3,0,1,1] | [1,3,0,1] |
| [4,4,4,3,3] | [4,3] |

## Problem-solving process

기존에 푼 문제를 python으로 풀면서 늘 있었던, `원래 제공되는 함수를 몰라서 직접 구현한 사례`를 없애고자 list에서 중복되는 값이 있으면 제거해주는 내장함수는 없는지 인터넷에서 검생을 해보았다. 검색을 한 보람이 있게 방법이 있었다

```python
def solution(arr):
    return list(set(arr))
```

검색을 조금 더 해보니 `set()`은 집합과 비슷하며, 순서가 없다. 또한 집합안에서는 unique한 값을 가지기 때문에 중복되는 값은 자동으로 제거된다. 이 속성을 이용해서 사용한 것 같다.<br/>
하지만 문제는 중복되는 값을 전부 제거하다보니, 첫번째 케이스인 경우 `[3,0,1]`이 만들어져 원하는 값이 나오지 않아 그냥 for loop를 돌면서 조건에 해당하는 원소만 새로만든 list에 넣는 것으로 문제를 풀었다.

## Problem answer

```javascript
function solution(arr)
{
   return arr.reduce((acc,cur) => {
     let length = acc.length;
       if(length == 0 || acc[length - 1] !== cur) {
           acc.push(cur);
       }
       return acc;
   },[]);
}
```

```python
def solution(arr):
    answer = []

    for index in range(len(arr)):
        if index is 0 or arr[index] is not arr[index-1]:
            answer.append(arr[index])

    return answer
```
