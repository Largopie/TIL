# mac, Linux 3000포트 죽이기

```sh
# 원하는 포트 조회
$ lsof -i tcp:3000

# 해당 포트 죽이기
$ kill -9 PID
```