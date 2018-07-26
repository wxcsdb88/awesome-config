# shadowsocks 使用

## download

`apt install shadowsocks`
or
`pip install shadowsocks`

## shadowsocks 文件创建

`vi /etc/shadowsocks.json`

```json
{
    "server":"0.0.0.0",
    "server_port":7788,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"loveu123",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```

## command

- 前台启动

`ssserver -c /etc/shadowsocks.json`

- 后台启动
  
`ssserver -c /etc/shadowsocks.json -d start`
or
`nohup ssserver -c /etc/shadowsocks.json >/dev/null 2>&1 &`

- 后台关闭
  
`ssserver -c /etc/shadowsocks.json -d stop`
