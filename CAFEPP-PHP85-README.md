# CAFEPP PHP 8.5 호환 수정 패치

이번 cafepp.zip + pg.zip 전용입니다. 그누보드 원본은 5.6.391입니다. 변경 PHP 파일과 안내만 포함하며 이미지/CSS 등 전체 설치본이 아닙니다.

## 재현한 문제와 수정

- 원본 메인에서 짧은 PHP 태그 때문에 공통 코어가 로딩되지 않아 index.php 5줄 G5_BBS_PATH 미정의 오류를 재현했습니다.
- 원본 게시판에서 pg/head.sub.boa.php 63줄 G5_CSS_VER 미정의 오류를 재현했습니다. 같은 파일의 G5_JS_VER와 함께 기존 코어의 get_versioned_asset_url()로 처리했습니다.
- 표준 PHP 태그로 변경하고 공통 코어를 화면 출력 전에 불러오며, 홈페이지 하위 페이지와 게시판 상단/하단/메뉴의 연결 경로를 파일 위치 기준으로 보완했습니다.
- PHP 8.5의 구형 생성자/매개변수/배열 키/일부 라이브러리 경고를 수정했습니다.
- 기본 목록 계열의 누락 아이콘, 반응형 작성 폼의 빈 유튜브 ID와 문의 작성 폼의 없는 분류 값에 기본값을 적용했습니다.
- 기존 제품 소개·도입 안내·화면·게시판 분기를 유지했습니다.

## 적용 방법

1. 홈페이지 전체 파일과 DB를 백업합니다.
2. ZIP을 풀어 홈페이지 최상위에 같은 구조로 덮어씁니다. pg/head.php는 기존 pg/head.php에, inc/head.php는 홈페이지 inc/head.php에 들어가야 합니다. ZIP 전체를 pg 안에 넣지 마세요.
3. 사이트 파일을 전체 삭제하지 마세요. pg/data/, DB 설정, 게시글·첨부·사진, 제품 자료, CSS/JS/이미지, 인증서·API 키는 유지합니다. DB 구조 변경·초기화·재설치는 필요 없습니다.
4. PHP 8.5에서 메인, 제품·솔루션·창업안내, 설치사례·문의·견적·프로모션 게시판, 로그인·관리자, 기존 글·첨부파일과 글 작성을 확인합니다. mysqli, mbstring, GD, cURL, DOM/XML, OpenSSL, ZIP 확장이 필요합니다.
5. 흰 화면이 남으면 해당 시각 PHP 오류 로그의 Fatal error/Uncaught 줄(경로·줄 번호 포함)을 확인합니다. 운영 사이트 전체에 오류 내용을 공개하는 설정은 넣지 않았습니다.

## 검증

PHP 8.5.12 / short_open_tag=Off / E_ALL로 검사했습니다.

- 제공된 코어와 격리된 MariaDB 테스트 DB에서 홈페이지·하위 페이지 31개, 로그인·관리자 메인·회원 목록, 기본/갤러리 스킨의 저장·목록·조회·작성 폼을 확인했습니다.
- gallery_responsive/basic_new/basic_voc/basic_new_voc/basic_new_voc2 스킨의 목록·조회·작성 폼과 cases/callback/estimate/promotions 게시판 진입 경로를 확인했습니다.
- 비밀번호, 메일 MIME 생성, HTML 필터, 구형 XLS, PHPExcel XLS/XLSX/PCLZip 생성·읽기·수식, JSON, 캡차, 썸네일, XML 엔티티 차단 등 11개 기능 검사 통과.
- 전체 PHP 구문·컴파일 경고 검사 결과는 cafepp-php85-validation.txt에 기록했습니다.

운영 DB는 제공되지 않아 실제 스킨·테마·권한·상단 경로·문의 항목과 모든 데이터 조합을 확인하지 못했습니다. 테스트 DB 설정·계정·데이터는 패치에 포함하지 않았습니다. 문의/견적의 실제 통지·메일 전송, 외부 결제/인증/SMS/소셜/API, 모든 브라우저/모바일 화면과 라이브러리 고급 기능은 실서비스 검증하지 않았습니다. 적용 후 운영 환경에서도 확인하세요.

## 재검사

사이트 최상위에서 실행합니다. 검사 도구는 CLI 전용입니다.

```sh
php -d short_open_tag=0 pg/tests/php85/lint.php .
php -d short_open_tag=0 pg/tests/php85/regression.php
```

파일별 SHA-256은 CAFEPP-PHP85-manifest.json에 기록했습니다.
