# my_ci_cd_test
ci/cd 테스트


# CI 절차
    - github 사이트 이동 -> 현 프로젝트로 이동
    - Setting -> Security - Secrets and variable - Actions
    - new repository secret 버튼
        - git에 노출되면 안되는 정보들
        - 환경변수 (노출되면 안되는 키 정보, 디비 정보 등등)
        - aws 계정 관리 IAM에서 계정 별로 access ID/KEY 발급 받아서 등록 -> 외부에서 aws 엑세스 가능
        - action에 의해 .env 설정 파일로 이관
            - 소스코드 상에는 없다
        - 등록(필요한 만큼, 수시로)
            - 이름, 값

    - git action에서 작동한 내용 기술
        - deploy.yaml
        - 위치
            - 프로젝트루트/.github/workflows/deploy.yaml
            - gitaction을 작동시키는 이벤트(명령, 트리거)는 서브 브런치일 경우 아래처럼 추가 가능
                ```
                pull_request:
                    branches: [dev]
                ```
            - jobs -> step -> name => 검증할 내용들을 추가할 수 있다.
                - package.json 추가
                    - "build": "babel routes -d build"
                        - 개발된 소스를 표준으로 변환
                        - npm install --save-dev babel-cli
                        - npm run build