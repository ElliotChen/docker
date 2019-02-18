# Description

在Docker中提供ftp server，主要是為了測試功能用，避免另找機器安裝。

## 參考

[fauria/vsftpd](https://hub.docker.com/r/fauria/vsftpd/)

## 注意事項

1. ports 的設定中，不可省略```"```符號。

```
    ports:
      - "20:20"
      - "21:21"
      - 21100-21110:21100-21110
```

