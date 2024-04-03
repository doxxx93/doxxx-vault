---
date_created: 2024-03-25 20:39
author: 
date_published: 
url:
---
# synchronized

멀티 스레드 환경에서는 두 개 이상의 스레드가 동시에 변경 가능한 공유 데이터를 업데이트하려고 시도할 때 경쟁 조건([Race Condition](Race%20Condition.md))이 발생합니다. Java는 공유 데이터에 대한 스레드 액세스를 동기화하여 경쟁 조건을 피할 수 있는 메커니즘을 제공합니다.

동기화됨으로 표시된 로직은 동기화된 블록이 되어 주어진 시간에 하나의 스레드만 실행할 수 있습니다.
