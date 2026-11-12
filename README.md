# 分层台架故障率的精确验收与停止边界

本项目保存虚构台架测量表及Python读取工具。当前工具加载文件并检查输入，不执行统计检验、求解、配准或分析。所有仪器、试件、对象与人工标签均为合成。

## 字段与单位

trial_id为试次身份，stratum为工况；decision取failure/success/pending，received_at为人工判定获知时间。plan中的目标权重、误差预算与检查点事先确定，未决不作为成功。

material-index.json记录全部输入内容哈希；fixtures保存原始资料与配置，计算输出可放.workspace-output，原始资料不应被覆盖。

## 运行已有读取器

Python 3.11以上，标准库即可，不需安装第三方依赖。

    python -m src.reliability_reader fixtures/trials.csv
    python -m compileall -q src tests
    python -m unittest discover -s tests -v

## 固定容器

    docker build -t stratified-reliability:local .
    docker run --rm stratified-reliability:local

容器镜像以完整digest固定，默认仅检查输入契约；实现新增分析功能所需依赖由开发者明确登记。
