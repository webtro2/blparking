# GYC PHP 8.5 호환 패치

이번 gyc.zip + pg.zip 전용입니다. 원본 그누보드는 5.6.391입니다. 다른 사이트용 패치와 혼용하지 마세요.
홈페이지 32개, pg 199개(검사 도구 2개 포함)의 변경 PHP 파일만 담았습니다. 전체 설치본이 아닙니다.

## 원인과 수정

원본 파일을 PHP 8.5.12에서 실행해 다음 오류를 재현했습니다.

- 게시판: pg/head.sub.boa.php 63줄 Undefined constant G5_CSS_VER. 같은 파일의 G5_JS_VER도 현재 코어에서 제공하는 get_versioned_asset_url()로 변경했습니다.
- 홈페이지: 짧은 PHP 태그로 코어가 로딩되지 않아 index.php 6줄 Undefined constant G5_BBS_PATH. 표준 태그와 파일 위치 기준 경로로 수정했습니다.

홈페이지 출력 전에 공통 코어를 실행하도록 정리하고, 게시판의 상단/하단 및 메뉴 include 경로를 보완했습니다. 짧은 태그, 배열 키, 구형 생성자/매개변수, 일부 라이브러리의 PHP 8.5 경고를 수정했습니다. 기본 목록 스킨의 누락 아이콘 값을 보완했습니다. 제품·카탈로그·홈페이지의 기존 내용과 게시판 분기는 유지했습니다.

## 적용

1. 사이트 파일 전체와 DB를 백업합니다.
2. ZIP을 풀어 홈페이지 최상위에 같은 구조로 덮어씁니다. pg/head.php는 기존 pg/head.php에, inc/head.php는 홈페이지 inc/head.php에 들어가야 합니다. ZIP 전체를 pg 안에 넣지 마세요.
3. 사이트 파일을 전체 삭제하지 마세요. pg/data/, DB 연결 설정, 게시글·업로드·사진·제품/인증서 자료, 기존 이미지·CSS·JS, API 키는 유지합니다. DB 구조 변경·초기화·재설치는 필요 없습니다.
4. 홈페이지와 고객센터, 제품별 게시판, 카탈로그, 로그인·관리자, 글 작성·조회·첨부파일을 확인합니다. PHP 8.5에 mysqli, mbstring, GD, cURL, DOM/XML, OpenSSL, ZIP 확장이 필요합니다.
5. 적용 후에도 흰 화면이면 해당 시간의 PHP 오류 로그 중 Fatal error/Uncaught 줄(경로와 줄 번호 포함)을 확인합니다. 운영 사이트에 오류 내용을 공개하는 설정은 넣지 않았습니다.

## 검증 범위

- PHP 8.5.12, short_open_tag=Off, E_ALL로 검사했습니다.
- 별도 MariaDB 테스트 DB와 제공된 코어에서 홈페이지·문서 13페이지, 로그인·관리자 메인·회원 목록, 기본/갤러리 스킨의 글 저장·목록·조회·작성 폼을 확인했습니다.
- catalog, gallery_responsive, gallery_responsive2, basic_new 스킨의 목록·조회·작성 폼 및 comm1~3/product1~6/e_catalog 진입 경로를 테스트 게시판 설정으로 확인했습니다.
- 비밀번호, 메일 MIME 생성, HTML 필터, 구형 XLS, PHPExcel XLS/XLSX/PCLZip 생성·읽기·수식, JSON, 캡차, 썸네일, XML 엔티티 차단 등 11개 기능 검사 통과.
- PHP 전체 구문·컴파일 경고 검사 결과는 함께 게시한 검증 결과 파일에 기록했습니다.
- 운영 DB는 제공되지 않아 실제 스킨·테마·권한·상단 경로·제품별 여분필드와 모든 데이터 조합은 확인하지 못했습니다. 테스트 DB/계정/설정/데이터는 패치에 포함하지 않았습니다.
- 문의 메일의 실제 발송, 외부 결제/인증/SMS/소셜/API, 모든 브라우저·모바일 화면 및 라이브러리의 모든 고급 기능을 실서비스 검증한 것은 아닙니다. 적용 후 운영 환경에서도 확인하세요.

## 로컬 검사

사이트 최상위에서 실행합니다. 검사 도구는 CLI 전용입니다.

```sh
php -d short_open_tag=0 pg/tests/php85/lint.php .
php -d short_open_tag=0 pg/tests/php85/regression.php
```

파일별 SHA-256은 GYC-PHP85-manifest.json에 있습니다.
