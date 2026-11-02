<p align="center">
  <img src="assets/logo.png" width="160" alt="MTM Logo">
</p>

<h1 align="center">Metalworking Training Management System（金工实习管理系统）</h1>

<p align="center"><b>面向高校金工实习场景的全流程管理控制台应用</b></p>

<p align="center">
  围绕「设备 — 人员 — 安全 — 成绩」四条主线，覆盖注册审批、设备预约与签到、<br>
  安全考试资格、故障报修闭环、工时成绩管理与实习证明开具，数据以 CSV 持久化。
</p>

<p align="center">
  <img src="https://img.shields.io/badge/release-v1.0-blue" alt="release">
  <img src="https://img.shields.io/badge/platform-Windows%2010%2F11-blue" alt="platform">
  <img src="https://img.shields.io/badge/language-C-555555" alt="language">
  <img src="https://img.shields.io/badge/license-CC--BY--NC--SA%204.0-orange" alt="license">
</p>

<p align="center">
  <a href="https://ifvxavb5oowr6.ok.kimi.link/"><img src="https://img.shields.io/badge/🔗%20在线演示-live%20demo-brightgreen" alt="在线演示"></a>
</p>

<p align="center">
  <a href="#下载">下载</a> · <a href="#功能一览">功能一览</a> · <a href="#从源码构建">从源码构建</a> · <a href="https://ifvxavb5oowr6.ok.kimi.link/">在线演示</a>
</p>

- **账户**：注册审批制，管理员 / 教师 / 学生三角色，登录三次失败锁定
- **设备**：设备台账管理、利用率报表、检修记录与保养到期预警
- **安全**：安全考试合格名单管理、资格剥夺、合格名单一键导出 PDF
- **报修**：故障报修闭环（报修 → 派修 → 完工验收），进度可查
- **预约**：设备按时段预约、到场签到、取消 / 改期
- **成绩**：教师录入工时与成绩，班级 / 个人维度统计导出
- **证明**：实习证明 LaTeX 自动生成，调用 pdflatex 编译输出 PDF
- **数据**：CSV 文件持久化（`data/` 目录，随安装包分发），管理员数据备份
- **审计**：全量操作日志记录与审计
- **UI**：Windows 控制台多主题配色（欢迎 / 登录 / 管理员 / 教师 / 学生），居中排版

## 下载

- **在线演示**：<https://ifvxavb5oowr6.ok.kimi.link/> —— 项目演示站点（建设中，仅供预览，以本地安装版功能为准）
- **本地安装**：下载 `金工实习管理系统_setup.exe`，双击安装即可（Windows 10 / 11，64 位）。

安装包由 Inno Setup 生成，内置中文安装向导，可选创建桌面快捷方式；数据文件随安装目录分发，无需额外配置。

## 功能一览

### 管理员

- 查看所有用户、注册申请审批（通过 / 驳回）
- 设备信息管理（查看 / 添加 / 删除）
- 检修记录与保养预警
- 安全考试名单管理与合格名单 PDF 导出
- 故障报修闭环处理：派修、完工验收
- 操作日志审计、设备利用率报表、数据备份、系统设置

### 教师

- 查询学生信息、录入成绩 / 工时
- 班级 / 个人工时与成绩统计导出
- 设备利用率报表、设备预约（含签到、取消 / 改期）
- 故障报修与进度查看
- 安全考试名单导入、安全资格剥夺

### 学生

- 查询个人工时与成绩、设备预约、我的预约
- 取消 / 改期预约、签到
- 实习证明开具、个人信息与安全考试合格情况查看

## 从源码构建

依赖：MinGW-w64（GCC）与 Inno Setup 6。

```bash
# 1. 编译主程序（Windows，MinGW-w64）
gcc main.c admin.c cert.c device.c log.c maint.c repair.c reserve.c \
    safety.c student.c teacher.c ui.c user.c utils.c work.c \
    -o main.exe -O2 -std=c99

# 2. 编译安装包（可选）
iscc setup.iss
```

生成的 `金工实习管理系统_setup.exe` 位于 `output/` 目录。

> **提示**：实习证明 PDF 导出依赖本机安装 TeX Live 或 MiKTeX（提供 `pdflatex`）。未安装时会退化为输出 LaTeX 源文件并提示手动编译。

## 目录结构

```
├── main.c / main.exe     # 程序入口与主循环
├── login.h / login.c     # 数据结构与账户体系（用户、预约、检修、安全、报修、工时、日志）
├── admin.c               # 管理员功能
├── teacher.c             # 教师功能
├── student.c             # 学生功能
├── device.c              # 设备台账与利用率
├── reserve.c             # 预约与签到
├── repair.c              # 故障报修闭环
├── maint.c               # 检修记录与保养预警
├── safety.c              # 安全考试资格
├── cert.c                # 实习证明（LaTeX → PDF）
├── work.c                # 工时与成绩
├── user.c / log.c        # 用户管理 / 操作日志
├── ui.c / utils.c        # 控制台主题与工具函数
├── setup.iss             # Inno Setup 安装包脚本
└── data/                 # CSV 数据文件（随程序加载）
```

## License

本作品采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可。

---

<p align="center">(C) Wing North Studio 2026 · WS3105 课程设计 · 仅供学习交流，谢绝一切商业用途</p>
