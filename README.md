# MS24 PHP 8.5 호환 수정 패치

- [MS24 수정 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/ms24-php85-patch.zip)
- [적용 방법과 검증 범위](MS24-PHP85-README.md)
- [검증 결과](ms24-php85-validation.txt)

이번 ms24.zip + pg.zip 전용입니다. 그누보드 원본은 5.6.4이며 최신글 함수·HTML 필터·썸네일·스킨의 PHP 8.5 경고와 짧은 PHP 태그/연결 경로를 수정했습니다. 홈페이지 46개와 pg 166개 변경 PHP 파일을 담았습니다. **백업 후 홈페이지 최상위에 같은 구조로 덮어쓰세요. 전체 삭제하지 말고 data/·DB 설정·업로드·이미지·인증서는 유지하세요.** PHP 1,593개 구문 검사와 홈페이지/문서 41페이지, 로그인·관리자·게시판 및 라이브러리 11개 검사가 통과했습니다. 운영 DB와 외부 서비스는 실서비스 검증하지 않았습니다.

---

# GYC PHP 8.5 호환 수정 패치

- [GYC 수정 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/gyc-php85-patch.zip)
- [적용 방법과 검증 범위](GYC-PHP85-README.md)
- [검증 결과](gyc-php85-validation.txt)

이번 gyc.zip + pg.zip 전용입니다. 게시판의 버전 상수 오류와 메인의 짧은 PHP 태그 문제를 재현·수정했습니다. 홈페이지 32개와 pg 199개 PHP 변경 파일을 담았습니다. **백업 후 홈페이지 최상위에 같은 구조로 덮어쓰세요. 전체 삭제하지 말고 data/·DB 설정·업로드·제품 자료·이미지·인증서는 유지하세요.** DB 재설치는 필요 없습니다. PHP 1,709개 구문 검사, 홈페이지/문서 13개, 로그인·관리자·게시판·제품/카탈로그 스킨과 라이브러리 11개 검사가 통과했습니다. 운영 DB와 외부 서비스는 실서비스 검증하지 않았습니다.

---

# 칠곡경북대학교병원 권역호스피스센터 PHP 8.5 패치

- [knuhhospice 수정 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/knuhhospice-php85-patch.zip)
- [적용 방법과 검증 범위](KNUHHOSPICE-PHP85-README.md)

이번 knuhhospice.zip + pg.zip 전용입니다. 원본 그누보드는 5.4.5.5이며 짧은 태그, DB 예외 및 게시판 출력 문자열 처리 오류를 재현·수정했습니다. 홈페이지 60개와 pg 155개 PHP 변경 파일을 담았습니다. **백업 후 홈페이지 최상위에 같은 구조로 덮어쓰세요. 전체 삭제하지 말고 data/·DB 설정·이미지·인증서는 유지하세요.** DB 재설치는 필요 없습니다. PHP 1,052개 구문 검사와 홈페이지/문서 45개, 로그인·관리자·게시판 및 라이브러리 11개 검사를 통과했습니다. 운영 DB와 외부 서비스는 실서비스 검증하지 않았습니다.

---

# 또이스 게시판 흰 화면 수정 패치

- [또이스 변경 파일 8개 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/ttois-board-php85-patch.zip)
- [원인과 적용 안내](TTOIS-BOARD-PHP85-README.md)

이번 ttois.zip + pg.zip 전용입니다. 게시판 전용 head.sub.boa.php:63에서 G5_CSS_VER 미정의 오류를 재현하고, 같은 파일의 G5_JS_VER 및 게시판 연결 경로·메뉴 태그를 수정했습니다. 백업 후 홈페이지 최상위에 같은 구조로 덮어쓰세요. 전체 삭제나 DB 재설치는 필요 없습니다. PHP 8.5.12에서 변경 파일 구문 검사, 홈페이지·게시판 목록·로그인·글 저장·조회·작성 폼을 확인했습니다. 운영 DB 설정은 제공받지 않아 테스트 게시판 설정으로 검증했습니다.

---

# map_basic 변경 파일만 포함한 PHP 8.5 패치

- [map_basic 변경 파일 6개 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/map_basic-php85-changed-only.zip)
- [변경 파일 목록](map_basic-php85-changed-only-files.txt)

마지막으로 첨부한 map_basic.zip 원본을 기준으로 PHP 8.5 호환 수정한 파일만 담았습니다. 기존 map_basic 스킨 폴더를 백업한 뒤 ZIP 안 PHP 파일 6개를 해당 폴더(예: pg/skin/board/map_basic/)에 덮어쓰세요. 기존 이미지·CSS·댓글 파일은 유지합니다. 이전 map_basic2 스킨이나 다른 사이트 전체에 덮어쓰는 파일이 아닙니다. 기존 지도 중심 화면, 카카오톡 채널과 본문 편집기는 유지했습니다.

PHP 8.5.12, short_open_tag=Off/E_ALL에서 전체 스킨 PHP 7개 구문 검사 통과. 격리된 그누보드 5.6.391/MariaDB에서 목록·조회·저장·수정 폼과 네 번째 링크 저장, 대체 목록 2개, 생성 JavaScript 문법을 확인했습니다. 실제 카카오 API·운영 DB는 실서비스 검증하지 않았습니다. 기존 wr_12·wr_15·wr_16·wr_17 DB 필드와 API 키 설정은 유지해야 하며 DB 구조를 자동 변경하지 않습니다.

---

# map_basic2 두 번째 첨부본 PHP 8.5 수정

- [이번 첨부본 수정 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/map_basic2-php85-v2.zip)
- [적용 안내 및 DB 필드·검증 범위](MAP-BASIC2-PHP85-V2-README.md)

두 번째 map_basic2.zip 전용입니다. 카카오톡 채널을 포함한 링크 4개, 본문 편집기와 소개 영역을 유지했습니다. 기존 스킨과 DB를 백업한 뒤 map_basic2/ 파일을 pg/skin/board/map_basic2/에 덮어쓰세요. 이번 원본은 사용자 정의 DB 필드를 전제로 하며 DB 구조를 자동 변경하지 않습니다.

---

# map_basic2 PHP 8.5 호환 스킨

- [map_basic2 수정 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/map_basic2-php85.zip)
- [적용 방법과 검증 범위](MAP-BASIC2-PHP85-README.md)

이번에 첨부한 map_basic2.zip 전용 전체 스킨입니다. 백업 후 ZIP의 map_basic2/ 내용을 기존 pg/skin/board/map_basic2/에 덮어쓰세요. PHP 8.5에서 목록·조회·저장·수정 폼과 생성 JavaScript 문법을 검사했습니다. 실제 카카오 지도 API는 별도 확인이 필요합니다. 홈페이지/코어 전체 패치는 아래에서 사이트별로 구분하세요.

---

# 더조은의정 갤러리 흰 화면 / PHP 8.5 수정 패치

- [더조은의정 수정 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/thejecti-php85-patch.zip)
- [적용 방법·재현 오류·검증 범위](THEJECTI-PHP85-README.md)

이번 thejecti.zip + pg.zip 전용입니다. 갤러리에서 G5_CSS_VER 미정의 오류와 홈페이지의 짧은 PHP 태그 문제를 재현·수정했습니다. 홈페이지 16개, pg 203개 PHP 변경 파일을 담았습니다. **백업 후 홈페이지 최상위에 같은 구조로 덮어쓰세요. 전체 삭제하지 말고 data/·DB 설정·이미지·인증서는 보존하세요.** 아래 rene/msrh24/BL 패치와는 다른 사이트용입니다.

---

# RENE + pg PHP 8.5 통합 패치

- [수정 파일 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/rene-pg-php85-patch.zip)
- [적용 안내와 검증 범위](RENE-PG-PHP85-README.md)

제공된 rene.zip + pg.zip 기준입니다. 홈페이지 57개, pg 225개 PHP 변경 파일(검사 도구 포함)을 담았습니다. **전체 설치본이 아닙니다. 백업 후 홈페이지 최상위 경로에 덮어쓰고 기존 data/·DB 설정·업로드·인증서는 보존하세요. 기존 사이트 전체를 삭제하지 마세요.** 이전 rene 수정사항도 포함합니다. pg의 버전은 5.6.391입니다. 실제 외부 결제·인증·문자 연동은 별도 확인이 필요합니다.

---

# RENE 의원 홈페이지 PHP 8.5 수정본

- [rene 수정본 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/rene-php85.zip)
- [RENE 적용 안내 및 검증 범위](RENE-PHP85-README.md)

첨부된 rene.zip 범위의 파일 전체를 담은 수정본입니다. **pg/는 제외했으며, 기존 사이트를 삭제하지 말고 동일 경로로 덮어쓰세요.** 아래의 BL 주차관리 패치와는 별도 파일입니다.

---

# MSRH24 병원 홈페이지 PHP 8.5 수정본

- [msrh24 수정본 ZIP 다운로드](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/msrh24-php85.zip)
- [MSRH24 적용 안내 및 검증 범위](MSRH24-PHP85-README.md)

첨부된 msrh24.zip 범위의 파일 전체를 담은 수정본입니다. **pg/는 제외했으며, 기존 사이트를 삭제하지 말고 동일 경로로 덮어쓰세요.** 아래의 BL 주차관리 패치와는 별도 파일입니다.

---

# 그누보드 5.4.2.7 · BL 주차관리 PHP 8.5 호환 패치

이 브랜치는 제공된 `pk.tar`에 적용할 **수정 파일 패치**를 배포합니다. 전체 신규 설치용 소스가 아닙니다.

## 다운로드

[수정 파일 ZIP 받기](https://github.com/webtro2/blparking/raw/refs/heads/php85-compat/blparking-php85-patch.zip)

파일 페이지에서 다운로드 버튼으로 받을 수도 있습니다.

## 적용

1. 기존 사이트 파일과 DB를 백업하고 복제한 테스트 사이트에서 먼저 확인하세요.
2. `blparking-php85-patch.zip`을 내려받아 풀고, 기존 사이트 최상위에 같은 경로로 덮어씁니다.
3. 기존 `data/dbconfig.php` 및 업로드 자료를 유지합니다. 기존 사이트에서 설치 프로그램을 다시 실행하지 마세요.
4. OPcache를 갱신하고 주요 업무를 확인합니다.

자세한 변경 사항, PHP 확장 요구사항, 테스트 방법은 [PHP85-MIGRATION.md](PHP85-MIGRATION.md)를 참조하세요.

## 검증

PHP 8.5.12에서 원본 PHP 854개와 추가 CLI 검사 스크립트 2개 문법 검사 통과. 회귀 테스트 8개 통과.
별도 MariaDB 10.11에서 로그인·관리자·게시글 저장/조회 및 주차 등록 → 출차 → 정리 흐름을 확인했습니다.
운영 DB와 실제 결제·SMS·소셜 로그인 연동은 별도 검증이 필요합니다.

이 브랜치에는 DB 설정, 운영 DB, 업로드 자료, 세션 파일을 포함하지 않았습니다.
