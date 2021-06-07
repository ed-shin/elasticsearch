## Snapshot Guide
```
elasticsearch version: 7.8
kibana version: 7.8
```

## flow
1. 환경변수 등록
2. snapshot repository 설정
3. snapshot 생성

### 1. 환경변수 등록
- [먼저, 엘라스틱서치를 실행하기 전에 환경변수 설정을 해야한다]
- `config/elasticsearch.yml` > `path.repo` 세팅
  - 윈도우인 경우와 유닉스 계열은 경로 구분자가 다르다: `unix: '/'` `windows: '\\'`
  - 엘라스틱서치 7.13 이후로 path.repo 입력 방법이 다르다
    - https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-register-repository.html
    - yaml의 설정 방식으로 입력하지 않고 기존과 같이 path.repo= ["/"] 와 같이 입력하는 경우 엘라스틱서치 실행시 parsing exception이 발생한다.
- [엘라스틱서치를 실행한다]

### 2. snapshot repository 설정
```
PUT _snapshot/[repository 명칭]
{
  "type": "fs",
  "settings": {
    "location": "[path.repo 경로]"
  }
}
```

### 3. snapshot 생성
```
PUT _snapshot/[repository 명칭]
{
  "indices": [index 명칭],
  "ignore_unavailable": true,
  "include_global_state": false
}
```
