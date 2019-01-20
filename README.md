# docker
Docker Compose Sample


## Volume

將實體目錄或檔案對應Container裡的目錄或檔案

### 目錄對應

```
services:
  jenkins:
    image: jenkins/jenkins:lts
...
    volumes:
      - ./jenkins_home:/var/jenkins_home
```

在Container裡設定```volumes```，讓container裡的```/var/jenkins_home```對應到實際環境下的```./jenkins_home```

### 檔案對應

```
services:
  redis:
    image: redis:5
    ...
    volumes:
      - ./redis.conf:/usr/local/etc/redis/redis.conf
```

讓實際的```./redis.conf```取代Container裡的```/usr/local/etc/redis/redis.conf```，利用這樣來修改設定檔，就不用大量地增加```environment```。

### Container共用

要讓多個Container共用目錄，就必需在最外層設定Volume

```
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:6.5.4
    ....
    volumes:
      - esdata:/usr/share/elasticsearch/data

volumes:
  esdata:
    driver: local
```

此時docker會在系統的Volume裡建立一個特別的instance，使得其他的Container也能讀取到這個Volume.

常用的相關指令如下

```
#看目前docker有哪些volume

$ docker volume ls
DRIVER              VOLUME NAME
local               elk_esdata
local               f2bae14120c2531d90d0d01fe59916ef8cf5f164fc84dcb4b33833ee00fab523
```

```
# 檢視Volume的詳細資料

$ docker volume inspect elk_esdata
[
    {
        "CreatedAt": "2019-01-20T03:32:27Z",
        "Driver": "local",
        "Labels": {
            "com.docker.compose.project": "elk",
            "com.docker.compose.version": "1.23.2",
            "com.docker.compose.volume": "esdata"
        },
        "Mountpoint": "/var/lib/docker/volumes/elk_esdata/_data",
        "Name": "elk_esdata",
        "Options": null,
        "Scope": "local"
    }
]
```