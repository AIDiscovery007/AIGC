---
name: prompt-forge
description: 参数化图像生成提示词工程。将自然语言描述转化为结构化、可复现的AI图像生成提示词，支持角色创建、场景部署和一致性控制。适用于Midjourney、Stable Diffusion、Flux等模型。
argument-hint: "[create|deploy|list|edit|clone] [角色名|描述]"
disable-model-invocation: false
user-invocable: true
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Prompt Forge - 参数化图像生成提示词工程

## 核心能力

将模糊的自然语言描述转化为可量化、可复现、可版本化的结构化提示词。

## 六大参数模块

1. **角色与身体参数** - 身高、比例、围度等体态基准
2. **面部结构参数** - 脸型、五官几何尺度
3. **肤质与妆容参数** - 色彩体系、光学属性、纹理细节
4. **姿势与动作参数** - 角度、方向、距离的姿态刻画
5. **光线与氛围参数** - 对比度、饱和度、颗粒感等风格控制
6. **场景与景深参数** - 环境几何与镜头语言

## 命令处理逻辑

当用户调用命令时，按以下逻辑处理：

### 命令: `create <角色名>`

启动交互式角色创建流程：

1. **检查角色是否已存在** - 如果存在，提示用户是否覆盖
2. **引导用户输入六大模块参数** - 每个模块提供默认值，用户可直接回车接受或输入新值
3. **生成 Character DNA JSON**
4. **保存到 `data/<角色名>.json`**
5. **输出生成的压缩指代句**

**交互流程示例**:
```
🎭 创建角色: eastern-idol

📏 模块1: 角色与身体参数
身高 (cm) [170]: 180
体型 [slender]:
上身:下身比例 [1:1.3]: 1:1.5
肩宽 (cm) [38]:
胸/腰/臀围 (cm) [90/62/92]:
腿长 (cm) [100]: 110
...

✅ 角色已保存到: data/eastern-idol.json
📋 压缩指代句: face[oval:1.4:120]+eye[almond:3.0x1.2:3.5]+skin[cool:0.9:0.7]
```

### 命令: `deploy <角色名> "场景描述"`

1. **读取 Character DNA** 从 `data/<角色名>.json`
2. **解析场景描述** - 提取关键参数（地点、时间、动作、光线等）
3. **合成完整提示词** - 按规则组合 Character Block + Scene Block
4. **输出多格式版本**:
   - Midjourney 格式
   - SD/ComfyUI 格式
   - Flux 格式
   - 关键指令块（Character Lock）

### 命令: `list`

扫描 `data/` 目录，列出所有 `.json` 文件，显示：
- 角色名
- 创建时间
- 版本
- 简要描述

### 命令: `edit <角色名> <参数路径> <新值>`

1. **读取现有 Character DNA**
2. **按路径更新参数** (如 `body.height_cm` 或 `makeup.lip.saturation`)
3. **更新 `updated_at` 时间戳**
4. **保存文件**
5. **输出变更摘要**

### 命令: `clone <原角色> <新角色>`

1. **读取原角色 DNA**
2. **修改 id 和 name**
3. **重置创建时间**
4. **保存为新文件**
5. **提示用户可编辑的参数**

## Character DNA Schema

```json
{
  "id": "角色标识符",
  "name": "角色名称",
  "version": "版本",
  "created_at": "创建时间",
  "updated_at": "更新时间",
  "body": { "身高、比例、围度参数" },
  "face": { "脸型、五官几何参数" },
  "skin": { "肤色、肤质光学参数" },
  "makeup": { "妆容范围与强度参数" },
  "hair": { "发色、长度、造型参数" },
  "clothing": { "服装细节参数" },
  "expression": { "表情参数" },
  "default_pose": { "默认姿势参数" }
}
```

## 提示词合成规则

1. **块顺序**: Character DNA → Pose → Scene → Lighting → Camera
2. **指代强化**: 使用 `[CHARACTER::ID="xxx"]` 语法创建锚点
3. **差异抹除**: 明确列出 "NO alteration to..." 防止漂移
4. **权重标记**: 关键特征添加 `:1.2` 等权重（SD语法）

## 输出格式

- **Midjourney**: 自然语言描述 + 参数后缀
- **SD/ComfyUI**: 标签式描述 + 权重标记
- **Flux**: 结构化自然语言

## 参考文档

- 详细模板: `reference/module-templates.md`
- 示例库: `reference/examples.md`
- Schema定义: `reference/character-schema.json`

---

## 当前命令执行

用户输入: `{{ARGUMENTS}}`

请根据上述命令处理逻辑，执行相应的操作。
