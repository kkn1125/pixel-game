# 이것저것 UI 리소스

사용자가 제공한 PNG를 `client/scripts/prepare-ui-assets.ps1`로 웹용 패킹했다. 입력 원본은 `client/art-source/1.0/ui/entry/`에 보존하며 도구의 기본 입력 경로다. 입력 원본은 수정하지 않는다. `main-example.png`는 배치 참고 이미지이며 런타임에 사용하지 않는다.

| 게임용 파일 | 제공 원본 | 처리 |
| --- | --- | --- |
| `main-background.png` | `main-background.png` | 1672×941 유지, JPEG 품질 92 |
| `panel-frame.png` | `modal-outline.png` | 투명 여백 정리, 알파 보존 |
| `button-frame.png` | `button-outline.png` | 상하의 큰 투명 여백 정리, 알파 보존 |
| `panel-mask.png`, `button-mask.png` | 패킹된 두 프레임 | 닫힌 테두리의 내부만 흰색 알파로 채운 배경용 마스크 |
| `emblem.png` | `emblem.png` | 투명 여백 정리, 폭 480px |
| `parchment.jpg` | `paper-background.png` | 폭 640px, JPEG 품질 92 |

CSS의 `border-image`가 각 프레임을 3×3의 아홉 구역으로 분할한다. 모서리는 고정 크기로, 상하좌우의 직선 부분만 늘린다. 중심은 투명하게 두고 양피지 또는 버튼 색상을 별도 레이어로 채운다.

배경 레이어는 원본 프레임 안쪽에서 생성한 알파 마스크를 같은 9분할 값으로 적용한다. 임의의 둥근 사각형이나 육각형으로 대체하지 않는다. 금색 프레임과 문장·글자는 마스크 밖의 별도 레이어에 두므로 장식은 잘리지 않는다. 마우스를 올리거나 버튼을 비활성화해도 요소 자체의 배경은 투명하게 유지한다. 마스크는 Chromium/WebKit의 `-webkit-mask-box-image`와 표준 `mask-border`를 함께 선언한다. [CSS Masking 사양](https://www.w3.org/TR/css-masking-1/#mask-borders)을 따른다.

- 패널: `border-image-slice: 180`, 기본 표시 폭 `42px`, 모바일 모달 `33px`.
- 버튼: `border-image-slice: 36 240` (상하 36px, 좌우 240px), 기본 표시 폭 `6px 38px`, 큰 로그인 버튼 `7px 47px`. 파란 보석 전체를 좌우 중앙 구역에 두어 세로로 늘어지지 않게 한다.
- 작은 능력치 버튼은 패널 프레임을 표시 폭 `13px`로 사용한다. 정사각형 버튼에 가로형 버튼의 끝 장식을 억지로 축소하지 않는다.
- 실제 스타일은 `src/assets/fantasy-ui.css`에 모으고 배포 경로는 Vite가 보정한다.

재패킹: PowerShell에서 `./client/scripts/prepare-ui-assets.ps1 -SourceDirectory <원본 폴더>` 실행. 폴더에는 위 다섯 제공 원본이 있어야 한다. 프레임 가운데의 투명 여부, 윤곽의 닫힘, 마스크의 내부 불투명·외부 투명을 자체 검사한다.
