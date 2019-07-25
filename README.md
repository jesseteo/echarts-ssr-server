# Echarts 服务器端生成图片服务


作者：jessezhang007007 <jessezhang007007@gmail.com>

github地址：https://github.com/jessezhang007007/echarts-ssr-server

Docker Hub 地址：https://hub.docker.com/r/jessezhang007007/echarts-ssr-server/


## 一、说明：

Echarts server side render by node canvas, generate chart image by Echarts.

使用NodeJs服务器端渲染echarts图表，生成图片格式。

## 二、安装

### 方式一：使用Docker运行

```
docker run -d -p 8081:8081 --name echarts-ssr-server --restart=always jessezhang007007/echarts-ssr-server
```


### 方式二：本地Node运行

#### 1. 安装依赖

操作系统 | 安装命令
----- | -----
OS X | `brew install pkg-config cairo pango libpng jpeg giflib`
Ubuntu | `sudo apt-get install libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev build-essential g++`
Fedora | `sudo yum install cairo cairo-devel cairomm-devel libjpeg-turbo-devel pango pango-devel pangomm pangomm-devel giflib-devel`
Solaris | `pkgin install cairo pango pkg-config xproto renderproto kbproto xextproto`
Windows | [Instructions on our wiki](https://github.com/Automattic/node-canvas/wiki/Installation---Windows)

#### 2. 下载并安装

```bash
git clone git@github.com:jessezhang007007/echarts-ssr-server.git
cd echarts-ssr-server
npm install
npm start
```


## 三、访问服务
### 1. 访问方式：使用http请求访问服务

### 2. 请求参数格式：
```javascript
{
    "width": 800,
    "height": 500,
    "option": {
    	"backgroundColor": "#fff",
        "xAxis": {
            "type": "category",
            "data": [
                "Mon",
                "Tue",
                "Wed",
                "Thu",
                "Fri",
                "Sat",
                "Sun"
            ]
        },
        "yAxis": {
            "type": "value"
        },
        "series": [
            {
                "data": [
                    820,
                    932,
                    901,
                    934,
                    1290,
                    1330,
                    1320
                ],
                "type": "line"
            }
        ]
    }
}
```

参数JSON里的第一层属性说明：

|属性名|类型|默认值|说明|
|---|---|---|---|
|width|Number|600|图片宽度|
|height|Number|400|图片高度|
|option|Object|{}|Echarts 的 Option 配置，参考Echarts文档|

### 3. GET方式访问

注意：GET方式只适合参数数据量小的情况，参数数据量大的时候请使用POST方式。

```
http://localhost:8081/?config=%7B%22width%22%3A800%2C%22height%22%3A500%2C%22option%22%3A%7B%22backgroundColor%22%3A%22%23fff%22%2C%22xAxis%22%3A%7B%22type%22%3A%22category%22%2C%22data%22%3A%5B%22Mon%22%2C%22Tue%22%2C%22Wed%22%2C%22Thu%22%2C%22Fri%22%2C%22Sat%22%2C%22Sun%22%5D%7D%2C%22yAxis%22%3A%7B%22type%22%3A%22value%22%7D%2C%22series%22%3A%5B%7B%22data%22%3A%5B820%2C932%2C901%2C934%2C1290%2C1330%2C1320%5D%2C%22type%22%3A%22line%22%7D%5D%7D%7D
```

### 4. POST方式访问

```
curl -X POST \
  http://localhost:8081/ \
  -o echart-image.png \
  -d '{
    "width": 800,
    "height": 500,
    "option": {
    	"backgroundColor": "#fff",
        "xAxis": {
            "type": "category",
            "data": [
                "Mon",
                "Tue",
                "Wed",
                "Thu",
                "Fri",
                "Sat",
                "Sun"
            ]
        },
        "yAxis": {
            "type": "value"
        },
        "series": [
            {
                "data": [
                    820,
                    932,
                    901,
                    934,
                    1290,
                    1330,
                    1320
                ],
                "type": "line"
            }
        ]
    }
}'
```

