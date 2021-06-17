# 免费的天气API

## 高德地图天气

[天气查询-API文档](https://lbs.amap.com/api/webservice/guide/api/weatherinfo#weatherinfo)

请求示例：

```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "上海",
            "city": "上海市",
            "adcode": "310000",
            "weather": "阵雨",
            "temperature": "25",
            "winddirection": "东",
            "windpower": "≤3",
            "humidity": "100",
            "reporttime": "2021-06-17 16:31:17"
        }
    ]
}
```



## 天气API 免费(仅限个人测试每日300次)

[免费实况天气接口API开发指南](https://www.tianqiapi.com/index/doc?version=v6)

请求示例：

```json
{
    "cityid": "101010100",
    "date": "2021-06-17",
    "week": "\u661f\u671f\u56db",
    "update_time": "2021-06-17 16:48",
    "city": "\u5317\u4eac",
    "cityEn": "beijing",
    "country": "\u4e2d\u56fd",
    "countryEn": "China",
    "wea": "\u6674",
    "wea_img": "qing",
    "tem": "32",
    "tem1": "33",
    "tem2": "19",
    "win": "\u897f\u98ce",
    "win_speed": "3\u7ea7",
    "win_meter": "12km\/h",
    "humidity": "16%",
    "visibility": "30km",
    "pressure": "997",
    "air": "31",
    "air_pm25": "31",
    "air_level": "\u4f18",
    "air_tips": "\u7a7a\u6c14\u5f88\u597d\uff0c\u53ef\u4ee5\u5916\u51fa\u6d3b\u52a8\uff0c\u547c\u5438\u65b0\u9c9c\u7a7a\u6c14\uff0c\u62e5\u62b1\u5927\u81ea\u7136\uff01",
    "alarm": {
        "alarm_type": "",
        "alarm_level": "",
        "alarm_content": ""
    }
}
```



待补充...