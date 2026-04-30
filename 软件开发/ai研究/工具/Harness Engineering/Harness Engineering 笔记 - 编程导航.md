## 💡 引言

用 AI 编程时，你可能会碰到这些问题：

- 让 AI 改样式，结果它重新开发了整个布局
- AI 忘了一开始的约束，把代码写得很长
- 修 Bug 反而出了更多新 Bug

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LlSQOKIxJ1FBibcCZvL958yC0ZIvC7GlhTf3v73LDLm7unnrFicIT2xicD5YVIm3IToT1c5vkIiacQ8JZFp4W1Zps5gic8j545SWEwHSd5j8RSWY/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

前两个问题可以通过写好提示词、给够信息解决，第三个问题更棘手。要让 AI 做好完整项目，得给它搭一整套靠谱的工作环境和流程。

这就是 **Harness Engineering**！

---

## 一、什么是 Harness Engineering？

### 🐴 定义

Harness 翻译过来是「马具」，把 AI 模型比作马，Harness 就是驾驭它的一切：缰绳、路线规划、围栏等。我们要让这匹马跑得更快、更稳。

具体来说，Harness 是围绕 AI 模型搭建的**工作环境和工作流程**，包括：项目规则文件、配置的工具、任务拆分和执行顺序、测试检查流程等。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LlSQOKIxJ1EmCJv7g3o4xWK6cAgZClVo1vuAxocEiaq9oAJUI2CiavwMCVmRDxbYAZVp3rz1APHoE30UZmibjJTCicVn5gzDgiclSb7MiaWiabicVpw/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=1)

### 🔥 背景

两个案例让这个概念火了：

1. **LangChain 实验**：同一 AI 模型，只优化 Harness，编码基准测试排名从 30 名开外到前 5
2. **OpenAI 团队**：3 人团队靠 Harness 引导 AI 生成上百万行代码，产品内部上线

**行业共识**：

> AI 编程的瓶颈不在模型有多聪明，而在围绕模型搭的环境和流程够不够好

### 📈 发展历程

Harness 不是 2026 年的新东西，从 2022 年 ChatGPT 出来时大家就已经在做了，只是当时没叫这个名字。三者是层层包含的关系：

1. **提示词工程（2022-2024）**
   - 核心：通过对话让 AI 听懂需求
   - 方法：设定角色、约束格式、思维链、给示例
   - 效果：提升 AI 输出质量

2. **上下文工程（2025）**
   - 核心：在对的时候把对的信息喂给 AI
   - 方法：AGENTS.md、RAG、上下文压缩、跨对话记忆

3. **Harness Engineering（2026）**
   - 核心：让 AI 持续靠谱地完成整个任务
   - 关注点：工具配置、任务拆分、自检修复、质量防护

![图片](https://mmbiz.qpic.cn/mmbiz_png/LlSQOKIxJ1HfsPrfbdibRTwmPloPP2bUIibTa8XANM8w0ticrOZ01JLjYSX9ibnd5lZDiccA4vWkY8ZYYXwA1hadWXEcncaHFfPAaJdLfK8FJ22A/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=5)

**业界公式**：

> Agent = 模型 + Harness

围绕 AI 模型搭建的工具、规则、流程、检查机制都属于 Harness。

![图片](https://mmbiz.qpic.cn/mmbiz_png/LlSQOKIxJ1EHibhaShO5UPdOP2ccOicg0tdTm9bbK5ehZz4sLLeDBXoWcPkEObX6Baqhcfg2BfKkYUhSZqDDPwTnibEmCTMsGZzm5HhvbAxOTk/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=7)

---

## 二、五个核心模块

Harness 解决 AI 干活时的核心问题，这些方法对有项目经验的人来说并不陌生。

### 1️⃣ 上下文架构

> 关键词：AGENTS.md、分层文档、上下文压缩、渐进式加载

做项目第一步是了解需求、背景和规范，用 AI 做项目也一样，需要把这些信息喂给它。

我们可以写 **AGENTS.md** 规则文件，告诉 AI 技术栈、代码规范、禁止事项。

AI 能处理的上下文空间有限！OpenAI 团队踩过坑：把几千行规则塞进一个文件，AI 反而会忽略关键信息。

后来他们改成把 **AGENTS.md 当成一个「目录」来用**，只写大概 100 行的摘要和索引，然后在 `docs/` 目录下放详细的设计文档。AGENTS.md 里面写清楚「前端规范看 `docs/FRONTEND.md`、安全相关看 `docs/SECURITY.md`」这样的指引，AI 需要什么就去读对应的文件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/LlSQOKIxJ1Ep9P0zZzryyjhhfWvX1IxVnkz6kltjHaHOo3mFdKCFVLTeWMyQrpXuQ0HNXmQrxNZagNHpjZ1S1w9ibayopib5GHpnkuXmYB9Gk/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=8)

这种**按需加载**的思路，就是上下文架构的核心！

### 2️⃣ 执行能力

> 关键词：工具调用、Bash 终端、文件系统、MCP、Browser Use、Skills

AI 模型本身只能输出文本。要让它帮你开发项目，得通过工具调用让它具备操作电脑的能力：

- 配终端环境执行命令
- 给文件系统读写代码
- 给浏览器测试网页

通过 **MCP** 可进一步扩展操作范围，比如读写数据库、联网搜索等。

还有 **Agent Skills**，把复杂工作流封装成技能包，让 AI 学会各种专业技能，如自动生成 PPT、处理 Excel。

总之，**让 AI 能用的工具越多，它能帮你干的活就越多！**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LlSQOKIxJ1EJZTQR1eB6eHPba1ZDEm0fq4MwScyCrE1ztvpKVzFNUmRibficEPxBeWvVx6yLWrUFF5C1tqDInYIiaJiaor9mAodv9e6AHeLObDc/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=9)

### 3️⃣ 任务编排

> 关键词：Plan Mode、任务拆分、增量开发、文档沉淀、SubAgents 并行执行

丢给 AI 一个大需求，它可能会一把梭全部搞定。但 AI 上下文空间有限，开发到一半可能装不下信息，方案和约束慢慢被冲淡，留下跑不起来的代码。

解决办法是把**大任务拆成小任务**，每次只做一个功能点。开始前用 **Plan Mode（计划模式）** 让 AI 出方案，人工确认后再写代码。

每做完一个功能，最好都**沉淀一下文档**，记录当前实现的功能、技术方案、待办事项。这样新开对话窗口，AI 读文档就能快速了解之前做了什么。

如果有多个互不依赖的小任务，可用 **SubAgents** 让它们并行执行，效率更高。

![图片](https://mmbiz.qpic.cn/mmbiz_png/LlSQOKIxJ1FlkDPL8pAt7Os80LWvry7I62cf5CWlPFPEUYnCqmY3bGg2IYnr3j392iaMshFTs9uRQlkYe9NHXao1vuAf4hs8tibibQ7f1xFTIs/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=10)

### 4️⃣ 反馈机制

> 关键词：Linter、自动化测试、Browser Use、Agent 互审

AI 写完代码可能自信满满，但运行起来全是 Bug！

所以得让 AI 写完代码后能**自己检查自己的工作**：

- 跑 Linter 查语法和规范问题
- 跑自动化测试验证功能
- 让 AI 自己打开浏览器操作，功能正常才算完成

如果测试没通过，AI 可以自动读取报错信息，分析原因并修复。也可以人工检查，把问题、报错、截图给 AI。

还可以让另一个 AI 来审查代码，搞「**多 Agent 互审**」机制。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/LlSQOKIxJ1EFGtM17aPvYnrzeG9t9O8CJ9Mib1DxSDbfeLdF3979JHhJh87O9ITSweeiaKRCFzWhAJR7icKDKI5BH2ictibD6o2RjKAWxJICqpiag/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=11)

### 5️⃣ 架构护栏

> 关键词：架构约束 Linter、Pre-commit Hooks、垃圾回收机制、Git 检查点

AI 生成代码会**模仿仓库里已有的代码风格，哪怕是烂代码**。比如同样的页面代码写好几遍，不知道拆分成可复用组件，导致改一处漏改重复的地方，时间长了技术债越滚越大。

常见做法是用专门的 Linter 来**强制执行架构层面的约束**（和之前的 Linter 不同，它查架构规则，比如 UI 层不能直接调用数据库层、模块依赖必须单向。AI 违反会被自动拦住，Pre-commit Hooks 在提交时拦截不合规代码。

OpenAI 还有「**垃圾回收**」机制，定期让 AI 扫描代码库，检查偏离架构规范，自动提交修复 PR，持续偿还技术债。

另外建议**每完成一个功能就用 Git 提交一次代码**。Git 是版本控制工具，记录代码历史版本，相当于存档点，改出问题可以恢复。

![图片](https://mmbiz.qpic.cn/mmbiz_png/LlSQOKIxJ1HTUiapfUhojFrQm3lJpoyAvjiczhF3XDXicnEAt3LddgyBDt2lYKpIZ3giaHOfD5Lg4NHpGjQl7nic7cTJKHDQ1C8XK9yxrG1VW7hs/640?wx_fmt=png\&from=appmsg\&tp=webp\&wxfrom=5\&wx_lazy=1#imgIndex=12)

---

## 三、Harness 项目实战

用实际项目看看，Harness 在真实开发中是怎么落地的。

这个项目是[「**万能视频下载总结器**」](https://www.codefather.cn/course/2027618983506640897)：用 AI 从零开发一个视频下载和总结网站，含 SEO/GEO 优化和 Stripe 支付。

### 1️⃣ 方案设计阶段

动手前先自己想清楚核心方案，用 AI 调研后决定用 yt-dlp 做下载、Python 为主技术栈。

把思考写成文档给 AI，开启 Plan Mode 让它先出方案再确认。发现它计划了后续功能，就让它先完成核心下载功能，一步步来。

这就是**任务编排**和**上下文架构**的应用：先规划再执行，给 AI 充足背景信息，约束它不要一把梭！

### 2️⃣ 编码开发阶段

确认方案后 AI 开发，做了几件关键事：

- **装联网能力**：配置 Firecrawl MCP 抓网页、Context7 MCP 查最新文档，避免过时写法
- **沉淀文档**：核心功能完成后写总结文档，记录功能、架构和实现细节，提交 Git
- **新开对话**：新功能用干净对话 + 文档找回记忆，避免上下文污染导致表现下降

这些是**上下文架构**和**执行能力**的建设：给 AI 装工具、维护好上下文！

### 3️⃣ 测试验证阶段

AI 能通过 Cursor 的 Browser Use 自己启动浏览器测试。

遇到问题时：
- B 站 403 错误 → AI 自己发现是防盗链并修复
- Markdown 渲染问题 → 人工换角度提示（查后端 SSE），AI 恍然大悟改好
- 小技巧：用模拟数据直接测试，不用走完整流程

这是**反馈机制**：AI 自我修复，搞不定时人工介入，Harness 把精力用在关键点！

### 4️⃣ 功能扩展阶段

核心功能跑通后加了 3 个需求：Markdown 排版、思维导图全屏下载、字幕下载。

- 独立需求用 SubAgents 并行开发
- 每完成一个功能就提交代码更新文档当检查点
- SEO 优化用 SEO Audit 技能，GEO 优化复用对话上下文省时间

这些操作涵盖了**任务编排（并行开发）、架构护栏（Git 检查点）和执行能力（Skills 扩展）几个方面，都是 Harness 的重要实践！**

---

## 四、快速上手 Harness

Harness 不复杂，上面项目里的操作就是你现在能用的技巧！

### 🚀 实用方法

按项目流程总结的实用方法：

1. **写 AGENTS.md 规则文件**，告诉 AI 项目背景、技术栈、代码规范
2. **AI 出方案先确认，再写代码**
3. **用 MCP 和 Skills 给 AI 配工具**，让它能联网查最新资料
4. **做完功能让 AI 自己跑测试**
5. **每完成一个功能沉淀文档并提交代码**当存档点

### 🛠️ 工具推荐

缺经验或嫌麻烦可用现成工具：

- **Spec Kit**：SDD 规范驱动开发，先拆需求成规范文档，AI 按文档一步步开发，每个阶段有明确验收标准
- **Superpowers**：Agent Skills 框架，内置强制 TDD、两阶段代码审查、子代理协作等，相当于给 AI 装完整项目管理流程

虽然这些工具可以帮你快速起步，但从长远来看，**理解 Harness 的思路比掌握某个工具更重要**！毕竟工具一直在变化，但「怎么系统地驾驭 AI」这个思路是通用的。想要真正掌握 Harness，最好的办法还是在实战项目中去体会！

---

## 五、总结

**Harness 不是新技术，本质是把工程经验系统地应用到 AI 上！**

- **以前**：工程师核心是写代码
- **现在**：AI 帮写代码，我们花更多精力在需求分析、方案设计、任务拆解、质量把关

**用好 AI，取决于你的工程能力！**

所以，建议大家平时多做完整的项目，从零到一走完全流程，这个过程中积累的工程经验，就是你驾驭 AI 最好的 Harness！

---

参考链接：

- [原文链接](https://mp.weixin.qq.com/s/qdTXCvMA4yI9mTuQv8Zq6A)：鹅厂面试官：“你用过 Harness Engineering 吗？” 我冷笑：“这不是 22 年的技术么？” 他激动了：明天入职！
