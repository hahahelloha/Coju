# CoJu 修复版

## 运行
推荐 Python 3.12。Windows 解压后双击 start.bat，首次运行会安装依赖，然后打开本地网页。
若已有 Python 环境，也可运行：
```text
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

本地地址：http://localhost:8501 。需要让启动窗口保持运行。此地址不是公网分享链接。

## 测试
默认“离线示例”模式使用固定的3位上海成员和模拟数据。
真实测试：选择“真实地点查询” → 输入自己的高德 Web 服务 Key → 填写具体地点 → 点击“核对出发地点” → 逐人选择正确地点并勾选确认 → 点击“生成聚会方案”。
Key 不包含在本压缩包内，也不会写入源代码。程序将查询所需地点发送给高德服务。

菜系先选分类，再选具体菜系；多个菜系表示任一均可。不选表示不限。
公共交通优先模式不会改成驾车。短途无公交时可查询步行/骑行；也可以指定仅公共交通、步行或骑行。
修改地点、预算、菜系等条件后须重新生成；只调整推荐权重时使用已取得的候选重新排序，不再请求高德。
真实查询会调用多次接口。调试额度有限时，先用离线示例体验页面，避免反复生成。

## 文件
- app.py：界面、地点核对、状态更新和地图
- amap.py：高德接口与验证；无驾车/示例数据的静默兜底
- cuisines.py：分类、同义词、严格菜系匹配
- scoring.py：可解释评分与重新排序
- llm.py：基于真实结果的规则文案，以及暂未连接界面的可选自然语言解析函数
- mock_data.py：显式标注的模拟数据
- tests/：28项回归测试
- 修复说明.md：修改点与验证边界
- Demo_Day_Script_Revised_EN.md：与当前功能一致的英文演示稿

运行测试：python -m unittest discover -s tests -v
requirements.txt 固定已验证的直接依赖版本；requirements-lock.txt 记录本次 Windows / Python 3.12 完整测试环境。

