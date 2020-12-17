## Electron-builder의 속성

### build

```
asar	- asar 패키지 사용할 지 여부
			- asar는 어플리케이션(app) 파일들을 묶어준다.
      - 디폴트는 true
appId - 어플리케이션의 고유 id
productionName	- 어플리케이션 이름
win	- 윈도우 installer(builder) 설정
		- target: 윈도우 인스톨러 타겟 포멧 설정
		- icon: 윈도우 어플리케이션 파일 아이콘 설정
nsis	- windows의 nsis 타겟 빌드 방법 설정
			- oneClick: 인스톨러 파일 한 번 클릭 시 인스톨 되도록 설정. true가 디폴트
			- perMachine: 설치가 항상 모든 사용자인지 여부. false가 디폴트
			- installerIcon: 인스톨러 파일 아이콘 설정
			- createDesktopShortcut: 인스톨러 설치 시 바탕화면에 바로가기 아이콘 생성. 디폴트는 false
```

