# Git Flow

2025.02.21
<br>

## Git Flow란 무엇일까?
<br>
Git Flow는 Git을 활용한 브랜치 전략 중 하나로, <u>Vincent Driessen이</u> 제안한 워크플로우
<br>
**여러 개발자가 동시에 협업할 때 효율적인 브랜치 관리를 위해 사용됨**
<br><br>

### Git Flow의 특징<br>

[master, develop, feature, release, hotfix](/2025/git주요%20branch_02_21.md) 
브랜치를 활용하여 코드 변경 사항을 체계적으로 관리.
개발, 테스트, 배포 단계를 명확하게 구분.
안정적인 코드만 운영(master) 브랜치에 반영.
긴급 수정(hotfix) 시에도 안정성을 유지하면서 빠르게 배포 가능.
<br><br>


## 📌 Git Flow 브랜치 흐름 정리 (merge 병합)

         feature → develop → release → master
                     ↑         ↓        ↓
                    (merge)  (merge)  (merge)
                            hotfix → master
                                ↓
                             develop
이런 방식으로 브랜치를 관리하면 여러 명이 협업할 때 코드가 깔끔하게 정리되고, 안정적인 배포가 가능

<br>



## ⚪️ Git Flow의 장점 & 단점 <br>

✅ 장점
<br>✔ 체계적인 브랜치 관리 가능
<br>✔ 여러 개발자가 협업하기 쉬움
<br>✔ 긴급 수정(hotfix)도 안정적으로 처리 가능
<br>✔ 개발과 운영(배포) 환경을 분리하여 안정성 유지

❌ 단점
<br>✖ 작은 프로젝트에서는 너무 복잡할 수 있음
<br>✖ 브랜치가 많아지면서 관리가 어려울 수도 있음
<br>✖ CI/CD(자동 배포)를 활용하는 경우 Git Flow보다 GitHub Flow나 Trunk-based Development가 더 적합할 수도 있음

