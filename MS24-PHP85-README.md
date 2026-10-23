# MS24 PHP 8.5 호환 패치

이번 ms24.zip + pg.zip 전용 변경 파일 패치입니다. 원본 그누보드 버전은 5.6.4입니다. 앞서 제공한 msrh24 등 다른 ZIP용 패치와 혼용하지 마세요. 이미지·CSS 등을 포함한 전체 설치본이 아닙니다.

## 수정 내용

- 짧은 PHP 태그, 구형 생성자·매개변수와 PHP 8.5에서 경고가 발생하는 일부 라이브러리 코드를 수정했습니다.
- 원본에서 latest()의 선택 매개변수가 필수 매개변수보다 먼저 선언된 경고, HTML 필터의 동적 속성 경고, 썸네일 imagedestroy() 경고를 재현했습니다.
- 공통 코어를 HTML 출력 전에 실행하고 홈페이지·게시판 include 경로를 파일 위치 기준으로 정리했습니다.
- 반응형 작성 스킨에서 없는 유튜브 ID, 기본 목록에서 없는 아이콘 값에 기본값을 적용했습니다.
- DB 결과와 일부 자원 해제 처리, switch 내부의 continue 경고를 보완했습니다.
- 기존 홈페이지 내용과 디자인, 로그인 메뉴·게시판 분기와 DB 구조는 유지했습니다.
- 이 원본은 extend/version.extend.php에서 버전 상수를 정의합니다. 다른 사이트의 버전 상수 오류로 단정해서 변경하지 않았습니다.

## 적용 방법

1. 홈페이지 전체 파일과 DB를 백업합니다.
2. ZIP을 풀어 홈페이지 최상위에 같은 구조로 덮어씁니다. pg/lib/common.lib.php는 기존 pg/lib/common.lib.php에, inc/head.php는 홈페이지 inc/head.php에 들어가야 합니다. ZIP 전체를 pg 안에 넣지 마세요.
3. 사이트를 전체 삭제하지 마세요. pg/data/, DB 설정, 게시글·업로드·사진, CSS·JS·이미지, 인증서·API 키는 유지합니다. DB 초기화·구조 변경·재설치는 필요 없습니다.
4. PHP 8.5에서 홈페이지, 소개/후기/고객센터 게시판, 기존 게시글·첨부파일, 로그인·관리자, 글 작성/수정을 확인합니다. mysqli, mbstring, GD, cURL, DOM/XML, OpenSSL, ZIP 확장이 필요합니다.
5. 흰 화면이 남으면 해당 시각의 PHP 오류 로그에서 Fatal error/Uncaught 줄(파일 경로·줄 번호 포함)을 확인합니다. 오류 내용을 운영 화면 전체에 공개하는 설정은 넣지 않았습니다.

## 검증과 한계

PHP 8.5.12 / short_open_tag=Off / E_ALL에서 다음을 검사했습니다.

- 별도 MariaDB 테스트 DB와 제공 코어에서 홈페이지·문서 41페이지, 로그인·관리자 메인·회원 목록.
- 기본/갤러리 스킨의 글 저장·목록·조회·작성 폼.
- gallery_responsive/basic_new/basic_voc 스킨의 목록·조회·작성 폼과 intro4/intro5/review1/review2/comm1/comm2/comm3 진입 경로.
- 비밀번호, 메일 MIME 생성, HTML 필터, 구형 XLS, PHPExcel XLS/XLSX/PCLZip 생성·읽기·수식, JSON, 캡차, 썸네일, XML 엔티티 차단 등 11개 기능 검사 통과.
- 전체 PHP 구문·컴파일 경고 검사 결과는 게시한 ms24-php85-validation.txt에 기록했습니다.

운영 DB는 제공되지 않아 실제 게시판의 스킨·테마·권한·상단 파일·여분필드와 모든 데이터 조합은 확인하지 못했습니다. 테스트 계정·DB 설정·데이터는 포함하지 않았습니다. 외부 결제/인증/SMS/소셜/API, 실제 메일 발송, 모든 브라우저·모바일 화면과 라이브러리 고급 기능은 실서비스 검증하지 않았습니다. 적용 후 운영 환경에서도 확인하세요.

## 로컬 검사

사이트 최상위에서 실행합니다. 검사 도구는 CLI 전용입니다.

```sh
php -d short_open_tag=0 pg/tests/php85/lint.php .
php -d short_open_tag=0 pg/tests/php85/regression.php
```

변경 파일별 SHA-256은 MS24-PHP85-manifest.json에 있습니다.
