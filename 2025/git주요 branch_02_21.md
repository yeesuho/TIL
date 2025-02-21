###  1. master 브랜치
배포(운영) 환경에 사용되는 최종 안정적인 코드가 저장됨.
배포 가능한 코드만 병합됨.
일반적으로 release 또는 hotfix 브랜치만 master에 병합됨.

###  2. develop 브랜치
새로운 기능 개발이 이루어지는 브랜치.
feature 브랜치에서 작업한 후 병합됨.
배포가 준비되면 release 브랜치를 만들어서 관리함.
보통 master에서 분기되며, release 또는 hotfix가 끝나면 다시 병합됨.

###  3. feature 브랜치 (기능 개발)
특정 기능을 개발하는 브랜치 (feature/기능이름)
develop 브랜치에서 분기하여 작업함.
기능이 완성되면 develop 브랜치로 병합됨.
완료되면 보통 브랜치는 삭제됨.



###  4. release 브랜치 (배포 준비)
새로운 버전 배포를 위한 브랜치 (release/v1.0.0)
develop 브랜치에서 분기함.
여기서 버그 수정 및 최종 테스트를 진행한 후 master와 develop에 병합됨.
병합 후 브랜치는 삭제됨.




###  5. hotfix 브랜치 (긴급 수정)
운영 중인 master 브랜치의 버그를 긴급히 수정할 때 사용 (hotfix/버그이름)
master에서 분기하여 버그를 수정한 후 다시 master와 develop에 병합됨.
배포가 즉시 필요할 때 사용됨.

