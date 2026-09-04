# HeCS-omnibus 웹페이지 설계도

> 근거: `reference/` 논문 9편 (CIRS 2006 → HeCS 2013 → HeCS-SZ 2016 → HeCS-red 2018 → **HeCS-omnibus 2020** → VDF 2020 / Pizzardo 2021 / Logan 2022 → **Park 2026 (MACH)**).
> 사이트 언어: 영어. 데이터 접근: `http://147.46.135.40:3000/sharing/va94quU2B`

---

## 0. 한 줄 정체성

**HeCS-omnibus** = MMT/Hectospec + SDSS 분광으로 만든, 국소우주(0.02 < z < 0.30) 은하단 **227개 / 분광 멤버 52,325개**의 통합 카탈로그.
**MACH** = 그 중 가장 무겁고 가장 촘촘하게 관측된 9개 은하단의 심층 분광 서브셋 (Park et al. 2026).

사이트는 "데이터 릴리즈 페이지 + 서베이 소개" 성격. 홈에서 두 가지(omnibus 전체, MACH 서브셋)가 바로 보이게.

---

## 1. 사이트 맵

```
/                      Home        — 히어로 + 핵심 숫자 + 두 갈래(omnibus / MACH) 진입
/survey/               Survey      — 계보(CIRS→HeCS→SZ→red→omnibus), 관측·분석 방법
/mach/                 MACH ★      — 9개 은하단, 완결성, SMF 결과 (Park 2026 강조)
/data/                 Data        — 카탈로그 설명 + 외부 링크(147.46.135.40 공유 링크, VizieR, Dataverse)
/publications/         Publications— 핵심 논문 + 활용 논문
/team/                 Team        — (내용은 사용자 확인 필요)
```

단일 페이지(스크롤 앵커)로 시작해도 되고, 나중에 다중 페이지로 분리 가능. **1차 구현은 단일 `index.html` + 앵커** 추천 (빌드 도구 없이 push만으로 배포되는 지금 구조와 맞음).

---

## 2. 페이지별 글감

### 2.1 Home

**Hero**
- 타이틀: `HeCS-omnibus`
- 부제: *A spectroscopic compilation of 227 galaxy clusters in the local universe*
- 한 줄: *Built from MMT/Hectospec and SDSS spectroscopy, HeCS-omnibus provides caustic-based membership, dynamical masses, and galaxy properties for clusters at 0.02 < z < 0.30.*
- CTA 버튼 2개: **Get the data** (→ /data) / **Explore MACH** (→ /mach)

**Key numbers (stat tiles)**
| 값 | 라벨 | 출처 |
|---|---|---|
| 227 | galaxy clusters | Sohn+20 |
| 52,325 | spectroscopic members | Sohn+20 |
| 0.02 – 0.30 | redshift range | Sohn+20 |
| ~180 | median members per cluster (range 16 – 1209) | Sohn+20 §3.1 |
| 220 | BCGs identified | Sohn+20 §3.3 |
| 9 | MACH clusters, >4,500 spectra each | Park+26 |

**Two-track cards**
- *HeCS-omnibus* — "The full compilation: cluster properties (σ_cl, R200, M200), member catalogs, BCG catalog."
- *MACH* — "The Massive Cluster Survey with Hectospec: the nine most massive local clusters (0.07 < z < 0.11), spectroscopically complete to r ≈ 20.6–21.1."

**What's in the catalog (짧은 리스트)**
- Cluster table: ID, RA/Dec, z, N_mem(caustic), N_mem(<R200), σ_cl, R200, M200
- BCG table: SDSS objID, RA/Dec, z, r_petro, log M*, σ_*, D_n4000
- Member galaxies: redshift, D_n4000, stellar mass (Le Phare), central stellar velocity dispersion (aperture-corrected to 3 kpc)

---

### 2.2 Survey (계보 + 방법)

**Lineage timeline** (가로 타임라인 그래픽 추천)

| 연도 | 서베이 | 선택 기준 | 은하단 수 (omnibus 기여) | z | 논문 |
|---|---|---|---|---|---|
| 2006 | **CIRS** | X-ray flux, SDSS DR4 분광 | 74 (71) | 0.02–0.10 | Rines & Diaferio 2006 |
| 2013 | **HeCS** | X-ray flux, MMT/Hectospec | 58 (58) | 0.10–0.29 | Rines+2013 |
| 2016 | **HeCS-SZ** | Planck SZ | 123 (50 unique) | 0.02–0.20 | Rines+2016 |
| 2018 | **HeCS-red** | redMaPPer λ > 64 | 27 (23) | 0.10–0.26 | Rines+2018 |
| — | HeCS-faint | low L_X (< 5×10⁴³ erg/s) | 16 (12) | 0.04–0.17 | Rines+2020 |
| — | ACReS | LoCuSS clusters | 31 (8) | 0.16–0.29 | Haines+2013 |
| — | other Hectospec | A68, A611, A1703, A2537, A2457 | 5 | 0.05–0.28 | — |
| **2020** | **HeCS-omnibus** | 위 전부 통합 + SDSS DR14 | **227** | **0.02–0.29** | Sohn+2020 |
| 2017–23 obs / 2026 | **MACH** | omnibus 중 가장 무거운 9개 | 9 | 0.07–0.11 | Park+2026 |

(표 출처: Sohn+20 Table 1 "The Origin of the HeCS-omnibus Sample")

**Each survey in one paragraph** (글감)
- *CIRS*: SDSS DR4로 X-ray 선택 은하단 72개의 infall pattern 확인, caustic mass profile 최초 대규모 샘플. 턴어라운드 반경 내 질량 ≈ 2.19 ± 0.18 × M_vir.
- *HeCS*: MMT/Hectospec으로 58개 X-ray 은하단, 은하단당 ~200 멤버. "Ultimate halo mass" ≈ (1.99 ± 0.11) M200. NFW profile이 infall region까지 잘 맞음.
- *HeCS-SZ*: Planck SZ 선택 은하단의 속도분산–SZ 질량 관계. SZ 질량 편향이 작음 → Planck 은하단/CMB 긴장은 SZ bias로 해결 안 됨. velocity bias 작음.
- *HeCS-red*: redMaPPer 고richness 은하단이 실제 rich cluster임을 분광으로 확인. σ_p–λ 관계에 24% intrinsic scatter. photo-z 약간 과대(Δz = −0.0028).
- *HeCS-omnibus*: 위 전부를 SDSS DR14 + Hectospec 아카이브(HSRed v2.0, RVSAO R_XC > 3)로 균질 재처리. BCG 220개 식별, σ_*,BCG–σ_cl 관계가 매우 tight; σ_*,BCG/σ_cl이 σ_cl 증가에 따라 감소 → 저질량 헤일로에서 BCG 형성 효율이 높음(Dolag+10 시뮬 예측과 다름).

**Methods (아코디언/짧은 카드)**
- *Spectroscopy*: Hectospec 300-fiber, 1° FOV, 3700–9100 Å, R~1500–1700; SDSS r < 17.77 (R~2000, δz ~ 7 km/s); 일부 OmegaWINGS/ACReS/NED/DESI 보충.
- *Membership*: caustic technique (Diaferio & Geller 1997; Diaferio 1999). 시뮬 기준 멤버 ~90% 회수, 인터로퍼 < 8% (N_mem > 50).
- *Cluster properties*: caustic M200/R200; bi-weight σ_cl within R200, 10,000 bootstrap 오차.
- *Galaxy properties*: Le Phare 항성질량(BC03, Chabrier IMF), D_n4000 (Balogh+99 정의), 항성속도분산(SDSS Portsmouth pPXF ↔ Hectospec ULySS, aperture correction β = −0.059, 3 kpc 기준).
- *BCG identification*: r-band 최밝 + R_cl < 0.5 R200 + 시각 검사(SDSS DR14 cModel 광도 문제로 ~25개 수정).

---

### 2.3 MACH ★ (강조 섹션)

**Header**
- `MACH — MAssive Cluster survey with Hectospec`
- 부제: *Deep, dense, complete spectroscopy of the nine most massive clusters in the local universe*
- 한 줄: *MACH targets the most massive, best-sampled clusters in HeCS-omnibus at 0.07 < z < 0.11 — a redshift window chosen so that R200 fits inside the 1° Hectospec field. Observed 2017–2023, 41,897 unique Hectospec spectra, no color selection.*

**Why MACH (3 포인트)**
1. **Complete** — 은하단당 4,500+ 스펙트럼, 90% 완결성 한계 r ≈ 20.1–21.1 (Table 1). 색 선택 없음 → quiescent/star-forming 모두 동일 깊이.
2. **Massive** — M200 = 5.5×10¹⁴ – 1.0×10¹⁵ M☉ (typical 7.4×10¹⁴). HeCS-omnibus M200–N_spec 평면에서 우상단 박스(Park+26 Fig. 1).
3. **Deep** — SMF를 log M* ≳ 8.5까지, 보정 없이 log M* > 9 완결. SDSS field(log M* ≳ 10.5)보다 2 dex 깊음.

**The nine clusters (표 — Park+26 Table 1 & 2 합침)**

| ID | z | N_spec | N_spec(<R200) | N_mem | N_mem(<R200) | R200 (Mpc) | log M200 | r_comp |
|---|---|---|---|---|---|---|---|---|
| A2245 | 0.088 | 39,270 | 1,390 | 548 | 312 | 1.65 | 14.74 | 20.875 |
| A1767 | 0.071 | 13,394 | 1,840 | 668 | 377 | 1.70 | 14.78 | 20.875 |
| A2244 | 0.099 | 39,129 | 1,319 | 748 | 364 | 1.72 | 14.80 | 20.875 |
| A1831 | 0.075 | 18,466 | 1,785 | 520 | 313 | 1.76 | 14.82 | 20.125 |
| A2034 | 0.113 | 37,944 | 915 | 410 | 287 | 1.78 | 14.85 | 20.625 |
| A7 | 0.103 | 13,463 | 992 | 436 | 281 | 1.83 | 14.89 | 20.875 |
| A2255 | 0.080 | 11,944 | 2,057 | 1,099 | 618 | 1.90 | 14.93 | 20.625 |
| A2029 | 0.079 | 34,829 | 2,235 | 1,377 | 538 | 1.90 | 14.93 | 20.625 |
| A2065 | 0.073 | 25,159 | 3,109 | 1,099 | 609 | 2.03 | 15.01 | 21.125 |

(M200 오름차순. 각 행 클릭 → 그 은하단의 R–v diagram / completeness map 이미지 모달, 나중 단계)

**Key results (Park+26) — 카드 4개**
1. *Cluster vs. field SMF*: 모양은 10.5 < log M* < 11.4에서 field와 같지만 진폭 ~2배. log M* > 11.4에서 BCG 포함 massive galaxy excess.
2. *Quiescent vs. star-forming*: quiescent SMF는 log M* ≈ 10.5에서 피크가 있는 곡선형, star-forming은 저질량으로 단조 증가. 중심부로 갈수록 quiescent 피크가 저질량 쪽으로 이동 → 코어에서 저질량 은하 quenching.
3. *Radial dependence*: quiescent fraction이 저질량·중심부로 갈수록 증가 (3 radial bins).
4. *vs. IllustrisTNG-300*: 10.5–11.4 잘 맞음. 9.0 < log M* < 10.5에서 관측이 ~2배 더 많음; log M* > 11.4에서는 시뮬 BCG가 더 무거움 (BCG/ICL 분리 이슈).

**Figure candidates** (`reference/2026_Park_SMF-nine-clusters/src/images/`, 본인 논문이라 재사용 OK; PDF → PNG/SVG 변환 필요)
- Figure1 — omnibus M200 vs N_spec에 MACH 박스 → **MACH 섹션 히어로 그래픽**
- Figure2/3 — completeness curve / 2D map
- Figure4 — R–v diagram 9개 (갤러리)
- Figure10/11 — MACH SMF (보정 전/후)
- Figure15 — field vs cluster SMF
- Figure16/17 — quiescent/SF radial SMF, f_quiescent
- 마지막 그림 — vs TNG300

**MACH 관련 선행 논문 (링크)**
- Sohn+2017, 2019 — A2029 pilot (~1,200 members)
- Sohn+2020 (omnibus §2.2.2)에서 MACH를 "seven clusters, >2500 spectra each"로 소개 → 최종 9개로 확장됨 (사이트에 그 변천 한 줄 언급 가능)

---

### 2.4 Data

**Data access — 메인 버튼**
- `Download HeCS-omnibus / MACH data` → `http://147.46.135.40:3000/sharing/va94quU2B`
  - 참고: HTTP(비 HTTPS)라 GitHub Pages(HTTPS)에서 링크 클릭은 되지만 브라우저가 "안전하지 않음" 경고를 띄울 수 있음. iframe 임베드는 mixed-content로 차단되므로 **링크만**.
  - 접근 조건(공개/비번/기간)은 사용자가 정해서 페이지에 한 줄 명시 필요.

**What you get** — 폴더 구성 미정. v1에서는 큰 버튼 하나 + 한 줄 설명("Cluster catalog, BCG catalog, member galaxies, and MACH spectroscopic products. Contents will be documented here as the release is finalized.")만 두고, 파일 목록은 나중에 채움.

**External archives**
- VizieR `J/ApJ/891/129` — HeCS-omnibus catalog (Sohn+2020)
- Harvard Dataverse doi:10.7910/DVN/UR9XE5 — BCG identification figures (Sohn 2020)
- MMT archive (OIRSA) — raw Hectospec spectra
- VizieR `J/ApJ/862/172`, `J/ApJ/819/63`, `J/ApJ/767/15`, `J/AJ/132/1275` — HeCS-red / SZ / HeCS / CIRS

**Citation box**
> If you use HeCS-omnibus data, please cite Sohn et al. (2020, ApJ 891, 129). For MACH, please cite Park et al. (2026, ApJ 1001, 185). (BibTeX 복사 버튼 → `reference/hecs-omnibus.bib`에서 가져옴)

**Cosmology note**: H0 = 70, Ωm = 0.3, ΩΛ = 0.7.

---

### 2.5 Publications

**Core (the survey papers)**
1. Rines & Diaferio 2006, AJ 132, 1275 — CIRS
2. Rines, Geller, Diaferio, Kurtz 2013, ApJ 767, 15 — HeCS
3. Rines, Geller, Diaferio, Hwang 2016, ApJ 819, 63 — HeCS-SZ
4. Rines, Geller, Diaferio, Hwang, Sohn 2018, ApJ 862, 172 — HeCS-red
5. **Sohn, Geller, Diaferio, Rines 2020, ApJ 891, 129 — HeCS-omnibus**
6. **Park, Sohn, Geller, Rines, Diaferio 2026, ApJ 1001, 185 — MACH SMF**

**Science with HeCS-omnibus / HeCS**
- Sohn+2020b, ApJ 902, 17 — VDF of quiescent galaxies in nine lensing clusters (omnibus empirical distributions 사용)
- Pizzardo+2021, A&A 646, A105 — Mass accretion rates of 129 CIRS+HeCS clusters (MAR ↑ with mass & z, ΛCDM 일치)
- Logan+2022, A&A 665, A124 — Chandra vs caustic masses, 44 clusters; M_X/M_C = 1.12 (+0.11/−0.10) → hydrostatic bias < 20% (3σ)
- (ADS citations 검색 결과에서 추가 가능: Sohn+2021 HectoMAP BCGs, Sohn+2022 TNG BCGs, Pizzardo+2023 TNG caustic, Kang+2025 Coma, Kim+2026 A85 WL 등 — 필요하면 "Papers using HeCS-omnibus" 자동 리스트로)

각 항목: 제목 / 저자 / 저널 / **ADS** · **arXiv** · **DOI** 링크 3개.

---

### 2.6 Team (사용자 확인 필요)
- 논문 저자 기준 후보: Jubee Sohn, Margaret J. Geller, Antonaldo Diaferio, Kenneth J. Rines, Ho Seong Hwang, Jong-In Park, Michael J. Kurtz, Daniel Fabricant
- 소속·역할·사진·링크는 사용자가 결정. 임시로 "Contact: (이메일)"만 두는 것도 가능.
- Acknowledgements: MMT Observatory, SDSS, NRF Korea (RS-2023-00210597, RS-2023-00301976), CfA Fellowship, INFN InDark.

---

## 3. 참고 사이트 분석 (2026-09 조사)

| 사이트 | 구조 | 눈여겨볼 점 | 우리에 적용 |
|---|---|---|---|
| **GOGREEN** (gogreensurvey.ca) | WordPress. Home / Science / Public / Astronomers(Survey Details: Cluster Targets, Design, Spectroscopy, Imaging, Status · Data Releases DR1/DR2) / Publications / Team / Internal | 홈 첫 줄이 **날짜 + 뉴스 한 줄** ("April 30, 2025: DR2 now public"). 홈 본문이 그림 4장+캡션으로 서베이를 설명 (2D 스펙트럼 스택, 색 이미지에 멤버 동그라미). **Cluster Targets** 페이지 = 표 하나 (이름/RA/Dec/z). **DR2 페이지** = Description → Errata → Data Access → Citations → Cluster Sample → 디렉터리별 파일 설명. Team = 이름/역할/소속 표 + 사진 49장. 헤딩에 Lora(세리프), 네이비 #114878 | 홈 상단 날짜-뉴스 한 줄, 은하단 표 페이지, Data 페이지 순서(설명→접근→인용), Team 표 형식 |
| **SAMI** (sami-survey.org) | Home / Team / Joining / Papers / Public Data(DR별) | 홈에 **관측 밤 타임랩스 영상** → 사람·망원경 냄새. Data 섹션이 릴리즈별 한 줄(이름·날짜·은하 수·인용) | 히어로에 MMT/Hectospec 관측 사진 또는 영상. Data 릴리즈 한 줄 요약 형식 |
| **COSMOS** | 대상별 nav: For the Public / For Astronomers / For Reviewers | 청중별 분리. 홈에 Spotlight 4개 | 우리는 규모가 작으니 미적용, 다만 "For astronomers" 톤의 Data 섹션 |
| **KiDS** | 홈 = 뉴스 피드, Data access = DR1–DR5 페이지 + Science data products | 릴리즈 히스토리가 곧 홈 | 홈 하단 "News / Changelog" 작게 |
| **CLASH** (STScI) | 단일 페이지, **은하단 표가 페이지 중심** (이름·z·이미지·카탈로그·렌즈모델 링크 열) + Latest Updates + footnotes | 표 한 장이 데이터 릴리즈 전체 | MACH 9개 표를 이 형식으로(행마다 R–v / completeness / catalog 링크) |
| **LoCuSS** | Home / Science / Observations / People / For Scientists / Publications | 홈이 **같은 은하단의 다파장 이미지 4장 세로 스택**으로 시작 — 한 은하단으로 서베이를 설명 | A2029 하나로 SDSS 이미지 + R–v + SMF 3연작 히어로 가능 |
| **ZFOURGE** | Home / Survey / Science / Team / Publications / Data / Contact | 흰 배경, 그림 6장 갤러리, 정적 HTML | nav 구성이 우리와 거의 같음 → 기본 골격으로 채택 |
| **HSC-SSP** | Survey / Science / Instrument / Pipeline / Publications / Data Release | Data Release가 nav에서 독립 + 큰 CTA 버튼 | Data 버튼을 nav 오른쪽 끝에 강조색으로 |
| **DESI docs** | MkDocs 좌측 사이드바, 릴리즈별 페이지, "Data License and Acknowledgments" 별도 | 인용/라이선스 섹션 명시 | Data 섹션에 Citation 박스 필수 |
| **Frontier Fields** | 블로그형. 팀원 소개를 개별 포스트로 | 사람 중심 서사 | Team을 표가 아니라 짧은 소개+사진 카드로 |

**공통 패턴**: (1) 홈은 서베이 한 문단 + 대표 그림 + 최신 뉴스 한 줄, (2) 은하단 목록은 반드시 표, (3) Data 페이지는 설명→접근→인용 순, (4) 흰 배경·산세리프·장식 최소. 다수가 WordPress/구식 HTML이라 조금만 다듬어도 돋보임.

## 4. 디자인 방향 (수정: 따뜻하고 사람 냄새, Apple 기본 느낌)

- **배경**: 다크 네이비 폐기. 따뜻한 오프화이트(#faf8f5 계열) 바탕, 본문 진회색(#1d1d1f). 다크 배경은 히어로/푸터 한두 군데만, 그것도 검정에 가까운 웜 그레이(#1c1b19)에 흰 글씨 정도.
- **액센트 1색**: 테라코타/앰버 계열(예: #c2552f 또는 #b8862b) 하나만. 링크·버튼·MACH 강조에만 사용. 그라디언트·네온·글로우 금지.
- **타이포**: 헤딩 세리프(Source Serif 4 / Newsreader / Lora — GOGREEN도 Lora), 본문 시스템 산세리프(-apple-system, Inter). 헤딩을 세리프로 두면 "논문·사람" 느낌이 나고 AI 템플릿 느낌이 빠짐. 숫자·표는 tabular-nums.
- **레이아웃**: 최대 폭 ~1040px, 넉넉한 여백, 한 열 흐름. 카드 남발 금지 — 카드는 MACH Key results 4개, Two-track 2개만. 나머지는 문단+표+그림.
- **이미지 (사람 냄새의 핵심)**:
  - 히어로: MMT 돔/Hectospec 파이버 포지셔너 실사(SAO/MMTO 크레딧 확인) 또는 관측 밤 사진. 없으면 A2029 SDSS 컬러 이미지.
  - 각 섹션에 논문 그림 1장씩 캡션과 함께 — GOGREEN 홈 방식. 그림은 흰 배경 PNG로 재출력.
  - Team: 얼굴 사진 + 두 줄 소개 (표보다 카드). 현재 Team 명단 미정 → Contact만 우선.
- **모션**: 없음. hover 시 링크 밑줄 정도.
- **아이콘**: 없음 (아이콘 그리드가 가장 AI스러움).
- **푸터**: 기관 로고(SNU, CfA/SAO, MMTO, SDSS) 회색 처리로 한 줄 + 인용 안내 + last updated.
- nav: `HeCS-omnibus` 워드마크 왼쪽, 오른쪽에 Survey · MACH · Data · Publications · Team, 맨 끝 **Data** 버튼만 액센트색.

## 5. 구현 단계

1. **v1 (단일 페이지)**: Home + Survey 타임라인 + MACH 섹션(표 + 텍스트) + Data 링크 + Publications. 그림 없이 텍스트/표만 → push.
2. **v2**: Park+26 Fig. 1, SMF 그림 PNG 변환해서 MACH 섹션에 삽입. Sohn+20 BCG 요약 그림 1장.
3. **v3**: 은하단별 페이지/모달 (R–v diagram, completeness map, 멤버 수) — MACH 9개 우선, 이후 omnibus 227개는 Dataverse 그림 링크.
4. Team/Contact 채우기, 공유 폴더 내용에 맞춰 Data 섹션 파일 목록 확정.

---

## 6. 사용자 확인 필요 항목

- [x] Data: 공유 링크를 버튼으로만. 파일 구성은 미정 → 나중에 채움
- [x] HeCS-omnibus가 메인, MACH는 서브 브랜드. Publications에 관련 논문 전부
- [x] 논문 그림 재사용 OK
- [x] 디자인: 다크 네이비 X → 따뜻한 오프화이트 + 세리프 헤딩, Apple 기본 느낌, 사람 냄새
- [ ] Team 섹션 명단 (미정 → v1은 Contact만)
- [ ] 히어로용 MMT/Hectospec 사진 있는지 (직접 찍은 관측 사진이 있으면 최고)
- [ ] 홈 상단 뉴스 한 줄에 넣을 첫 소식 (예: "2026-04: Park et al. 2026 published in ApJ")
