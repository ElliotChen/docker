# RabbitMQ

## Reference

[docker rabbitmq](https://hub.docker.com/_/rabbitmq)

## config

若要自行設定的參數較多，可用[rabbitmq.conf.example](https://raw.githubusercontent.com/rabbitmq/rabbitmq-server/master/docs/rabbitmq.conf.example)，另存檔後使用。

本docker採用此種方式，檔案置於```config```目錄下

```
    volumes:
      - ./config/rabbitmq.conf:/etc/rabbitmq/rabbitmq.conf
```

## management

使用的dockder image是帶有managenet介面的，
可透過[http://127.0.0.1:15672](http://127.0.0.1:15672)登入。

帳密預設為 guest/guest。
此部份可經由修改```./config/rabbitmq.conf```改變。

### 登入限制
自github下載的config sample是未開啟外網登入management，所以需修改下列設定，以便登入。

```
loopback_users.guest = false
```