# 18회 하계 해킹캠프 CTF 풀이
처음 해킹캠프에 갔다. 2위와는 약 900점, 1위와는 2800점 정도 차이로 3등을 했다.
팀에 잘하시는 분도 많이 계셔서 3등을 했던 것같다.
## WEB
### url_routing
다른 문제 2개 풀고 이거만 파다가 잤는데, 결국 못 풀었다. 다음날에 우리팀에 계신 김지섭님에게 풀이를 듣고서야 이해했다.
```php
<?php
    error_reporting(0);
    require __DIR__."/secret.php"; // flag is here

    # parse
    $request_uri = urldecode($_SERVER['REQUEST_URI']);
    $url_query = parse_url('http://example.com/'.$request_uri, PHP_URL_QUERY);
    $parameters = explode("&", $url_query);

    # waf
    foreach($parameters as $param){
        if(stripos($param, 'flag') !== false){
            die('no hack');
        }
    }

    # routes
    switch(isset($_GET['p']) ? strtolower($_GET['p']) : 'home'){
        case 'home':
            highlight_file(__FILE__);
            die;

        case 'author':
            die('safflower');

        case 'flag':
            die($flag);
        
        default:
            die('404 not found');
    }
?>
```
$_GET['p']가 `author`이면 `safflower`을 출력하고, `flag`면 `$flag`를 뱉는다.
그런데, 앞에서 `&`을 기준으로 explode를 하고, 각각을 stripos 함수로 `flag`가 있는지 확인한다.
만약 `flag`라는 `string`이 있다면 `no hack`을 출력하고 종료한다.
여기서 `stripos` 함수는 `strpos`와 달리 "대소문자를 구분"하며 어떤 문자열이 처음으로 나타나는 위치를 반환 해주는 함수이다.

페이로드 부터 말하자면, `http://~~~.kr/?%23=??&p=flag`이다. 이게 가능한 이유는, 
우선 맨 처음에 `urldecode`를 하기 때문에 `?%23=??&p=flag`이 `?#=??&p=flag`가 된후, `parse_url`를 하는데 `parse_url`에서는 fragment(#)뒤로는 무시를 하기 때문이다. 따라서 최종적으로 `$url_query`에는 #뒤가 무시되어 저장된다. 그래서 문자열 필터링은 우회하면서 `$_GET['p']`는 `flag`가 되게 된다.

### SQR
`QR`코드에 SQLi 페이로드를 넣으면 될 것 같았는데, 결국 아직도 못 풀었다.

(계속)