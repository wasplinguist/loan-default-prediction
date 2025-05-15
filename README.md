# 대출 연체 예측 (Loan Default Prediction)

ML(머신러닝) 모델의 학습, 테스트, 배포를 위한 소프트웨어 엔지니어링 실습을 위한 엔드 투 엔드 예시입니다.  
이 프로젝트는 대출 연체 가능성을 예측하는 ML 모델을 학습시키고 서빙합니다.

---


## 설정 (Setup)

Go 스크립트를 실행하여 필수 종속성을 설치합니다.  
Go 스크립트는 Python 3과 Poetry를 설치하고, 호스트에 가상 환경을 생성합니다.  
이렇게 하면 IDE에서 해당 프로젝트의 Python 인터프리터를 인식할 수 있습니다.

```shell
# Mac 사용자의 경우
scripts/go/go-mac.sh

# Linux 사용자의 경우
scripts/go/go-linux-ubuntu.sh

# Windows 사용자의 경우
# 1. Python3을 설치하지 않았다면 다운로드하고 설치하세요: https://www.python.org/downloads/release/python-31011/
#    - 설치 시, "Add Python to PATH" 옵션을 선택하세요.
# 2. Windows 탐색기 또는 검색에서 'Manage App Execution Aliases'로 이동하여, 'App Installer'의 python 항목을 비활성화하세요. 
#    이는 `python` 실행 파일이 PATH에서 인식되지 않는 문제를 해결합니다.
# 3. Powershell 또는 Command Prompt에서 Go 스크립트를 실행합니다.
.\scripts\go\go-windows.bat
# 참고: 만약 HTTPSConnectionPool read timed out 에러가 발생한다면, poetry 설치가 성공할 때까지 몇 번 더 실행해 보세요.
```

## Docker 런타임 설치 및 설정

### - 옵션 1: **Docker Desktop** 사용  
Docker Desktop 라이선스가 있거나, 개인 또는 교육용 목적으로 무료로 사용할 수 있다면 사용합니다.  
[Docker Desktop 라이선스 약관](https://docs.docker.com/subscription/desktop-license/)을 참조하세요.
- 설치 방법: https://docs.docker.com/desktop/

### - 옵션 2: **Colima** 사용  
Colima는 Docker Desktop의 라이선스가 필요 없는 Docker 런타임입니다.  
상업적 환경에서 Docker Desktop을 사용할 수 없을 때 유용합니다.  
- 설치 방법:
    - https://gist.github.com/jcartledge/0ce114e9719a62a4776569e80088511d
    - https://github.com/abiosoft/colima

> **참고:**  
> 이 예제에서는 Docker Desktop 라이선스가 없을 경우를 대비해 **Option 1 (Colima)**를 사용합니다.

---

## IDE 설정  
Go 스크립트가 생성한 가상 환경을 IDE에 설정하세요.  
- [PyCharm 설정 방법](https://www.jetbrains.com/help/pycharm/creating-virtual-environment.html#existing-environment)
- [VS Code 설정 방법](https://code.visualstudio.com/docs/python/environments)

---

## 시작하기 (Getting started)

로컬 개발 환경을 빌드하고 시작합니다.

```shell
# Docker 런타임을 실행합니다 (Docker Desktop 또는 Colima 중 하나). Colima를 사용할 경우:
colima start

# 로컬 개발 이미지에 종속성 설치
./batect --output=all setup

# 컨테이너 시작 (로컬 개발 환경)
./batect start-dev-container

Here are common tasks that you can run in the dev container during development.

```shell
# run model training smoke tests
scripts/tests/smoke-test-model-training.sh

# train model
scripts/train-model.sh 

# run api tests
scripts/tests/api-test.sh

# exit container
exit # or hit Ctrl + D
```

You can also run these as batect tasks from the host (e.g. `./batect train-model`, `./batect api-test`) 

For the following commands, you have to run it as batect tasks because the port mappings are defined at the level of each task. For example, in `batect.yml`, the `start-jupyter` task exposes port 8888 and makes it accessible from the host.

if you don't need
```sh
# start jupyter notebook
./batect start-jupyter

# start API in development mode
./batect start-api-locally

# send requests to API locally (run this from another terminal outside of the Docker container, as it uses curl, which we haven't installed)
scripts/request-local-api.sh
```

## Sources and attributions

- original data: https://www.kaggle.com/competitions/will-they-default-devday19/data
