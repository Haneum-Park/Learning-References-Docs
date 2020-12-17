## rbenv 설치

`rbenv`을 이용하여 루비를 설치할 것을 권고

### 맥 OS X

```bash
$ brew update
$ brew install rbenv
```

새로운 루비 버전이 릴리스된 후에는 아래와 같이 명령을 실행한 후

```bash
$ brew upgrade ruby-build
```

다음의 명령을 실행하여 설치할 수 있는 루비 비전을 확인

```bash
$ rbenv install -l
```

```bash
$ rbenv install 2.3.3 && rbenv rehash
```

각각의 필요성에 따라 `global`, `local`, `shell` 옵션을 이용하여 루비 버전을 지정

```bash
$ rbenv global 2.3.3
```



### 리눅스

```bash
$ git clone git://github.com/sstephenson/rbenv.git .rbenv
```

명령 프롬프트에서 `rbenv`를 실행할 수 있게 쉘 환경변수를 수정. `.bashrc` 파일을 읽어들일 수 있도록 편집기를 열어서 `.bash_profile`에 다음과 같이 추가

```bash
[ -f "$HOME/.profile" ] && source "$HOME/.profile"
[ -f "$HOME/.bashrc" ] && source "$HOME/.bashrc"
```

`.bashrc` 내용은 다음과 같이 작성. `rbenv`가 저장된 디렉토리를 `RBENV_ROOT` 환경 변수에, `rbenv` 실행 파일이 들어 있는 디렉토리를 `PATH`에 추가

쉘을 실행할때마다 `rbenv init -` 명령을 실행

```bash
export RBENV_ROOT="${HOME}/.rbenv"
if [ -d "${RBENV_ROOT}" ]; then
  export PATH="${RBENV_ROOT}/bin:${PATH}"
  eval "$(rbenv init -)"
fi
```

루비를 설치하기 위해서는 `rbenv`의 플러그인 `ruby-build`가 필요하다. `.rbenv/plugins` 디렉토리를 생성하고 `github`에서 `ruby-build`를 받아온다.

```bash
$ mkdir -p ~/.rbenv/plugins
$ cd ~/.rbenv/plugins
$ git clone git://github.com/sstephenson/ruby-build.git
```

`install` 옵션을 사용해서 루비를 설치해보자. 여기서는 `2.0.0-p451` 버전을 설치했다.

```sh
$ rbenv install 2.0.0-p451
```

`rehash` 옵션은 새로운 환경을 재설정하는 옵션으로 새로 루비를 설치하거나 루비 젬을 설치한 다음 반드시 실행해야 한다.

```sh
$ rbenv rehash
```

`global` 옵션은 전역 설정을 변경하는 옵션으로 시스템에서 해당 버전의 루비를 사용하기 위해 사용한다.

```sh
$ rbenv global 2.0.0-p451
```

설치하고자 했던 루비 버전이 제대로 설치되었는지 확인해보자.

```sh
$ ruby -v
ruby 2.0.0p451 (2014-02-24 revision 45167) [x86_64-linux]
```

루비 설치가 끝났으면 루비 젬을 관리하기 위해 `bundler`를 설치한다. 새로운 환경을 재설정하기 위해 `rehash`를 잊지 말자.

```sh
$ gem install bundler
$ rbenv rehash
```



### 윈도우

윈도우에서는 `rbenv`을 사용할 수 없다. 관련 문서에 의하면, 대신에 [RubyInstaller](http://rubyinstaller.org/) 또는 [Pik](https://github.com/vertiginous/pik)를 사용할 것을 권한다.