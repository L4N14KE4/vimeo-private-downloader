# Vimeo 비공개 동영상 다운로더 한국어 번역판

> 안녕하세요! 이 Repository는 [Vimeo Private Video Downloader](https://github.com/Tusko/vimeo-private-downloader)를 기반으로, 한국어 번역과 윈도우 사용자에 맞게 내용을 보완하였습니다. 또한 vimeo-combine.bat 파일을 추가하였습니다.<br>
제 지식의 한계로 인해 오역/오류가 있을 수 있습니다. 이해 부탁드립니다.
<br> 
docker test 안함

#### Node.js 스크립트를 사용하면 [Vimeo](https://vimeo.com)에서 비공개 동영상을 다운로드할 수 있습니다.

## 요구사항
1. Node.js

    시작하기 전에 [Node.js](https://nodejs.org/en/download/)를 설치했는지 확인해주세요.

    확인하려면 터미널(cmd)에서 `node -v` 명령을 실행하세요. 예를 들어 `v10.11.0`이 표시됩니다. 에러가 발생하면 최신 [Node.js](https://nodejs.org/en/download/)를 설치해주세요.

2. ffmpeg

    `ffmpeg`를 설치해주세요. [여기](https://ffmpeg.org/download.html)에서 다운로드할 수 있습니다.
    비디오/오디오 조각들을 결합하고 mp4로 변환하는데 필요합니다.

    확인하려면 터미널에서 `ffmpeg -version` 명령을 실행하세요. 예를 들어 `ffmpeg version 5.1.2`이 표시됩니다. 

## 다운로드 방법

비공개 동영상을 받으실 때는 아래의 단계들을 따라주시면 됩니다.

1. 네트워크 탭에서 브라우저 개발자 도구를 열어주세요.<br>
    (윈도우/리눅스의 경우 `F12`, 맥 OS의 경우 `CMD + Option + I`).

2. 동영상 재생을 시작하세요.(또는 마우스 커서를 동영상 위에 올리세요)

3. 네트워크 탭에서 `master.json` 파일의 로드를 찾아 **전체 URL**을 복사합니다.
- 경우에 따라 Vimeo에서 암호화된 동영상 데이터를 전송하는 경우가 있습니다.

    **해결방법**
> 1. `query_string_ranges` 쿼리 파라미터를 제거
> 2. `base64_init=1`을 추가

<br>

4.  `videojson.js` 파일에 복사한 `url`과 원하는 파일명인 `name`필드를 채워주세요.

5.  터미널에서 `node index.js` 또는 `npm run start` 명령을 실행하세요.

6.  콘솔에 `🌈 List finished` 메시지가 출력될때까지 기다리세요.

7.  `parts` 폴더에 비디오/오디오 segment(조각)가 저장됩니다.

## 결합 및 변환

1. 비디오/오디오 segment를 하나의 `mp4` 파일로 합치고 변환하려면 터미널에서 `sh vimeo-combine.sh` 또는 `npm run combine`을 실행하세요.
윈도우에서 sh 명령어 사용이 불가능하다면 cmd에서 `vimeo-combine.bat`을 실행하세요.

- 1.1. `vimeo-combime.bat`이 작동하지 않는 경우, ffmpeg의 PATH 설정을 확인하시거나, `vimeo-combine.bat` 파일 위치로 `ffmpeg.exe`를 이동하여 실행해보세요.

2. converted 폴더에 완성된 `mp4` 파일이 생성됩니다.

새 영상 작업 전에 이전 영상 segment는 삭제하는 것이 좋습니다.<br>
(명령 실행시마다 convented 폴더 내부의 모든 파일이 변환됨)

## Docker 설정

이 Repository에는 Node 18이 설치된 Alpine 이미지를 사용하는 Dockerfile이 있습니다. 

다음과 같은 몇 가지 Makefile 명령이 추가되었습니다.
- `make build`: `ffmpeg` OS 종속성을 설치하는 `FROM node:18-alpine` Docker 이미지를 빌드합니다.
- `make start`: `npm run start` entrypoint 실행
- `make convert`: `npm run convert` entrypoint 실행
- `make bash`: 실행 중인 컨테이너에서 sh 명령 실행

<hr></hr>

### (원 Repo의) 기여자

기여자에게 특별한 감사를 전합니다:
[@ftitreefly](https://github.com/ftitreefly/) - 비디오/오디오 부분을 `mp4`로 병합하는 bash 스크립트 생성