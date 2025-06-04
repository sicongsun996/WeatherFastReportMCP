# ChinaWeatherMCP - 中国天气快报Agent

## 项目概述
基于MCP协议的中国天气快报服务，提供精准的天气预报数据采集、处理和推送功能。支持通过微信自动发送天气预警和预报信息。

## 功能特性
- 多时间尺度天气预报（24小时/3天/7天/15天/30天）
- 支持多种查询方式（城市名称、经纬度、LocationID、Adcode）
- 微信自动推送功能
- 覆盖全国所有城市和区县的详细地理编码数据
- 基于MCP协议的标准化服务接口

## 安装部署

### 前置要求
- Python 3.10+
- UV工具链

### 安装步骤
1. 克隆仓库：
   ```bash
   git clone https://github.com/your-repo/ChinaWeatherMCP.git
   cd ChinaWeatherMCP
   ```

2. 安装依赖：
   ```bash
   uv pip install -e .
   ```

3. 启动MCP服务：
   ```bash
   uv --directory . run china_weather_forecast2025022.py
   ```

## 使用说明

### 天气预报查询
通过MCP工具`fastreport_in_word`查询天气：
```python
{
  "location": "北京",  # 或"116.40,39.90"
  "time": "24h",      # 24h/3d/7d/10d/15d/30d
  "interval": 6       # 可选，时间间隔
}
```

### 微信通知配置
1. 修改wechat.py中的微信配置
2. 使用`send_text`或`send_files`工具发送消息

## 数据文件
- `China-City-List-latest.csv`: 中国城市列表
- `geo-json/`: 全国行政区划地理编码数据

## 示例
```python
# 获取北京未来24小时天气预报
response = mcp_tool(
    server="weather_fast_report",
    tool="fastreport_in_word",
    arguments={
        "location": "北京",
        "time": "24h"
    }
)

# 通过微信发送预警
mcp_tool(
    server="wechat",
    tool="send_text",
    arguments={
        "text": "北京将有大到暴雨，请注意防范",
        "nick_name": "天气预警群"
    }
)
```

## 许可证
本项目采用 [MIT License](LICENSE) 开源协议
