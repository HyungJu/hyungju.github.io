# macOS PHP libffi Library not loaded 오류 해결하기

PHP를 오랫동안 쓰지 않고 실행하는데 아래와 같은 오류가 발생했다 🤭


`dyld: Library not loaded: /usr/local/opt/libffi/lib/libffi.6.dylib
  Referenced from: /usr/local/bin/php
  Reason: image not found
[1]    39507 abort      php`



얼마 전에 Make 빌드 환경을 새로 설정하는 과정에서 문제가 생긴 모양이다.

----


터미널에서  `brew switch libffi 3.2.1` 명령을 입력하는것으로 해결했다. 🥳🥳

