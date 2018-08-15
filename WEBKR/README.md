# webhacking.kr write-up

## Challenge 1
```php
$password="????";
if(eregi("[^0-9,.]",$_COOKIE[user_lv])) $_COOKIE[user_lv]=1;
if($_COOKIE[user_lv]>=6) $_COOKIE[user_lv]=1;
if($_COOKIE[user_lv]>5) @solve();
echo("<br>level : $_COOKIE[user_lv]");
```
`user_lv`가 6 이상이면 `user_lv`가 1로 되돌아가고, `user_lv`가 5보다 크면 풀리게 된다.
5 < `user_lv` < 6 이면 된다는 것이다. `user_lv`가 5.xx면 풀릴 것 같다.
### payload
`document.cookie = "user_lv=5.1"`

## Challenge 18
```php
if(eregi(" |/|\(|\)|\t|\||&|union|select|from|0x",$_GET[no])) exit("no hack"); 
$q=@mysql_fetch_array(mysql_query("select id from challenge18_table where id='guest' and no=$_GET[no]")); 
if($q[0]=="guest") echo ("hi guest"); 
if($q[0]=="admin") { 
    @solve(); 
    echo ("hi admin!"); 
} 12
```


## Challenge 23
`Your mission is to inject <script>alert(1);</script>`이라고 한다.
그냥 GET으로 넘길 때 code값 맨 앞에 NULL(%00)을 추가해 주면 풀린다.
### payload
`http://webhacking.kr/challenge/bonus/bonus-3/index.php?code=%00<script>alert(1);</script>`

## Challenge 58
문제 페이지에 들어가면 플래시로 되어있는 로그인 창이 뜬다. 게싱으로 몇 가지 패스워드를 넣어봤지만 되지 않아서 플래시 파일을 다운로드 받은뒤 iHex로 열었다. 파일 맨 뒷 부분에 보면 `http://webhacking.kr/challenge/web/web-35/g1v2m2passw0rd.php`이 있다. 들어가면 문제가 풀린다!