# Korean term base

The terms `ko.yaml` (Korean) is translated with. Every value in `ko.yaml` follows this table: a thing is named the
same way on every screen, in every hint, in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its Korean value must contain the `ko` term.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `ko` for a different concept.
- A row whose `ko` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.
- Loanwords follow the Korean Unity editor: Hangul transliteration (`레이어`, `인스펙터`, `키프레임`).

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `ko.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for Korean: `Assets/Addressables/TEXT-STYLE.md`, section 10, in
the game's repository.

| en | ko | kind | note |
|---|---|---|---|
| Level | 레벨 | strict | 한 번의 플레이를 이루는 모든 것: 오브젝트, 오디오, 이벤트, 자체 리소스. 소리 크기의 "level"은 다른 뜻이며 "음량" 또는 "신호 레벨"로 옮긴다 |
| Object | 오브젝트 | strict | 타임라인 위에서 제작자가 만드는 것. 구간, 트랜스폼, 부모를 가진다. Unity 한국어판 용어 |
| Rect | 빈 오브젝트 | loose | 아무것도 그리지 않는 오브젝트: 트랜스폼, 구간, 자식만 가진다. ru처럼 두 단어로 나눈다: 타입으로는 "빈 오브젝트", 도형(사각형)으로는 "직사각형" |
| Shape | 도형 | loose | 오브젝트가 그리는 실제 지오메트리. 이미지가 아니다. 게임이 약 500종을 직접 생성한다 |
| Collider | 콜라이더 | strict | 오브젝트가 충돌하는 범위. 그려지는 모양과 달라도 된다. Unity 한국어판 용어 |
| Prefab | 프리팹 | strict | 레벨에 몇 번이든 배치할 수 있는 재사용 가능한 오브젝트 템플릿. Unity 한국어판 용어 |
| Prefab Mode | 프리팹 모드 | strict | 주변 레벨이 아니라 템플릿 자체의 내용을 편집하는 모드. Unity 한국어판 용어 |
| Effect | 이펙트 | loose | 생성기 같은 오브젝트: 몇 가지 파라미터로 매 프레임 자기 오브젝트를 만든다. Bloom, Vignette 등은 "포스트 프로세싱 효과"이지 "이펙트"가 아니다 |
| Inframe Object | 프레임 내 오브젝트 | loose | 이펙트가 만든 오브젝트. 엔진이 관리하며 선택도 편집도 할 수 없다 |
| Theme | 테마 | strict | 레벨이 인덱스로 참조하는 팔레트. 색 변경은 한 곳만 고치면 된다 |
| Frame | 프레임 | strict | 레벨 시간의 단위. 프레임은 칸이고, 시간은 칸과 칸 사이의 경계 |
| Keyframe | 키프레임 | strict | 어떤 프레임에서 제작자가 정한 값. 두 키프레임 사이는 보간된다. Unity 한국어판 용어 |
| Key | 키프레임 | loose | "키프레임"의 줄임말이면 "키프레임", 키보드 키는 "키", 현지화 키도 "키" |
| Track | 트랙 | strict | 애니메이션 가능한 속성 하나의 키프레임 행: 위치, 회전, 음량. Audio Track은 "오디오 트랙" |
| Timeline | 타임라인 | strict | 레벨을 편집하는 프레임 축. 내용 종류마다 탭이 하나씩 있다 |
| Span | 구간 | loose | 오브젝트가 존재하는 기간: 끝 프레임이 아니라 시작 프레임과 길이. 동사 span("걸치다")은 "구간"으로 옮기지 않는다 |
| Playhead | 재생 헤드 | strict | 지금 표시하고 있는 프레임. 띄어 쓴다 |
| Ease | 이징 | strict | 이전 키프레임에서 이 키프레임까지 값이 움직이는 방식 |
| Marker | 마커 | strict | 레벨 눈금자 위의 이름 붙은 지점. 위치를 다시 찾기 위한 것 |
| Checkpoint | 체크포인트 | strict | 죽은 플레이어가 돌아가는 위치 |
| Anchor | 앵커 | strict | 부모의 가장자리를 따라가는 가장자리. 부모가 줄어들면 자식도 함께 움직인다. Unity 한국어판 용어 |
| Layer | 레이어 | strict | 그리기 순서. 부모 기준의 상대값: 자식의 레이어에 부모의 레이어가 더해진다. Unity 한국어판 용어 |
| Pivot | 피벗 | loose |  |
| Gizmo | 기즈모 | strict | 뷰포트에서 선택한 오브젝트 위에 그려지는 드래그 핸들. Unity 한국어판 용어 |
| Snapping | 스냅 | strict | 드래그를 무언가에 달라붙게 하는 기능: 자석이면 다른 내용, 비트 토글이면 음악 |
| Snap | 스냅 | strict | Snapping과 같음 |
| Beat | 비트 | strict | 음악 자체의 그리드. 레벨이 설정하며 플레이 중에는 읽지 않는다 |
| Beat Segment | 비트 세그먼트 | strict | 템포가 일정한 한 구간. 자체 템포, 위상, 마디 길이를 가진다. "구간"은 Span이므로 쓰지 않는다 |
| BPM | BPM | strict | 분당 비트 수. 라틴 문자 그대로, 한국 리듬 게임 커뮤니티에서도 공통 |
| Tap | 탭 | loose |  |
| Generator | 생성기 | strict | 제작 자동화: 몇 가지 파라미터로 레벨 내용을 만든다 |
| Modifier | 모디파이어 | strict | 추가하지 않고 기존 내용을 편집하거나 제거하는 생성기. Blender 한국어판 용어 |
| Seed | 시드 | strict | 레벨의 모든 무작위 값이 나오는 수. 같은 시드면 같은 결과가 재현된다 |
| Raw Data | 원시 데이터 | strict | 저장 모델 전체를 편집 가능한 트리로 보여 준 것. 일부러 검증하지 않는다 |
| Recommendation | 권장 | strict | 다섯 라벨 중 하나. `<b>권장:</b>`으로 쓴다 |
| Tip | 팁 | strict | 다섯 라벨 중 하나. `<b>팁:</b>`으로 쓴다 |
| Worth knowing | 참고 | strict | 다섯 라벨 중 하나. `<b>참고:</b>`로 쓴다 |
| Warning | 경고 | strict | 다섯 라벨 중 하나. `<b>경고:</b>`로 쓴다 |
| Caution | 주의 | strict | 다섯 라벨 중 하나. `<b>주의:</b>`로 쓴다 |
| More | 자세히 | loose | 힌트 마지막 링크 줄 `More:`는 `자세히:` |
| Bullet Hero | Bullet Hero | strict | 제품명. 번역하지 않는다 |
| Steam | Steam | loose |  |
| JSON | JSON | strict | 형식 이름. 번역하지 않는다 |
| MSAA | MSAA | strict | 기술 약어. 번역하지 않는다 |
| FXAA | FXAA | strict | 기술 약어. 번역하지 않는다 |
| HDR | HDR | loose |  |
| VFX | VFX | loose |  |
| URL | URL | loose |  |
| Ctrl | Ctrl | loose |  |
| Shift | Shift | loose |  |
| Enter | Enter | loose |  |
| Hierarchy | 계층 구조 | strict | 부모 자식 관계로 오브젝트를 나열하는 에디터 패널. Unity 한국어판의 "계층 구조" 창 |
| Inspector | 인스펙터 | strict | 선택한 내용의 속성을 보여 주는 에디터 패널. Unity 한국어판 용어 |
| Viewport | 뷰포트 | strict | 에디터 안에서 레벨 화면을 보여 주는 영역 |
| Command Palette | 명령 팔레트 | strict | 이름으로 명령을 찾아 실행하는 창. VS Code 한국어판 용어 |
| Command | 명령 | loose |  |
| Selection | 선택 | loose | 선택된 항목의 모음은 "선택 항목"으로도 쓸 수 있다 |
| Select | 선택 | loose |  |
| Marquee | 사각형 선택 | strict | 사각형을 드래그해서 선택하는 것 |
| Apply | 적용 | loose |  |
| Reset | 초기화 | loose |  |
| Cancel | 취소 | loose |  |
| Confirm | 확인 | loose |  |
| OK | 확인 | loose | 한국어 UI의 OK 버튼은 "확인" |
| Save | 저장 | loose |  |
| Load | 불러오기 | loose |  |
| Open | 열기 | loose |  |
| Close | 닫기 | loose |  |
| Exit | 종료 | loose |  |
| Create | 생성 | loose |  |
| Add | 추가 | loose |  |
| Remove | 제거 | loose | Delete(삭제)와 구별한다: Remove는 목록에서 빼는 것, Delete는 지우는 것 |
| Delete | 삭제 | loose |  |
| Duplicate | 복제 | loose |  |
| Copy | 복사 | loose |  |
| Paste | 붙여넣기 | loose |  |
| Cut | 잘라내기 | loose |  |
| Undo | 실행 취소 | loose |  |
| Redo | 다시 실행 | loose |  |
| History | 기록 | loose |  |
| Edit | 편집 | loose |  |
| Rename | 이름 바꾸기 | loose |  |
| Move | 이동 | loose |  |
| Import | 가져오기 | loose |  |
| Export | 내보내기 | loose |  |
| Archive | 아카이브 | loose |  |
| Folder | 폴더 | loose |  |
| File | 파일 | loose |  |
| Search | 검색 | loose |  |
| Filter | 필터 | loose |  |
| Refresh | 새로 고침 | loose |  |
| Toggle | 전환 | loose |  |
| Show | 표시 | loose |  |
| Hide | 숨기기 | loose |  |
| Hidden | 숨김 | loose |  |
| Visible | 표시됨 | loose |  |
| Enabled | 활성화됨 | loose |  |
| Disabled | 비활성화됨 | loose |  |
| On | 켜짐 | loose |  |
| Off | 꺼짐 | loose |  |
| None | 없음 | loose |  |
| Auto | 자동 | loose |  |
| Custom | 사용자 지정 | loose |  |
| Default | 기본값 | loose |  |
| All | 모두 | loose |  |
| Nothing | 없음 | loose |  |
| Current | 현재 | loose |  |
| Active | 활성 | loose |  |
| Global | 글로벌 | loose |  |
| Local | 로컬 | loose |  |
| Parent | 부모 | loose |  |
| Child | 자식 | loose |  |
| Root | 루트 | loose |  |
| Fold | 접기 | loose |  |
| Unfold | 펼치기 | loose |  |
| Flatten | 평탄화 | loose |  |
| Transform | 트랜스폼 | loose |  |
| Position | 위치 | loose |  |
| Rotation | 회전 | loose |  |
| Scale | 스케일 | loose |  |
| Size | 크기 | loose |  |
| Offset | 오프셋 | loose |  |
| Angle | 각도 | loose |  |
| Radius | 반지름 | loose |  |
| Width | 너비 | loose |  |
| Height | 높이 | loose |  |
| Min | 최소 | loose |  |
| Max | 최대 | loose |  |
| Step | 단계 | loose |  |
| Random | 무작위 | loose |  |
| Rnd | 무작위 | loose |  |
| From | 시작값 | loose |  |
| To | 끝값 | loose |  |
| Value | 값 | loose |  |
| Type | 타입 | loose |  |
| Name | 이름 | loose |  |
| Mode | 모드 | loose |  |
| Count | 개수 | loose |  |
| Speed | 속도 | loose |  |
| Velocity | 속도 | loose |  |
| Gravity | 중력 | loose |  |
| Particle | 파티클 | loose |  |
| Orbital | 궤도 | loose |  |
| Lifetime | 수명 | loose |  |
| Color | 색상 | loose |  |
| Alpha | 알파 | loose |  |
| Opacity | 불투명도 | loose |  |
| Opaque | 불투명 | loose |  |
| Transparent | 투명 | loose |  |
| Gradient | 그레이디언트 | loose |  |
| Texture | 텍스처 | loose |  |
| Font | 폰트 | loose |  |
| Text | 텍스트 | loose |  |
| Localized Text | 현지화 텍스트 | loose |  |
| Language | 언어 | loose |  |
| Audio | 오디오 | loose |  |
| Audio Track | 오디오 트랙 | loose |  |
| Volume | 음량 | loose |  |
| Music | 음악 | loose |  |
| Sound | 사운드 | loose |  |
| Resource | 리소스 | loose |  |
| Resources | 리소스 | loose |  |
| Metadata | 메타데이터 | loose |  |
| Meta | 메타 | loose |  |
| License | 라이선스 | loose |  |
| Author | 제작자 | loose |  |
| Artist | 아티스트 | loose |  |
| Settings | 설정 | loose |  |
| Editor | 에디터 | loose |  |
| Game | 게임 | loose |  |
| Player | 플레이어 | loose |  |
| Avatar | 아바타 | loose |  |
| Dash | 대시 | loose |  |
| Hitbox | 히트박스 | loose |  |
| Damage | 대미지 | loose |  |
| Health | 체력 | loose |  |
| Death | 사망 | loose |  |
| Camera | 카메라 | loose |  |
| Zoom | 줌 | loose |  |
| Pan | 팬 | loose |  |
| Shake | 흔들림 | loose |  |
| Grid | 그리드 | loose |  |
| Ruler | 눈금자 | loose |  |
| Loop | 반복 | loose |  |
| Play | 재생 | loose | 에디터에서의 재생은 "재생", 레벨을 하는 것은 "플레이" |
| Pause | 일시 정지 | loose |  |
| Stop | 정지 | loose |  |
| Preview | 미리 보기 | loose |  |
| Render | 렌더링 | loose |  |
| Post-processing | 포스트 프로세싱 | loose |  |
| Post | 포스트 | loose |  |
| Bloom | 블룸 | loose |  |
| Vignette | 비네트 | loose |  |
| Chromatic Aberration | 색수차 | loose |  |
| Lens Distortion | 렌즈 왜곡 | loose |  |
| Film Grain | 필름 그레인 | loose |  |
| Grain | 그레인 | loose |  |
| Motion Blur | 모션 블러 | loose |  |
| Blur | 블러 | loose |  |
| Color Curves | 컬러 커브 | loose |  |
| Curve | 커브 | loose |  |
| Lift Gamma Gain | 리프트/감마/게인 | loose |  |
| Shadows Midtones Highlights | 섀도/미드톤/하이라이트 | loose |  |
| White Balance | 화이트 밸런스 | loose |  |
| Analog Glitch | 아날로그 글리치 | loose |  |
| Digital Glitch | 디지털 글리치 | loose |  |
| Glitch | 글리치 | loose |  |
| Gamma | 감마 | loose |  |
| Background | 배경 | loose |  |
| Framerate | 프레임 레이트 | loose |  |
| Fixed Framerate | 시뮬레이션 업데이트 빈도 | loose |  |
| Collision | 충돌 | loose |  |
| Screen Limit | 화면 제한 | loose |  |
| Cursor | 커서 | loose |  |
| Control | 조작 | loose |  |
| Controls | 조작 | loose |  |
| Keybinding | 키 할당 | loose |  |
| Shortcut | 단축키 | loose |  |
| Button | 버튼 | loose |  |
| Interface | 인터페이스 | loose |  |
| Screen | 화면 | loose |  |
| Window | 창 | loose |  |
| Panel | 패널 | loose |  |
| Tab | 탭 | loose | Tap도 한국어로는 "탭"이다. 둘은 문맥으로 구별한다 |
| Menu | 메뉴 | loose |  |
| Tool | 도구 | loose |  |
| Library | 라이브러리 | loose |  |
| Bot | 봇 | loose |  |
| Tutorial | 튜토리얼 | loose |  |
| Sandbox | 샌드박스 | loose |  |
| Hint | 힌트 | loose |  |
| Glossary | 용어집 | loose |  |
| Validation | 검증 | loose |  |
| Rules | 규칙 | loose |  |
| Format | 형식 | loose |  |
| Version | 버전 | loose |  |
| Desktop | 데스크톱 | loose |  |
| Mobile | 모바일 | loose |  |
| Alignment | 정렬 | loose | Placement(배치)와 구별한다 |
| Align | 정렬 | loose |  |
| Center | 가운데 | loose |  |
| Left | 왼쪽 | loose |  |
| Right | 오른쪽 | loose |  |
| Top | 위쪽 | loose |  |
| Bottom | 아래쪽 | loose |  |
| Horizontal | 가로 | loose |  |
| Vertical | 세로 | loose |  |
| Linear | 선형 | loose |  |
| Appearing | 등장 | loose |  |
| Scissors | 가위 | loose |  |
| Edges | 가장자리 | loose |  |
| Point | 점 | loose |  |
| Continue | 계속 | loose |  |
| Next | 다음 | loose |  |
| Back | 뒤로 | loose |  |
| Loading | 불러오는 중 | loose |  |
| Progress | 진행 상황 | loose |  |
| Statistics | 통계 | loose |  |
| Preset | 프리셋 | loose |  |
| Clipboard | 클립보드 | loose |  |
| Console | 콘솔 | loose |  |
| Ping | 위치 표시 | loose |  |
| Override | 오버라이드 | loose |  |
| Placement | 배치 | loose |  |
| Template | 템플릿 | loose |  |
| Clip | 클립 | loose |  |
| Slip | 슬립 | loose |  |
| Slot | 슬롯 | loose |  |
| Beat Grid | 비트 그리드 | loose |  |
| Bar | 마디 | loose |  |
| Tempo | 템포 | loose |  |
| Tap Tempo | 탭 템포 | loose |  |
| Stereo Pan | 스테레오 팬 | loose |  |
| Font Size | 폰트 크기 | loose |  |
| Word Wrap | 자동 줄 바꿈 | loose |  |
| Backup | 백업 | loose |  |
| Branch | 브랜치 | loose |  |
| Fit | 맞춤 | loose |  |
| Finding | 문제 | loose |  |
| Fix | 수정 | loose |  |
| Group | 그룹 | loose |  |
| Id | ID | loose |  |
| Mipmap | 밉맵 | loose |  |
| Sampling | 샘플링 | loose |  |
| Tiling | 타일링 | loose |  |
| Wrapping | 래핑 | loose |  |
| Pixel art | 픽셀 아트 | loose |  |
| Drawing | 그림 | loose |  |
| Emission Shape | 방출 형태 | loose |  |
| Over Lifetime | 수명에 따른 변화 | loose |  |
| Forces | 힘 | loose |  |
| Scatter | 흩뿌리기 | loose |  |
| Spread | 확산 | loose |  |
| Tangent | 탄젠트 | loose |  |
| Clamp | 클램프 | loose |  |
| Ping Pong | 핑퐁 | loose |  |
| Temperature | 색온도 | loose |  |
| Tint | 색조 | loose |  |
| Modifier Key | 보조 키 | loose |  |
| Dead Zone | 데드존 | loose |  |
| Sensitivity | 감도 | loose |  |
| Stick | 스틱 | loose |  |
| Shoulder | 숄더 버튼 | loose |  |
| Gamepad | 게임패드 | loose |  |
| Touchscreen | 터치스크린 | loose |  |
| Motion Sensor | 모션 센서 | loose |  |
| Handedness | 주로 쓰는 손 | loose |  |
| Double Tap | 더블 탭 | loose |  |
| Workshop | 창작마당 | loose | Steam 한국어판 용어 |
| Story | 스토리 | loose |  |
| Wave | 웨이브 | loose |  |
| Immortal | 무적 | loose |  |
| Dodge | 회피 | loose |  |
| Zen | 젠 | loose |  |
| Clears | 클리어 횟수 | loose |  |
| Hits | 피격 횟수 | loose |  |
| Profile | 프로필 | loose |  |
| Frame Hierarchy | 프레임 계층 구조 | loose | strict의 Hierarchy(계층 구조)에 맞춘다 |
| Stop Frame | 정지 프레임 | loose |  |
| Runtime Seed | 런타임 시드 | loose |  |
| Level Logo | 레벨 커버 | loose | 레벨 목록에 표시되는 이미지 |
| Post-processing effect | 포스트 프로세싱 효과 | loose |  |
| Audio effect | 오디오 효과 | loose | "이펙트"는 Effect 오브젝트에만 쓴다 |
| Chorus | 코러스 | loose |  |
| Compressor | 컴프레서 | loose |  |
| Distortion | 디스토션 | loose |  |
| Echo | 에코 | loose |  |
| Flange | 플랜저 | loose |  |
| Highpass | 하이패스 | loose |  |
| Lowpass | 로우패스 | loose |  |
| Normalize | 노멀라이즈 | loose |  |
| Param EQ | 파라메트릭 EQ | loose |  |
| Pitch Shifter | 피치 시프터 | loose |  |
| Reverb | 리버브 | loose |  |
| Emitter | 이미터 | loose |  |
| Variant | 베리언트 | loose |  |
| Fader | 페이더 | loose |  |
| Signal level | 신호 레벨 | loose | 오디오 효과 힌트에서의 "level". LocalizationGlossaryTests에서 제외되어 있다 |
| Swatch | 스와치 | loose |  |
| Device library | 이 기기의 공유 라이브러리 | loose |  |
| Collection | 컬렉션 | strict | 재사용할 수 있는 리소스의 폴더: 프리팹, 테마, 도형, 이펙트, 텍스처, 폰트, 오디오. Steam의 Collections(창작마당 아이템 모음)와는 무관하다. 데이터 구조의 collection(검증 규칙 이름)은 "컬렉션"으로 옮기지 않아도 되며, 그 키들은 LocalizationGlossaryTests에서 제외되어 있다 |
| Anti-aliasing | 안티앨리어싱 | loose |  |
| Overlay | 오버레이 | loose |  |
| Scrub | 스크럽 | loose |  |
| Gradient stop | 색상 정지점 | loose |  |
| Link to a docs page | 페이지 제목 | loose | 문서 링크는 링크 대상 페이지의 한국어 제목으로 쓴다 |
