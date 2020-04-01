# 위장

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.<br/>
<br/>
예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

| 종류 | 이름 |
|:---:|:---:|
| 얼굴 | 동그란 안경, 검정 선글라스 |
| 상의 | 파란색 티셔츠 |
| 하의 | 청바지 |
| 겉옷 | 긴 코트 |

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

**제한사항**
- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.

입출력 예

| clothes | return |
|:---:|:---:|
| [["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]] | 5 |
| [["crow_mask", "face"], ["blue_sunglasses", "face"], ["smoky_makeup", "face"]] | 3 |

입출력 예 설명<br/>

예제 #1<br/>
headgear에 해당하는 의상이 yellow_hat, green_turban이고 eyewear에 해당하는 의상이 blue_sunglasses이므로 아래와 같이 5개의 조합이 가능합니다.

```
1. yellow_hat
2. blue_sunglasses
3. green_turban
4. yellow_hat + blue_sunglasses
5. green_turban + blue_sunglasses
```

예제 #2<br/>
face에 해당하는 의상이 crow_mask, blue_sunglasses, smoky_makeup이므로 아래와 같이 3개의 조합이 가능합니다.

```
1. crow_mask
2. blue_sunglasses
3. smoky_makeup
```

## Problem-solving process

일단 문제풀기에 앞서 인풋으로 들어오는 2차원 배열을 `key:value` 형식으로 정리하기로 했다.

```javascript
function solution(clothes) {
    const clotheObject = clothes.reduce((final, clothe) => {
        final[clothe[1]] = !final[clothe[1]] ? [ clothe[0] ] : final[clothe[1]].push(clothe[0]);
        return final;
    }, {})
}
```

이렇게하면 `clotheObject`의 값이 `case 1` 기준 `{ headgear: 2, eyewear: [ 'blue_sunglasses' ] }` 가 되어버린다. (왜지...?)<br/>

가독성 떨어지고 지극히 개인적으로 싫은 방식이지만 급한대로 for문을 이용하였다.

```javascript
function solution(clothes) {
    let clotheObject = {};
    for(let i = 0; i < clothes.length; i++){
        if (clotheObject[clothes[i][1]]) {
            clotheObject[clothes[i][1]].push(clothes[i][0]);
        } else {
            clotheObject[clothes[i][1]] = [ clothes[i][0] ];
        }
    }
}
```

이렇게 하면 원하는 대로 `clotheObject` 값이 `case 1`기준 `{ headgear: ['yellow_hat', 'green_turban], eyewear: ['blue_sunglasses] }`가 되었다.<br/>
<br/>
이제 경우의 수를 고민을 해야한다.<br/>
겹치지 않는 스타일의 경우의 수를 생각하면, 각각의 옷 아이템의 수와 각 타입 별 경우의 수를 구하여 더해주면 될 것 같았다.<br/>
예를 들어, 옷의 수는 타입과 상관 없이 `case 1` 기준 `3가지`이다.<br/>
여기에 `headgear type은 2가지, eyewear 타입은 1가지`이므로 경우의 수는 `2 * 1 = 2`이다.<br/>
<br/>
이를 구현하면

```javascript
function solution(clothes) {
    let clotheObject = {};
    for(let i = 0; i < clothes.length; i++){
        if (clotheObject[clothes[i][1]]) {
            clotheObject[clothes[i][1]].push(clothes[i][0]);
        } else {
            clotheObject[clothes[i][1]] = [ clothes[i][0] ];
        }
    }

    const clothesKeys = Object.keys(clotheObject);

    return clothes.length + clothesKeys.reduce((final, clotheType) => {
        let clotheArrayLength = clotheObject[clotheType].length;
        return final *= clotheArrayLength
    }, 1)
}
```

그러나 `case 2`가 통과 되지 않는다.<br/>
이유는 각 아이템 수와 한번 곱해준 경우의 수를 더해주다보니 타입이 한 개인 경우엔 중복으로 더해지기 때문이다.<br/>
해당 방어코드를 넣어주면

```javascript
function solution(clothes) {
    let clotheObject = {};
    for(let i = 0; i < clothes.length; i++){
        if (clotheObject[clothes[i][1]]) {
            clotheObject[clothes[i][1]].push(clothes[i][0]);
        } else {
            clotheObject[clothes[i][1]] = [ clothes[i][0] ];
        }
    }

    const clothesKeys = Object.keys(clotheObject);

    return clothesKeys.length > 1
        ? clothes.length + clothesKeys.reduce((final, clotheType) => {
            let clotheArrayLength = clotheObject[clotheType].length;
            return final *= clotheArrayLength
        }, 1)
        : clothes.length;
}
```

하지만 테스트를 돌려보니 28%정도의 정답률을 기록했다. 속도 문제는 없으니, 로직 문제인 것 같아 고민을 해보았다. 아무래도 경우의 수를 잘 못 구하고, 너무 예제 케이스에 의존해서 로직을 짠 것 같았다.<br/>
<br/>
옷의 타입의 갯수에 해당 타입을 입지(쓰지) 않은 상태를 의미하도록 1을 각각 더해 준 뒤 각 숫자를 곱해주고, 마지막에 아무것도 입지 않은 상태인 1을 빼주면 어떨까 생각을 했다.

**테스트는 통과했지만, 경우의 수에 대한 지식이 거의 없어진 것이 많이 아쉬웠다. 알고리즘 문제를 풀기 위해서 수학을 다시 복습을 해야겠다는 생각을 다시금 생각하게 되었다.**

## Problem answer

```javascript
function solution(clothes) {
    let clotheObject = {};
    for(let i = 0; i < clothes.length; i++){
        if (clotheObject[clothes[i][1]]) {
            clotheObject[clothes[i][1]].push(clothes[i][0]);
        } else {
            clotheObject[clothes[i][1]] = [ clothes[i][0] ];
        }
    }

    const clothesKeys = Object.keys(clotheObject);

    return clothesKeys.reduce((final, clotheType, index) => {
            let clotheArrayLength = clotheObject[clotheType].length;
            return final *= (clotheArrayLength + 1)
        }, 1) - 1;
}
```