# 체육복

점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해 주세요.

**제한 사항**

- 전체 학생의 수는 2명 이상 30명 이하입니다.
- 체육복을 도난당한 학생의 수는 1명이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
- 여벌 체육복을 가져온 학생이 체육복을 도난 당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

**입출력 예**

| n | lost | reserve | return |
|:---:|:---:|:---:|:---:|
| 5 | [ 2, 4 ] | [ 1, 3, 5 ] | 5 |
| 5 | [ 2, 4 ] | [ 3 ] | 4 |
| 3 | [ 3 ] | [ 1 ] | 2 |

**입출력 예 설명**

예제#1

1번학생이 2번 학생에게 체육복을 빌려주고, 3번 학생이나 5번 학생이 4번 학생에게 체육복을 빌려주면 학생 5명이 체육수업을 들을 수 있습니다.

예제#2

3번 학생이 2번 학생이나 4번 학생에게 체육복을 빌려주면 학생 4명이 체육 수업을 들을 수 있습니다.

**출처**

- 공지 - 2019년 2월 18일 지문이 리뉴얼되었습니다.
- 공지 - 2019년 2월 27일, 28일 테스트케이스가 추가되었습니다.

## Problem-solving process

사실 이번 문제는, 이전에 시도를 많이 해보았으나 실패를 많이 한 문제로 이번 기회에 마음먹고 다시 풀어보자! 해서 도전하게 되었다.
이전에는 단순하게, lost 배열과 reserve 배열을 각각 forEach로 loop를 돌며 비교를 하고, reserve에 무언가를 해보려는 시도가 있었었다.(코드를 보니 그런 것 같은데 잘 모르겠다...)

```javascript
//first try
function solution(n, lost, reserve) {
    reserve.forEach(rStudent => {
        lost.forEach(lStudent => {
            if(rStudent != lStudent) {
                if(lStudent == rStudent - 1 || lStudent == rStudent + 1) {
                    lost.splice(lost.indexOf(lStudent), 1);
                }
            }
        })
    })

    return n - lost.length;
}
```

이전의 내가 적어놓은 문제점들을 보면, 도둑맞은 reserve 들을 고려를 안했다고 했는데, 현재 보기로는 그것외에도 문제점은 많다. 일단 가급적 꼭 필요하지 않는 이상 loop안의 loop는 피하는 방법을 고려하지 못한 점이 아쉬운 점이고, if도 nested 되어 있는 것이 아쉬웠다. 이 모든게 계속 nested 되다보니 가독성도 떨어지고, 현재의 내가 보기에 이해하지 못할 무언가의 코드가 나와버렸다. 계속 보다보니 든 생각인데, 나름 여분의 체육복을 가진 학생들의 앞, 뒤 번호가 맞는지 확인을 하고, 그렇다면 lost에서 하나씩 제거 해준뒤, 최종적으로 전체 학생들 수에서 lost인 학생 수(여분의 체육복을 받지 못한 학생 수)를 빼주면 될거라 생각 한 것 같다.

두 번째는 첫번째 시도에서 고려하지 못했다고 적어놓은 reserve가 도둑맞은 경우를 고려를 해보려고 이런저런 시도를 했었던 것 같다. (하지만 3번째 시도까지 해결을 못한듯하다.).

```javascript
//second try
function solution(n, lost, reserve) {
    reserve.forEach(rStudent => {
        lost.pop(lStudent => {
            if((rStudent != lStudent) && (lStudent == rStudent - 1 || lStudent == rStudent + 1)) {
                return lStudent;
            }
        })
    })

    return n - lost.length;
}
```

두 번째 시도를 했을 땐, 지금의 내가 생각했던 것처럼 loop안에 loop가 부담스러웠는지, 그것을 pop()을 이용해서 해결하려고 했던 것 같다. 이때당시 pop()이 정확히 어떤 역할을 하는지는 모른채, 그냥 해당하는 원소를 제거해주는 것으로만 알고 있었다. 용도를 아는 지금 보았을 때는, 적절치 않은 시도라고 생각한다.

```javascript
//third try
function solution(n, lost, reserve) {
    const filteredReserve = reserve.filter(rStudent => lost.indexOf(rStudent) == -1);
    const filteredLost = lost.filter(lStudent => reserve.indexOf(lstudent) == -1);

    filteredReserve.forEach(rStudent => {
        filteredLost.forEach(lStudent => {
            if(lStudent == rStudent - 1 || lStudent == rStudent + 1) {
                filteredLost.splice(filteredLost.indexOf(lStudent), 1);
            }
        })
    })
    return n - filteredLost.length;
}
```

이번엔 여유분을 가지고 있어도 도둑맞은 학생들을 감별하기위해 filteredReserve라는 것을 만들었고, lost에서도 중족되는 애가 있는지 확인 하기 위해서 filteredLost라는것을 만든 것 같다. 나머지 로직은 첫번째에서 벗어난 것이 없다. 생각을 해보니 이때는 reduce를 사용하는 방법이 익숙하지 않으니 forEach를 마구 썼던 것 같다.

과거에 이렇게 풀고 포기를 하고 이번에 다시 보았을 때, 왜 이 문제를 이렇게 어렵게 생각했나 그런 생각이 들었다.

일단, 모든 학생들이 체육복을 가지고 있다고 가정하고, 학생 수 만큼의 배열을 만들어 1로 채워둔다. (`Students` 배열)
그다음, lost배열을 돌면서, `Students`배열에서 해당하는 `번호 - 1`인덱스의 값에서 1을 빼준다.
그리고 reserve배열을 돌면서, `Students`배열에서 해당하는 `번호 - 1`인덱스의 값에서 1을 더해준다.

이 과정을 거치면 `Students`배열은 각 학생이 가지고 있는 체육복의 수를 가지고 있는 배열이 된다.
이 `Students`배열을 돌면서, 체육복을 2개 가진 학생인 경우, index가 0이 아닐때, 자기 번호 앞에있는 학생이 체육복이 없으면 해당 학생의 체육복 수를 1로 올려주고, 자신의 순번에는 체육복이 1개 있는걸로 한다. 만약 앞에있는 친구가 체육복을 가지고 있고 뒷 번호 학생이 체육복을 가지고 있지 않으면 뒷 번호 학생의 체육복 수를 1로 올려주고 자신의 번호에는 1을 넣어준다.
만약 체육복을 2개가지고 있지 않을 경우엔, 앞번호에서 채워준 경우를 고려하여 자신의 순번 배열의 값이 1이 아니거나 값이 없는 경우, 본래의 자신의 값을 넣어주도록 했다.

그리고 이렇게 만들어진 배열에서, 값이 1인 경우만 필터링하여 필터링된 배열의 길이를 넘겨주면 원하는 값을 얻을 수 있다.

## Problem answer

```javascript
function solution(n, lost, reserve) {
    const students = new Array(n).fill(1);

    lost.forEach(lostStudent => students[lostStudent - 1]  = students[lostStudent - 1] - 1);
    reserve.forEach(reserveStudent => students[reserveStudent - 1]  = students[reserveStudent - 1] + 1);

    return students.reduce((final, student, index) => {
        if (student === 2) {
            (index !== 0 && final[index-1] === 0)
                ? (final[index-1] = 1)
                : (students[index+1] === 0 && (final[index+1] = 1))
            final[index] = 1;
        } else {
            final[index] !== 1 && (final[index] = student);
        }
        return final;
    }, new Array(n)).filter(c => c === 1).length;
}
```
