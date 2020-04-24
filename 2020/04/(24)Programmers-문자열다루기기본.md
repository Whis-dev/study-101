# 문자열 다루기 기본

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다.
<br/><br/>

**제한 사항**

- s는 길이 1 이상, 길이 8 이하인 문자열입니다.

**입출력 예**

| s | return |
|:---:|:---:|
| "a234" | false |
| "1234" | true |

## Problem-solving process

문제에 주어진대로, 주어진 string의 길이가 4 또는 6인지 확인하고 해당 string이 int로 변환이 되는지 확인하면 된다.<br/>
방법은 2가지가 있는데, 하나는 정규식을 이용하는 것이고, 하나는 조건문을 이용하여 비교하면 된다.<br/>
파이썬 같은 경우, int() 함수를 실행시켜서, 에러가 날경우 그 에러를 잡아서 False를 리턴해주고, int로 변환될 경우 해당 타입이 int인지 아닌지에 대한 조건을 리턴해주었다.<br/>
처음에 `if len(s) is 4 or 6`으로 조건을 주었는데, 내가 의도했던 뜻은 `len(s)는 4 또는 6` 이었으나, 제대로 조건이 걸리지 않았고(case 5, 6이 fail로 뜸) 그래서 개선해본 `if len(s) is (4 or 6)`으로 변환 해보았는데, 아예 에러가 떠버렸다. 문제에서 원하는 것처럼 길이가 4 또는 6으로 비교를 할려면 조건을 각각 줘야함을 배웠다.(후자는 약간 javascript식으로 접근했다가 안된 것 같다.)

## Problem answer

```javascript
function solution(s) {
    // test 11번 안됨
    // var test = s.split('');
    // if(test.length == 4 || test.length == 6) {
    //     return isNaN(s) ? false : true;
    // } else {
    //     return false;
    // }

    //first Solution
    // if(s.length == (4 || 6)){
    //     let regExp = /^[0-9]+$/;
    //     return regExp.test(s);
    // } else {
    //     return false;
    // }

    //second Solution
    // return s.length == (4 || 6) ? /^[0-9]+$/.test(s) : false;

    //third Solution
    return /^\d{6}$|^\d{4}$/.test(s);
}
```

```python
def solution(s):
    try:
        if int(s):
            return len(s) is 4 or len(s) is 6
    except:
        return False;
```