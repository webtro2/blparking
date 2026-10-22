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
