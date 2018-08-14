# webhacking.kr write up
블로그가 너무 느려서 마크다운으로 갈아탔다

## prob 23
![prob23](./img/prob23.png)<br>
`Your mission is to inject <script>alert(1);</script>`이라고 한다.
그냥 GET으로 넘길 때 code값 맨 앞에 NULL(%00)을 추가해 주면 풀린다.
