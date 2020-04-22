# 문자열 내 p와 y의 개수

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.<br/>
<br/>
예를 들어 s가 pPoooyY면 true를 return하고 Pyy라면 false를 return합니다.<br/>
<br/>

**제한사항**

- 문자열 s의 길이 : 50 이하의 자연수
- 문자열 s는 알파벳으로만 이루어져 있습니다.

**입출력 예**

| s | answer |
|:---:|:---:|
| "pPoooyY" | true |
| "Pyy" | false |

**입출력 예 설명**<br/>
<br/>
입출력 예 #1<br/>
'p'의 개수 2개, 'y'의 개수 2개로 같으므로 true를 return 합니다.<br/>
<br/>
입출력 예 #2<br/>
'p'의 개수 1개, 'y'의 개수 2개로 다르므로 false를 return 합니다.<br/>

## Problem-solving process

주어진 문자열의 case를 맞춘뒤 p와 y의 갯수를 비교하여 리턴하면 된다.<br/>
이번 문제의 주안점으로 둔 것은 python의 filter와 lambda를 써보는 것이었다. 아직 잘은 모르겠지만 python에서의 람다는 javascript에서 화살표 함수같은 느낌이 들었다.<br/>
다만 이번 풀이에서 아쉬운 점은 filter된 값으로 이루어진 list의 len을 비교하는 것이기 때문에 꽤 nested되었다는 점인데, 조금더 좋은 방법이 없는지 고민해봐도 좋을 것 같다.

## Problem answer

```javascript
function solution(s){
    var countP = s.toLowerCase().split('').filter(s => s == 'p');
    var countY = s.toLowerCase().split('').filter(s => s == 'y');
    return countP.length == countY.length ? true : false;
}
```

```python
def solution(s):
    return len(list(filter(lambda x: x is 'p', s.lower()))) is len(list(filter(lambda x: x is 'y', s.lower())))
```