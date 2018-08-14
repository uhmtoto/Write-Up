# DIMICTF 2018 예선
1330p로 24위를 했다!
작년엔 예선 10위, 본선 3위였는데 많이 떨어졌다ㅠㅠ
## misc
### MIC CHECK (560p)
마이크 테스트 문제다.
```
Can you speak?
FLAG: dimi{Hello, DIMIGO!}
```
FLAG: `dimi{Hello, DIMIGO!}`

## reversing
### EZPZ (770p)
문제파일을 받고 실행시키면 입력창과 GO버튼만 나오고 최소화되서 아무것도 할 수 없다.
PEID로 확인해보니까 .NET이라길래 닷픽으로 풀었다.
```
if (string.Compare(this.INPUT.Text, "Welcome_reversing") != 0)
    return;
int num = (int) MessageBox.Show("dimi{" + this.INPUT.Text + "}");
```
이런 코드가 있는데, 
`INPUT.Text`의 값이 `Welcome_reversing`이라면 `dimi{}`안에 끼워서 출력해주는 것 같다.
FLAG: `dimi{Welcome_reversing}`