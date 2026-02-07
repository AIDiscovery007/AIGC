---
name: prompt-forge
description: 参数化图像生成提示词工程。将自然语言描述转化为结构化、可复现的AI图像生成提示词，支持角色创建、场景部署和一致性控制。适用于Midjourney、Stable Diffusion、Flux等模型。
argument-hint: "[create|deploy|list|edit|clone|analyze] [角色名|描述|图片路径]"
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

### 命令: `analyze <角色名> [图片路径] [--detail-level=standard|pixel|exhaustive]`

对参考图片进行像素级分析，提取六大模块参数并生成 Character DNA。

**分析流程**:

1. **图像预处理** - 验证格式、检测人物数量、评估质量
2. **六大模块并行分析** - 按像素级精度提取参数
3. **置信度分级** - A/B/C/D 四级置信度标记
4. **生成 Character DNA** - 组装带置信度标记的 JSON
5. **交互式确认** - 展示分级结果，支持修正低置信度参数

**置信度分级**:

- 🟢 **A级 (0.85-1.0)** - 直接可测：脸型、发色、服装颜色
- 🟡 **B级 (0.70-0.85)** - 比例推算：身高估算、上下身比例
- 🟠 **C级 (0.50-0.70)** - 经验估算：具体围度、品牌色号
- 🔴 **D级 (<0.50)** - 场景推断：光线角度、镜头焦距

**输出示例**:

```
🎭 像素级图片分析

📸 正在分析: photo.jpg
   图片质量: ✅ 优秀 (2048x2732)
   人物检测: ✅ 单人
   清晰度: ✅ 适合像素级分析

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📏 模块1/6: 角色与身体参数
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ [A级] 体型: slender elegant (置信度 85%)
📊 [B级] 身高估算: 168cm (范围 165-170, 置信度 70%)
   └─ 方法: 基于头身比估算（图示约7.5头身）
📊 [B级] 上下身比例: 1:1.55 (置信度 80%)
⚠️  [C级] 肩宽: 38cm (范围 36-40, 置信度 60%)
   └─ 建议: 如需精确值，请提供参考标尺

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
👤 模块2/6: 面部结构参数 (像素级)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ [A级] 脸型: oval with delicate jawline (置信度 90%)
✅ [A级] 眼型: almond with slight upward tilt (置信度 90%)
📊 [B级] 脸长宽比: 1:1.35 (置信度 85%)
📊 [B级] 下颌V角: 120° (置信度 80%)
📊 [B级] 眼长: 3.0cm (范围 2.8-3.2, 置信度 70%)
⚠️  [C级] 鼻梁高度: 1.5cm (置信度 60%)

📊 置信度统计
🟢 A级-直接可测: 8项 (25%)
🟡 B级-比例推算: 14项 (45%)
🟠 C级-经验估算: 7项 (22%)
🔴 D级-场景推断: 3项 (8%)
整体置信度: 72%

💾 是否生成 Character DNA? [Y/n/edit]:
```

**完整 workflow 示例**:

```
# 1. 分析图片生成角色
/prompt-forge analyze model-ref "./reference.jpg" --detail-level=pixel

# 2. 修正低置信度参数
/prompt-forge edit model-ref body.height_cm 170
/prompt-forge edit model-ref face.nose_bridge_height 1.6

# 3. 创建变体
/prompt-forge clone model-ref model-casual
/prompt-forge edit model-casual clothing.style "casual streetwear"

# 4. 部署到场景
/prompt-forge deploy model-ref "咖啡馆窗边，午后阳光，手持咖啡杯"
```

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

---

## 附录: analyze 命令详细规范

### 六大模块像素级分析规范

#### 模块1: 角色与身体参数

```json
{
  "confidence": "B级-比例推算",
  "height_cm": {
    "value": 168,
    "method": "基于头身比估算（图示约7.5头身）",
    "range": "165-170",
    "certainty": 0.7
  },
  "torso_to_leg_ratio": {
    "value": "1:1.55",
    "method": "视觉比例测量",
    "certainty": 0.8
  },
  "shoulder_width_cm": {
    "value": 38,
    "method": "基于头宽比例推算",
    "range": "36-40",
    "certainty": 0.6
  },
  "body_type": {
    "value": "slender elegant",
    "method": "视觉评估",
    "certainty": 0.85
  },
  "shoulder_shape": {
    "value": "straight angular",
    "method": "肩部线条分析",
    "certainty": 0.8
  }
}
```

#### 模块2: 面部结构参数（像素级精度）

```json
{
  "confidence": "A级-直接可测",
  "face_shape": {
    "value": "oval with delicate jawline",
    "certainty": 0.9
  },
  "face_width_height_ratio": {
    "value": "1:1.35",
    "method": "面部轮廓像素测量",
    "certainty": 0.85
  },
  "jaw_v_angle": {
    "value": 120,
    "unit": "degrees",
    "method": "下颌角像素角度测量",
    "certainty": 0.8
  },
  "eye_shape": {
    "value": "almond with slight upward tilt",
    "certainty": 0.9
  },
  "eye_size": {
    "length_cm": {
      "value": 3.0,
      "method": "基于面部比例推算",
      "range": "2.8-3.2",
      "certainty": 0.7
    },
    "width_cm": {
      "value": 1.2,
      "range": "1.0-1.4",
      "certainty": 0.7
    }
  },
  "eye_distance": {
    "value": 3.5,
    "unit": "cm",
    "method": "两眼内眼角间距测量",
    "certainty": 0.75
  },
  "nose_bridge_height": {
    "value": 1.5,
    "unit": "cm",
    "certainty": 0.6
  },
  "nose_wing_width": {
    "value": 2.5,
    "unit": "cm",
    "certainty": 0.65
  },
  "nose_tip_tilt": {
    "value": 10,
    "unit": "degrees",
    "certainty": 0.7
  },
  "lip_width": {
    "value": 4.0,
    "unit": "cm",
    "certainty": 0.75
  },
  "lip_thickness": {
    "upper_cm": {"value": 0.8, "certainty": 0.7},
    "lower_cm": {"value": 1.0, "certainty": 0.7}
  },
  "lip_peak_prominence": {
    "value": 0.5,
    "unit": "mm",
    "certainty": 0.6
  }
}
```

#### 模块3: 肤质与妆容参数

```json
{
  "confidence": "混合分级",
  "skin_tone": {
    "value": "cool porcelain",
    "pantone_estimate": "Cool Gray 1C",
    "confidence": "B级-色彩分析",
    "certainty": 0.75
  },
  "skin_reflectance": {
    "value": 0.9,
    "range": "0.85-0.95",
    "confidence": "C级-经验估算",
    "certainty": 0.6
  },
  "dewy_intensity": {
    "value": 0.7,
    "confidence": "C级-质感评估",
    "certainty": 0.65
  },
  "pore_visibility": {
    "value": "minimal with subtle texture",
    "pore_density_estimate": "50个/cm²",
    "confidence": "C级-细节推断",
    "certainty": 0.5
  },
  "makeup": {
    "eyeliner": {
      "visible": true,
      "style": "winged",
      "extension_mm": {"value": 2, "certainty": 0.6},
      "tilt_angle": {"value": 10, "certainty": 0.65}
    },
    "eyeshadow": {
      "visible": true,
      "color_estimate": "pink pearl",
      "saturation": {"value": 0.6, "certainty": 0.55}
    },
    "lip_color": {
      "visible": true,
      "color_estimate": "pink coral",
      "pantone_estimate": "13-1907 TPG",
      "gloss_level": {"value": 0.9, "certainty": 0.7}
    },
    "blush": {
      "visible": true,
      "placement": "apple of cheeks",
      "saturation": {"value": 0.4, "certainty": 0.6}
    }
  }
}
```

#### 模块4: 姿势与动作参数

```json
{
  "confidence": "B级-角度测量",
  "stance": {
    "value": "standing relaxed",
    "certainty": 0.9
  },
  "head_tilt": {
    "value": 10,
    "unit": "degrees",
    "direction": "down",
    "certainty": 0.8
  },
  "gaze_direction": {
    "value": "down",
    "eyeball_rotation": {"value": 15, "certainty": 0.7}
  },
  "body_tilt": {
    "value": 5,
    "unit": "degrees",
    "certainty": 0.75
  },
  "hand_position": {
    "description": "naturally at sides",
    "certainty": 0.85
  }
}
```

#### 模块5: 光线与氛围参数

```json
{
  "confidence": "D级-场景推断",
  "main_light_direction": {
    "value": "front-left",
    "angle_estimate": {"value": 45, "certainty": 0.6}
  },
  "contrast": {
    "value": 1.0,
    "range": "0.9-1.1",
    "certainty": 0.65
  },
  "saturation": {
    "value": 0.8,
    "certainty": 0.7
  },
  "color_temperature": {
    "value": "warm",
    "certainty": 0.75
  },
  "rim_light": {
    "intensity": {"value": 0.5, "certainty": 0.6},
    "visible": true
  }
}
```

#### 模块6: 场景与景深参数

```json
{
  "confidence": "D级-场景推断",
  "scene_type": {
    "value": "indoor studio",
    "certainty": 0.8
  },
  "background_blur": {
    "value": 0.3,
    "description": "slight blur",
    "certainty": 0.75
  },
  "focal_length_estimate": {
    "value": 85,
    "unit": "mm",
    "range": "50-100",
    "certainty": 0.5
  },
  "depth_of_field": {
    "description": "shallow",
    "certainty": 0.6
  }
}
```

### 完整 Character DNA 输出格式

```json
{
  "id": "analyzed-model",
  "name": "分析生成角色",
  "version": "1.0.0",
  "created_at": "2026-02-06T12:00:00Z",
  "updated_at": "2026-02-06T12:00:00Z",
  "source_image": "path/to/image.jpg",
  "analysis_metadata": {
    "analysis_version": "2.0.0",
    "detail_level": "pixel",
    "overall_confidence": 0.72,
    "confidence_breakdown": {
      "A级-直接可测": 0.25,
      "B级-比例推算": 0.35,
      "C级-经验估算": 0.30,
      "D级-场景推断": 0.10
    }
  },
  "body": { },
  "face": { },
  "skin": { },
  "makeup": { },
  "hair": { },
  "expression": { },
  "clothing": { },
  "default_pose": { },
  "lighting": { },
  "scene": { },
  "rendering": {
    "style": "photorealistic",
    "detail_level": "hyper detailed",
    "anti_anime": "NO anime style, NO cartoon, NO illustration"
  }
}
```

### 像素级测量方法参考

```javascript
// 基于面部关键点的比例计算
function estimateFacialParameters(keypoints) {
  // 以眼距为基准单位 (interpupillary distance)
  const ipd = distance(keypoints.leftEye, keypoints.rightEye);

  return {
    eyeLength: ipd * 0.85,      // 眼长约为眼距的85%
    eyeWidth: ipd * 0.34,       // 眼宽约为眼距的34%
    noseHeight: ipd * 0.43,     // 鼻梁高约为眼距的43%
    lipWidth: ipd * 1.14,       // 唇宽约为眼距的114%
    // ...
  };
}
```

### 置信度算法

```javascript
// 综合多因素计算置信度
function calculateConfidence(factor) {
  const weights = {
    imageClarity: 0.3,           // 图片清晰度
    featureVisibility: 0.25,     // 特征可见度
    measurementPrecision: 0.25,  // 测量精度
    referenceAvailability: 0.2   // 参考数据可用性
  };

  return weightedAverage(factor, weights);
}
```

### 分级颜色编码

- 🟢 **A级 (0.85-1.0)**: 直接可见、清晰可测
- 🟡 **B级 (0.70-0.85)**: 比例推算、相对可靠
- 🟠 **C级 (0.50-0.70)**: 经验估算、存在误差
- 🔴 **D级 (<0.50)**: 场景推断、仅供参考
