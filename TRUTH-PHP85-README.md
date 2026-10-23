# TRUTH PHP 8.5 호환 패치

이번 truth.zip + pg.zip 전용입니다. 그누보드 원본은 5.6.391입니다. 다른 사이트용 ZIP과 혼용하지 마세요. 변경 PHP 파일과 적용 안내만 포함하며 이미지/CSS 등 전체 설치본이 아닙니다.

## 재현한 문제와 수정

- 게시판: pg/head.sub.boa.php 87줄에서 G5_JS_VER 미정의 오류. 코어의 get_versioned_asset_url()을 이용하도록 수정했습니다.
- 메인: 짧은 PHP 태그로 공통 코어가 로딩되지 않아 inc/top.php의 is_member와 index.php의 G5_BBS_PATH 오류. 표준 PHP 태그와 파일 위치 기준 경로로 수정했습니다.
- 공통 코어를 HTML 출력보다 먼저 로딩하고 홈페이지·게시판 상단/하단·메뉴 include를 보완했습니다.
- 구형 매개변수/생성자, 배열 키, 일부 PHP 8.5 자원 해제 및 라이브러리 경고를 수정했습니다.
- 기본 목록 스킨의 누락된 아이콘 값을 보완했습니다.
- 기존 홈페이지의 내용·게시판 분기·화면 구성은 유지했습니다. 이번 원본 inc/link.php에서 comm4는 FAQ가 아니라 실제 게시판으로 연결됩니다. 원본 연결을 그대로 유지했습니다.

## 적용

1. 홈페이지 전체 파일과 DB를 백업합니다.
2. ZIP을 풀어 홈페이지 최상위에 같은 구조로 덮어씁니다. pg/head.php는 기존 pg/head.php에, inc/head.php는 홈페이지 inc/head.php에 들어가야 합니다. ZIP 전체를 pg 안에 넣지 마세요.
3. 사이트 파일을 전체 삭제하지 마세요. pg/data/, DB 설정, 게시글·사진·업로드, CSS/JS/이미지, 인증서·API 키는 유지합니다. DB 구조 변경·초기화·재설치는 필요 없습니다.
4. PHP 8.5에서 메인, word1~4/comm2~6 게시판, 기존 게시글·첨부파일, 로그인·관리자·글 작성/수정을 확인합니다. mysqli, mbstring, GD, cURL, DOM/XML, OpenSSL, ZIP 확장이 필요합니다.
5. 흰 화면이 남으면 해당 시각의 PHP 오류 로그에서 Fatal error/Uncaught 줄(파일 경로·줄 번호 포함)을 확인합니다. 운영 사이트 전체에 오류 내용을 공개하는 설정은 넣지 않았습니다.

## 검증

PHP 8.5.12, short_open_tag=Off, E_ALL에서 검사했습니다.

- 제공된 코어와 격리된 MariaDB 테스트 DB에서 홈페이지·문서 12페이지, 로그인·관리자 메인·회원 목록, 기본/갤러리 스킨의 글 저장·목록·조회·작성 폼.
- gallery_responsive/basic_new/basic_voc 스킨의 목록·조회·작성 폼과 word1~4/comm2~6의 9개 진입 경로.
- 비밀번호, 메일 MIME 생성, HTML 필터, 구형 XLS, PHPExcel XLS/XLSX/PCLZip 생성·읽기·수식, JSON, 캡차, 썸네일, XML 엔티티 차단 등 11개 기능 검사 통과.
- 전체 PHP 구문·컴파일 경고 검사 결과는 truth-php85-validation.txt에 기록했습니다.

운영 DB가 없어 실제 스킨·테마·권한·상단 경로와 모든 게시글/첨부파일 조합은 확인하지 못했습니다. 테스트 DB 설정·계정·데이터는 패치에 포함하지 않았습니다. 실제 메일 전송, 외부 결제/본인인증/SMS/소셜/API, 모든 브라우저·모바일 및 라이브러리 고급 기능은 실서비스 검증하지 않았습니다. 적용 후 운영 환경에서도 확인하세요.

## 로컬 검사

사이트 최상위에서 실행합니다. 검사 도구는 CLI 전용입니다.

```sh
php -d short_open_tag=0 pg/tests/php85/lint.php .
php -d short_open_tag=0 pg/tests/php85/regression.php
```

변경 파일별 SHA-256은 TRUTH-PHP85-manifest.json에 있습니다.
