# 환경 설정

## FastAPI 개발환경 준비: conda 또는 venv

### conda
1. miniconda 다운로드 및 설치, Anaconda Prompt 실행 후
2. conda create -n fastapi_env python=3.12
3. conda activate fastapi_env
4. python -m pip install ipykernel
5. python -m ipykernel install --user --name fastapi_env --display-name "FastAPI kernel"  
   → 현재 활성화된 파이썬 환경(fastapi_env)을 Jupyter가 인식할 수 있는 커널로 등록하는 명령어
   
   * --user: 시스템 전체가 아니라 현재 사용자 계정에만 등록
   *  --name fastapi_env: 내부적으로 식별할 커널의 이름
   *   --display-name "FastAPI kernel": 사용자에게 보여지는 이름
     
// python이 실행되는 현재 가상환경을 이름 "fastapi_env"로 등록, 화면 표시는 "  
// conda와 Jupyter의 이름 체계는 별개임  

--display-name"로 지정
6. python -m pip install fastapi uvicorn
7. conda init powershell
→ PowerShell은 시작할 때마다 프로필(profile) 스크립트를 읽어서 설정 관련 작업을 실행
→ conda init powershell은 프로필 파일에 conda 관련 초기화 코드를 작성
→ 변경 사항이 적용되려면 powershell을 다시 시작해야 함
※ command prompt에서 사용하려면 conda init cmd.exe
8. conda config --set auto_activate_base false
→ PowerShell 시작 시, 기본 conda 환경 base를 자동으로 활성화하는데 이 설정을 끄는 명령
※ 이 설정은 전역 설정이므로 powershell/command prompt 둘 줄의 한 군데서만 하면 됨
※ 단계 7, 8이 필요한 이유
- 우리가 필요한 것은 uvicorn 프로그램임, uvicorn이 있어야 웹 서버가 돌아감
- uvicorn은 conda 가상환경에 설치되어 있으므로, 그 가상환경을 활성화 해야 함
- uvicorn은 셸에서 실행해야 하는데, 셸 중에서 powershell을 쓴다고 가정하면
- powershell에서 conda 명령어가 사용이 가능해야 함 (활성화를 해야 하므로) → 7번 단계
- 이 시점에서 powershell을 실행하면 auto_activate_base 설정의 기본값은 true이므로 conda base 가상환경이 자동으로 활
성화 됨 → 8번 단계
- 나중에 노트북에서 커널을 선택하거나, .py 파일에서 인터프리터를 선택하면, VS Code가 그 가상환경의 파이썬 실행 파일을 직
접 지정해서 코드를 실행하기 때문에, conda activate 필요없이 사용가능
