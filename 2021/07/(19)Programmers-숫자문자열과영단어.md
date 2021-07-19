# 숫자 문자열과 영단어

네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

1478 → "one4seveneight"
234567 → "23four5six7"
10203 → "1zerotwozero3"

이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.

참고로 각 숫자에 대응되는 영단어는 다음 표와 같습니다.

| 숫자 | 영단어 |
|:---:|:---:|
| 0 | zero |
| 1 | one |
| 2 | two |
| 3 |	three |
| 4 |	four |
| 5 |	five |
| 6 |	six |
| 7 |	seven |
| 8 |	eight |
| 9 |	nine |

제한사항<br/>
1 ≤ s의 길이 ≤ 50<br/>
s가 "zero" 또는 "0"으로 시작하는 경우는 주어지지 않습니다.<br/>
return 값이 1 이상 2,000,000,000 이하의 정수가 되는 올바른 입력만 s로 주어집니다.<br/>
<br/>
입출력 예
| s |	result |
|:---:|:---:|
| "one4seveneight" | 1478 |
| "23four5six7" |	234567 |
| "2three45sixseven" |	234567 |
| "123" |	123 |
<br/>
입출력 예 설명<br/>
입출력 예 #1<br/>
문제 예시와 같습니다.<br/>
<br/>
입출력 예 #2<br/>
문제 예시와 같습니다.<br/>
<br/>
입출력 예 #3<br/>
"three"는 3, "six"는 6, "seven"은 7에 대응되기 때문에 정답은 입출력 예 #2와 같은 234567이 됩니다.<br/>
입출력 예 #2와 #3과 같이 같은 정답을 가리키는 문자열이 여러 가지가 나올 수 있습니다.<br/>
<br/>
입출력 예 #4<br/>
s에는 영단어로 바뀐 부분이 없습니다.<br/>
<br/>
제한시간 안내<br/>
정확성 테스트 : 10초<br/>

## Problem-solving Process

replaceAll은 Node version 15이상에서 사용가능한데, 지금 시점에서 programmers에서는 javascript compile option이 node version 12.18.3이다.
때문에,replace를 이용해서 사용해야하므로 아래와 같이 정규식을 이용하여 해결하면 된다.

## Problem answer
```javascript
function solution(s) {
    const stringNumberArray = ['zero','one', 'two','three','four','five','six','seven','eight','nine'];
    let answer = s;
    
    for (let i = 0; i < 10; i++) {
        const regExp = new RegExp(stringNumberArray[i], 'g');
        answer = answer.replace(regExp, i);
    }
    

    return +answer;
}
```
