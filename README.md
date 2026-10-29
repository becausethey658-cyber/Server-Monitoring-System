# Server-Monitoring-System
服务器巡检管理软件 V1.0一个面向运维场景的桌面端 GUI 演示原型：以服务器资产台账为基础，通过「巡检模板 → 巡检计划 → 巡检任务 → 异常工单 → 报表」的闭环，展示服务器巡检管理的完整工作流。配套文档：《服务器巡检管理软件 V1.0 操作手册》（DOCX / PDF，48 页，含 13 张界面截图与架构、流程图）。快速启动环境要求：Windows 10/11 x64，Python 3.10+（推荐 3.14），Tk 8.6。双击「启动软件.bat」
或在当前目录执行：python run.py
演示包已内置 CustomTkinter、darkdetect 与 Windows x64 / Python 3.14 对应的 Pillow，无需联网安装。若使用其他 Python 版本，请先安装 Pillow：python -m pip install pillow customtkinter
功能模块工作台：服务器总数、在线率、今日巡检、待处理异常，健康度环图、7 日趋势、待办与实时告警。服务器资产：12 条/页的资产清单，按名称/IP/机房/系统/状态筛选；新增服务器、查看详情、单机巡检。巡检模板：4 套模板（Linux 主机、MySQL、Nginx、安全基线），检查项、采集方式、判定标准与级别。巡检计划：10 个计划，展示频率、下次执行、通知方式与启停状态。巡检任务：任务列表、状态筛选、进度条、发起巡检弹窗、任务详情与实时日志（模拟进度自动推进）。异常工单：分级、SLA、工单列表、处置时间线、影响评估、知识库建议、一键闭环。报表中心：月报预览、任务趋势、异常分布、重点异常、报告模板与最近归档。系统设置：通知渠道、通知策略、最近通知、基础设置、用户与角色、审计日志。演示说明所有服务器、IP、人员、机房和指标均为虚构数据。数据保存在内存中；关闭程序后新增资产等临时操作不会持久化。界面右上角固定展示「演示环境」，避免与生产数据混淆。程序不会连接外部服务器，也不会执行真实的 SSH 命令。分辨率建议 1920×1080；最小窗口 1180×720。目录结构run.py                       启动入口（注入 vendor 路径）
启动软件.bat                 双击启动
server_inspection/
  app.py                     主窗口、页面与业务流程
  components.py             卡片、按钮、弹窗等基础组件
  table.py                  列宽严格对齐的数据表
  charts.py                 PIL 绘制的环图、趋势图、柱状图
  icons.py                  线性图标与品牌 Logo
  theme.py                  色彩与字体规范
  data.py                   演示数据
  capture.py                自动截图脚本
vendor/                     内置运行依赖
screenshots/raw/            原始界面截图
screenshots/annotated/      带编号标注的截图
assets/                     手册封面、架构图、流程图
manual_kit.py               手册排版工具
manual_content.py           手册正文
build_manual.py             构建 DOCX / PDF
build_manual_assets.py      生成封面、图表与标注
复现手册在已配置 Python 3.10+ 与 python-docx、pypdf 的环境中执行：python build_manual.py
脚本会生成 服务器巡检管理软件V1.0-操作手册.docx，经 LibreOffice Kit 转换后回填目录页码，并导出同名 PDF。手册中的截图来自 screenshots/annotated/。已知范围这是交互原型而非生产系统。模板/计划的新建入口保留界面反馈，资产新增、筛选、模板切换、任务下发与工单闭环可实际体验；真实采集、鉴权、持久化、审批与通知通道需在生产版中接入。