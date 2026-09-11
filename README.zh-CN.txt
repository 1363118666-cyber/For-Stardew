AliveNPCs Economy NPC Builder —— 使用说明
=========================================

【运行】
1. 把整个文件夹解压到任意位置（AliveNpcsBuilder.exe 和 config.json 必须放在一起）。
2. 双击 AliveNpcsBuilder.exe。
3. 首次运行会自动寻找星露谷目录；找不到时会让你手动选择。

【配置 AI（可选，但用 AI 生成/编辑需要）】
4. 用记事本打开同目录的 config.json，把你的 API Key 填到 "api_key" 里；
   或者不改文件、改用环境变量 OPENCODEGO_API_KEY。
   （发布包里不含任何 Key。）

【用其它 AI 服务/模型（可选）】
- AI 功能走标准 OpenAI「chat completions」接口，任何兼容服务或本地模型都能用。
  在 config.json 的 "ai" 里改：
    * OpenAI：      api_base "https://api.openai.com/v1"，   model "gpt-4o-mini"
    * DeepSeek：    api_base "https://api.deepseek.com/v1"， model "deepseek-chat"
    * OpenRouter：  api_base "https://openrouter.ai/api/v1"，model "<厂商>/<模型>"
    * Groq：        api_base "https://api.groq.com/openai/v1"，model "llama-3.3-70b-versatile"
    * Ollama 本地： api_base "http://localhost:11434/v1"，   model "llama3.1"，
                    api_key 填任意非空值（如 "ollama"）
  把该服务的 Key 填到 "api_key"（或用 "api_key_env" 指定的环境变量）。
- 若模型报错，试着把 "max_tokens" 调小（如 4096），或把 "token_param" 设为
  "max_completion_tokens"（部分新模型需要）。
- 把 "temperature" 设为 null 可省略该参数（有些模型只接受默认值）。
- "provider" 可保持 "opencodego" 或写任意名字；只有 "mock" 特殊（离线演示，无需 Key/联网）。

【使用】
5. 左侧选择 NPC 进行编辑；点“新建 (AI)”，用中文描述角色（卖什么、收什么、性格）。
6. 出售/收购物品支持中文输入，工具会列出候选让你点选，绝不瞎猜。
7. 改完点“应用修改 (保存)”。工具会：校验 → 显示改动 → 自动备份 → 写入。
8. 改错了可点“回滚最近备份”。

【目录里没有的物品】
- 可直接填星露谷物品 ID，如 (O)475、(W)11、(F)1234，工具会**原样写入**，无需查目录。
- 也可直接填精确的物品名；若不在内置列表里，工具会提供「按原样使用」并原样写入（附警告）。
  游戏/模组会按名字解析（英文或你的游戏语言都行）。
- 想严格检查？在 config.json 里把 "allow_unverified_items" 设为 false。

【界面语言】
- 在 config.json 里把 "ui_language" 设成语言代码（如 en/zh/ja/es/pt/de/fr/ru/ko/it/tr），
  或写语言名（如 English/中文）；默认 "auto" 跟随系统。
- 程序只内置英文和中文界面。想加其它语言：在 exe 旁放一个 lang/<代码>.json
  （复制 lang/en.json，把值翻译一下），程序会自动加载，**无需重新打包**；
  缺的键自动回退英文。欢迎社区提 PR 贡献翻译。

【已知限制】
- 带口味的手工品（草莓酒、芒果果酱、葡萄汁……）在星露谷里**不是独立物品**：
  游戏在运行时用"基础物品（果酒/果酱/果汁/腌菜/果干）+ 口味（水果/蔬菜）"拼出来，
  **游戏数据里没有各自的物品 ID**。
  因此本工具只能提供**基础物品**（如"果酒"），模组本身也不处理口味。
  若想让 NPC 交易特定口味，需要**模组作者**在模组里支持，请向作者反馈。

【物品名（任意语言，无需翻译）】
- 点“本地化物品名”（或运行 `localize-items`）一次即可：它会从**你自己的游戏文件**
  读取本语言的物品名（Content/Strings/Objects.<语言>.xnb），本地缓存。
  之后物品选择器/解析就能识别你的语言。
- 同时会索引**非 Objects 物品**（武器、服装、饰品等），可按名字搜索，工具会为你写入正确的物品 ID。
- `item_language` 控制物品名语言（默认 `auto` = 跟随 `ui_language`）；想"英文界面 + 中文物品名"就设成 `zh`。

【安全】
- 所有写入都会先校验、预览、备份；原文件不会被悄悄改动。
- 本工具是玩家自制，与 Stardew Valley / AliveNpcs Economy 官方无关。
- 详见 NOTICE.txt（含第三方组件许可与署名）。
