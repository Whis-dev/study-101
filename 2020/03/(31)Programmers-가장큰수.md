# 가장 큰 수

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

**제한 사항**
- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

입출력 예

|numbers|return|
|:---:|:---:|
|[6, 10, 2]|"6210"|
|[3, 30, 34, 5, 9]|"9534330"|

## Problem-solving proccess

**첫번째 실패**
주어진 배열을 sort()를 이용, 사전식으로 배열해서 해당 배열을 다시 reverse한 뒤 string으로 만들면 되겠지 하고 간단하게 생각했다.

```javascript
function solution(numbers) {
    return numbers.sort().reverse().join('');
}
```

하지만 입출력 예제 중 `case 2`가 실패가 떴다.
이유는 답이 `9534330`이 나와야하는데 `9534303`이 나왔기 때문이다.
`case 2`배열을 sort했을 때 나오는 배열은 `[3, 30, 34, 5, 9]`이며 해당 배열을 reverse했을 때 `[9, 5, 34, 30, 3]`이 나온다. 30이 3보다 크기때문에 3보다 앞에 있지만, 큰 수를 만들려면 3이 앞으로 나와야한다.


**두번째 실패**
주어진 배열을 돌면서, 숫자의 자릿수가 1개 이상이면 그 수를 한 자리 수로 쪼개어 배열에 push한뒤 정렬한 후 리버스를 하여 string으로 만들면 어떨까 생각했다.

```javascript
function solution(numbers) {
    return numbers.reduce((final,item) => {
        item.toString().length > 1 ? item.toString().split('').forEach(subItem => final.push(+subItem)) : final.push(item);
        return final;
    }, []).sort().reverse().join('');
}
```

하지만 입출력 예제 중 `case 2`가 실패가 떴다.
이유는 답이 `9534330`이 나와야하는데 `9543330`이 나왔기 때문이다.
`case 2` 배열을 reduce를 이용하며 loop를 돌때, 한 자리 수면 그냥 리턴하고 두 자리 수 이상인 수는 해당 숫자를 쪼개어 답으로 나오는 배열에 push 해주는 로직인데, 이 로직을 타면 `[3, 3, 0, 3, 4, 5, 9]`가 나온다. 해당 배열을 sort하면 `[0, 3, 3, 3, 4, 5, 9]`가 되고, 해당 상태에서 reverse()를 하면 `[9, 5, 4, 3, 3, 3, 0]`이 된다. 애초애 한 수였던 `34`가 쪼개지면서 없는 숫자가 만들어진 상황이 된 것 이다.

**세번째 실패**
고민하다가, 배열의 각 아이템의 앞뒤를 이어 붙인 숫자를 비교하면 어떻게 될까 생각했다.

```javascript
function solution(numbers) {
    return numbers.sort((a,b) => +(`${b}` + `${a}`) - +(`${a}` + `${b}`)).join('');
}
```

해당 로직을 테우면 [9, 5, 34, 3, 30]이 뜨고 이를 string으로 만들면 원하는 답인 `9534330`이 나오게 된다. 
하지만 제출 테스트 케이스 11 에서 실패가 떠서 질문하기를 보니, 0만 있는 배열일 경우를 생각하지 않아 해당 케이스를 위한 추가하여 아래와 같은 해답을 제출했다.

## Problem answer

```javascript
function solution(numbers) {
    const answer = numbers.sort((a,b) => +(`${b}` + `${a}`) - +(`${a}` + `${b}`)).join('');

    // 다른 사람 답변 보니 템플릿 리터럴을 썼을때 아래와 같이 제출할 걸... 하는 아쉬움이 있음.
    // const answer = numbers.sort((a,b) => +(`${b}${a}`) - +(`${a}${b}`)).join('');
    return answer[0] === '0' ? '0' : answer;
}