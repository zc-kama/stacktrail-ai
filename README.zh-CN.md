# StackTrail

沿着项目链路开发，把改动真正交付出去。

StackTrail 是一套可迁移的 AI 项目开发工作流。它让 AI 编程助手不只是“凭空写代码”，而是先读项目记忆，顺着前端、后端、数据库、配置、部署等链路理解现有系统，再做最小完整改动、验证受影响层级，并把长期有用的项目事实写回项目记忆。

它适合真实项目开发，尤其是这些场景：

- 前后端分离项目
- 全栈功能开发
- 接口联调
- 数据库表和历史数据设计
- 文件上传、下载、静态资源映射
- 登录鉴权、日志、缓存、配置
- Nginx、Linux、jar、容器或其他部署排查
- 多个 AI 编程工具之间迁移同一套开发习惯

## 为什么需要 StackTrail

很多 AI 写代码翻车，不是因为不会语法，而是因为没有先追完整链路。

比如一个看起来很简单的页面需求，真实路径可能是：

```text
UI/component
 -> API/client helper
 -> route/controller
 -> request DTO/schema
 -> service/use-case
 -> repository/mapper/storage
 -> response DTO/schema
 -> UI state
```

如果只改最显眼的页面文件，很容易出现：

- 前端能编译，但接口不通
- 后端字段改了，前端还在读旧字段
- 新功能能跑，但破坏了旧数据
- 本地没问题，部署环境路径、端口、配置全错
- 日志、上传、下载、权限这些边角处反复踩坑

StackTrail 的目标不是增加流程负担，而是让 AI 在动手前先知道“数据从哪里来，到哪里去，谁在消费它”。

## 包含内容

- `skills/stacktrail/`：Codex skill 版本
- `prompts/universal.md`：通用 AI 编程工具版本
- `prompts/claude-code.md`：Claude Code / `CLAUDE.md` 版本
- `prompts/openclaw.md`：OpenClaw 和其他 Coding Agent 版本
- `docs/name-research.md`：命名选择记录

## 安装到 Codex

把 skill 目录复制到 Codex skills 目录：

```bash
cp -R skills/stacktrail ~/.codex/skills/stacktrail
```

Windows PowerShell：

```powershell
Copy-Item -Recurse .\skills\stacktrail "$env:USERPROFILE\.codex\skills\stacktrail"
```

然后这样调用：

```text
Use $stacktrail to implement, verify, and document this project change end to end.
```

中文也可以直接说：

```text
Use $stacktrail 帮我把这个功能从代码实现到验证完整做完。
```

## 用在其他 AI 工具

如果不是 Codex，可以把对应提示词复制到项目说明文件里：

- Claude Code：把 `prompts/claude-code.md` 放进 `CLAUDE.md`
- OpenClaw：使用 `prompts/openclaw.md`
- 其他 AI 编程工具：使用 `prompts/universal.md`

## 核心工作流

1. 先读项目记忆和当前代码。
2. 判断任务类型：实现、调试、重构、部署、解释、更新记忆。
3. 判断影响层级：前端、后端、数据库、部署，还是跨层功能。
4. 跨层任务先追完整链路，再改代码。
5. 保留现有接口契约、鉴权方式、返回结构、数据约定和部署假设。
6. 做最小完整改动，不为了小问题引入大重构。
7. 根据影响范围做构建、编译、测试、浏览器、接口、数据库或部署验证。
8. 如果产生了长期事实，就更新项目记忆。

## 核心原则

- 先读现有项目，再决定怎么改。
- 优先沿用项目已有风格，而不是展示新架构。
- 前端接口、后端路由、DTO、Service、Mapper/Repository、数据库和页面渲染要连起来看。
- 当前状态、历史流水、快照、日志、统计、文件存储要分清楚。
- 部署问题先看进程、端口、日志、配置和依赖，不要靠猜乱改配置。
- 用户在学习时，从当前文件、当前页面或当前错误讲起，再逐步展开。

## 适合放进项目记忆的内容

当任务完成后，如果有这些变化，应该写进项目记忆：

- 新增或修改的接口
- 请求参数、返回字段、鉴权方式
- 表结构、索引、历史数据规则
- 上传目录、下载方式、静态资源路径
- 配置项、环境 profile、部署命令
- 日志、缓存、会话、权限规则
- 可重复的排查经验

不要把完整聊天记录塞进项目记忆。只记录未来开发真的会用到的事实。

## License

MIT
