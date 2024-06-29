---
Date: 2023-08-19
Type: TIL
Tags: TIL
---

https://stackoverflow.com/questions/29955500/code-is-not-working-in-on-the-command-line-for-visual-studio-code-on-os-x-ma

`sudo vi /etc/paths` 커멘드라인으로 path를 아래와 같이 설정해주었다. 
`export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"`

`which code` 명령어를 입력했을 때, `/usr/local/bin/code` 과 같이 나와야한다.

