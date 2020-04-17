# 완주하지 못한 선수

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

**입출력 예**

| participant |	completion | return |
|:---:|:---:|:---:|
| ["leo", "kiki", "eden"] | ["eden", "kiki"] | "leo" |
| ["marina", "josipa", "nikola", "vinko", "filipa"] | ["josipa", "filipa", "marina", "nikola"] | "vinko"|
| ["mislav", "stanko", "mislav", "ana"] | ["stanko", "ana", "mislav"] |	"mislav" |

입출력 예 설명<br/>
예제 #1<br/>
leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.<br/>
<br/>
예제 #2<br/>
vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.<br/>
<br/>
예제 #3<br/>
mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.<br/>

## Problem-solving process

이전에 자바스크립트로 풀었던 문제를 최근 공부중인 파이썬으로 다시 풀어본 문제이다.<br/>
기존에 자바스크립트로 풀었을 때는 해시 알고리즘에 맞게 풀지는 않았고, 두 배열을 sort() 하고 값이 틀리면 return 해주는 방식으로 문제를 풀었었다.<br/>

```javascript
function solution(participant, completion) {
    // completion.forEach(completion => {
    //     participant.splice(participant.indexOf(completion),1);
    // })
    // return participant[0];
    
    participant.sort()
    completion.sort()
    for(let i in participant) {
        if(participant[i] !== completion[i]) 
            return participant[i];
    }
}
```

처음에 접근할 때는 기존에 풀었던 방식을 토대로 해당 코드를 python방식으로 바꿔서 풀었다.<br/>
(python은 따로 sort를 안해도 값을 검색할 수 있어서 sort를 하는 건 무의미하다고 생각했다.)

```python
def solution(participant, completion):
    for p in participant:
        if p not in completion:
            return p
        else:
            completion.remove(p)
```

하지만, for loop안에 .remove를 써서 시간 복잡도가 O(n^2)가 되어버려서 효율성 테스트에서 떨어진 것 같았다.(일단 remove 또한 시간 복잡도에 영향을 준다는 것을 처음 배웠다.)<br/>
그래서 시간복잡도를 낮추기위해 고민을 했고, participant들이 들어가있는 dictionary를 만든 후, participant가 돌면서, 해당 선수가 있으면 해당 선수 값에 1을 더해준다.<br/>
같은 방법으로 completion이 돌때는, 해당 선수가 있으면 해당 선수 값에서 -1을 해준 후, 최종적으로 선수가들어있는 dictionary에서 값이 1인 선수를 return해주면 될거라고 생각했다.
따라서, 시간 복잡도 또한 분산되어 이전 코드 대비 더 빠르게 결과 값을 도출할 수 있었다.

## Problem answer

**Python3**

```python
def solution(participant, completion):
    dict_participant = dict.fromkeys(participant, 0)
    
    for p in participant:
        dict_participant[p] += 1
        
    for c in completion:
        dict_participant[c] -= 1
        
    for k in dict_participant:
        if dict_participant[k] == 1:
            return k
```

**javascript**

```javascript
function solution(participant, completion) {
    // completion.forEach(completion => {
    //     participant.splice(participant.indexOf(completion),1);
    // })
    // return participant[0];
    
    participant.sort()
    completion.sort()
    for(let i in participant) {
        if(participant[i] !== completion[i]) 
            return participant[i];
    }
}
```