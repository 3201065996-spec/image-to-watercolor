# image-to-watercolor

Cursor Agent Skill：把照片或插画转成**日系清新水彩纸上手绘**作品（英文标题、副标题、圆形色号、道具小图标、季节印章、局部特写、颜料偶然感）。

A Cursor [Agent Skill](https://cursor.com/docs/skills) that turns a reference image into a Japanese-style fresh watercolor hand drawing on white watercolor paper — with English title/subtitle, circular hex swatches, prop icon, season stamp, detail inset, and pigment accident marks.

## Features

- 原生水彩纸感（颜料渗入纸纹，边缘晕开，不是「贴图在白底上」）
- 固定版式：上方主画约 60–65%，底部留白放标题 / 副标题 / 四色色号
- 创意细节：道具线稿图标、角落淡彩印章、铅笔框局部特写、轻微水渍
- 输出比例跟随上传图（`1:1` / `4:3` / `3:4` / `16:9` / `9:16`）

## Requirements

- [Cursor](https://cursor.com)（Agent 模式）
- 可用的 **GenerateImage** 能力（本 skill 通过该工具出图）

> 在没有图像生成工具的环境里，需要自行改成对应画图 API；提示词与版式规则仍可复用。

## Install

### 方式 A：用户级（所有项目可用）

把本仓库克隆或下载后，复制整个文件夹到：

```text
~/.cursor/skills/image-to-watercolor/
```

Windows 示例：

```text
%USERPROFILE%\.cursor\skills\image-to-watercolor\
```

文件夹内必须直接包含 `SKILL.md`。

### 方式 B：项目级（仅当前仓库）

复制到：

```text
.cursor/skills/image-to-watercolor/SKILL.md
```

或：

```text
.agents/skills/image-to-watercolor/SKILL.md
```

安装后可在 Cursor → **Customize → Skills** 里确认是否已发现该 skill。

## Usage

1. 在 Agent 聊天中附上图片（或给出图片路径）
2. 说例如：
   - `转成手绘图`
   - `图片转水彩`
   - `photo to watercolor`
   - 或手动调用 `/image-to-watercolor`
3. Agent 会按 `SKILL.md` 起草标题/色号等，再生成成品，并回报文案与比例

### 可选覆盖

你可以指定或关掉部分元素，例如：

- 自定义标题 / 副标题 / 四个 hex
- 不要印章、不要局部特写、不要颜料偶然感
- 指定裁切焦点或强制某种 `aspect_ratio`

## Repository layout

```text
image-to-watercolor/
├── SKILL.md      # Agent 指令（核心）
├── README.md     # 给人看的说明
├── LICENSE       # MIT
├── assets/       # 可选：前后对比示例图
└── .gitignore
```

## Assets（可选）

在 `assets/` 放入前后对比图（原图 + 水彩成品），并在 README 中引用，方便访客预览效果。当前仓库可先不带示例图。

## License

[MIT](./LICENSE) © 2026 郑雅萍
