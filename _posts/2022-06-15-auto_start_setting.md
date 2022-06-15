---
layout: single
title:  "Ubuntu AUTO start setting"
---
# Ubuntu AUTO start setting 정리

본 포스팅은 Ubuntu에서 부팅시에 자동으로 프로그램을 실행 시키기 위한 setting 방법을 정리한 것. 

방법은 총 5가지가 있는데 본인에게 맞는 방법을 선택하면 된다.

## 1. Crontap 

Crontap은 Cron이라는 데몬이 어떤 프로그램을 자동으로 실행시킬지 적어놓는 리스트라고 보면된다. 

### Crontap 설정방법

in terminal 

```
crontab -e
```

