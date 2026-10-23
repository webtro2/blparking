# 게시판 본문 동기화 누락 수정

이번에 제공한 pg.zip의 bbs/write.php와 basic_new.zip을 기준으로 확인했습니다.
pg/bbs/write.php에서 editor_js를 빈 문자열로 시작해 get_editor_js() 호출이 빠져 있었습니다. CHEditor의 화면상 본문이 실제 name=wr_content인 전송 textarea로 복사되지 않아 서버가 빈 내용을 받으면 내용 입력 경고가 발생합니다. 일반 textarea/SmartEditor2에서도 초기화 변수가 빠져 검사 JavaScript 오류가 발생할 수 있습니다.

## 변경

한 줄만 변경했습니다.

```php
$editor_js = get_editor_js('wr_content', $is_dhtml_editor);
```

기존 내용 필수 검사, 상품/프로젝트 게시판 예외, 캡차·금지단어·글쓰기 토큰과 서버 검사는 유지합니다. basic_new 스킨의 디자인이나 파일은 변경하지 않았습니다.

## 적용

이 수정본은 이번 첨부 pg.zip 전용입니다. 다른 사이트의 write.php에는 별도 사용자 수정이 있을 수 있으므로 통째로 혼용하지 마세요.
기존 pg/bbs/write.php를 백업한 뒤 ZIP의 pg/bbs/write.php를 같은 경로에 덮어씁니다. 홈페이지 최상위 기준 폴더 구조입니다. 새로 글쓰기 페이지를 열어 내용을 입력하고 등록하세요. 다른 파일 삭제/DB 재설치는 필요 없습니다.
다른 변경사항이 있는 서버라면 파일 전체 대신 해당 editor_js 초기화 한 줄만 수동 반영하세요.

## 확인

PHP 8.5 구문 검사 통과. 실제 첨부된 editor.lib.php와 플러그인의 get_editor_js/chk_editor_js가 생성한 코드를 사용해 일반 textarea, SmartEditor2, CHEditor의 일반/상품 게시판과 빈/채운 본문 20개 조합을 Node VM에서 확인했습니다. 본문 전송 필드 동기화와 일반 게시판 빈 본문 거부, 상품 게시판 기존 예외를 확인했습니다. 실제 운영 브라우저·DB 등록은 이 검사에 포함하지 않았습니다.
적용 후에도 같으면 사용하는 편집기 이름, 게시판 주소, 경고 문구 및 브라우저 개발자도구 Console/Network의 오류를 확인해야 합니다.
