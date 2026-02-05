# 示例库

## 示例1: 东亚女偶像 (eastern-idol)

### Character DNA
```json
{
  "id": "eastern-idol-001",
  "name": "东亚女偶像",
  "version": "1.0",
  "created_at": "2024-01-15",
  "body": {
    "height_cm": 180,
    "weight_kg": 60,
    "body_type": "slender",
    "proportion_upper_lower": "1:1.5",
    "shoulder_width_cm": 38,
    "bust_waist_hip_cm": [90, 62, 92],
    "leg_length_cm": 110,
    "thigh_circumference_cm": 50,
    "calf_circumference_cm": 32,
    "neck_length_cm": 15,
    "arm_circumference_cm": 25,
    "foot_length_cm": 25,
    "ankle_circumference_cm": 20
  },
  "face": {
    "face_shape": "oval",
    "face_ratio": "1.4:1",
    "jaw_v_angle": 120,
    "cheekbone_height_cm": 1.0,
    "chin_sharpness_angle": 30,
    "face_symmetry_percent": 99,
    "eye_shape": "almond",
    "eye_size_cm": [3.0, 1.2],
    "eye_distance_cm": 3.5,
    "eye_fold_width_mm": 2,
    "pupil_diameter_mm": 4,
    "iris_color": "deep brown gradient",
    "nose_bridge_height_cm": 1.5,
    "nose_wing_width_cm": 2.5,
    "nose_tip_tilt_angle": 10,
    "lip_width_cm": 4,
    "lip_thickness_cm": [0.8, 1.0],
    "lip_peak_prominence_mm": 0.5,
    "ear_height_cm": 6,
    "forehead_width_cm": 12,
    "forehead_height_cm": 6
  },
  "skin": {
    "skin_tone": "cool porcelain",
    "pantone_ref": "Cool Gray 1C",
    "foundation_brand": "YSL BD10 Porcelain",
    "reflectance": 0.9,
    "dewy_intensity": 0.7,
    "skin_texture": "natural",
    "pore_density_per_cm2": 50
  },
  "makeup": {
    "brow": {
      "color": "light brown gray",
      "pantone": "7536C",
      "arc_angle": 15,
      "tail_drop_angle": 5,
      "density_per_cm": 30,
      "length_cm": 5
    },
    "eyeshadow": {
      "color": "light pink pearl",
      "brand": "Dior Pink Corolla 001",
      "coverage_cm2": 4,
      "saturation": 0.6
    },
    "eyeliner": {
      "width_mm": 0.1,
      "extension_mm": 2,
      "tilt_angle": 10,
      "brand": "Chanel Noir Intense"
    },
    "eyelashes": {
      "length_mm": 10,
      "curl_angle": 55,
      "style": "natural"
    },
    "blush": {
      "color": "pink orange",
      "diameter_cm": 3,
      "saturation": 0.4
    },
    "lip": {
      "color": "mirror light pink",
      "pantone": "13-1907 TPG",
      "brand": "MAC Russian Red",
      "saturation": 0.5,
      "reflectance": 0.9,
      "has_glitter": true
    },
    "highlight": {
      "areas": ["nose bridge", "nose tip", "brow bone", "cheekbones", "above lip"],
      "intensity": 0.7
    }
  },
  "hair": {
    "color": "black",
    "length_cm": 60,
    "style": "high ponytail",
    "texture": "straight",
    "parting_ratio": "3:7",
    "strand_diameter_mm": 0.08,
    "reflectance": 0.6,
    "accessories": ["nezuko Q-version hairpin with playforge logo"]
  },
  "clothing": {
    "top": "white shirt",
    "outerwear": "navy school blazer",
    "bottom": "plaid pleated skirt",
    "shoes": "black loafers",
    "accessories": ["white fluffy scarf with playforge label", "black knee-high socks"],
    "fabric_texture": "wool-like",
    "fabric_reflectance": 0.4
  },
  "expression": {
    "gaze_direction": "down",
    "eyelid_droop_angle": 30,
    "eyeball_rotation_angle": 15,
    "mouth_state": "slightly-open",
    "mouth_opening_mm": 0.2,
    "head_tilt_angle": 10,
    "neck_forward_angle": 5,
    "overall_mood": "elegant focus with slight detachment"
  },
  "default_pose": {
    "stance": "standing-leaning",
    "body_tilt_angle": 10,
    "body_tilt_direction": "door",
    "hand_position": "holding phone at chest level",
    "holding_object": "phone",
    "feet_distance_cm": 30
  }
}
```

### 部署场景: 地铁车厢

**场景描述**: "地铁车厢黄昏，靠着车门看手机"

**合成提示词 - Midjourney格式**:
```
Extremely detailed East Asian female idol, exact face-structure [oval face 1.4:1 ratio, jaw V-angle 120°, almond eyes 3.0x1.2cm, eye-distance 3.5cm, nose-bridge 1.5cm, lip-width 4cm], YSL-BD10 porcelain skin reflectance-0.9 dewy-0.7, navy school uniform with plaid skirt, standing in metro car interior ceiling-200cm, leaning 10deg against door holding phone at 120cm height, soft warm interior lighting saturation-0.8 contrast-1.0, 35mm lens, shallow depth of field focus-on-face, --ar 9:21 --stylize 0 --cref [anchor-image-url]
```

**合成提示词 - SD/ComfyUI格式**:
```
masterpiece, best quality, 1girl, eastern-idol-001 face-structure,
(oval face 1.4:1:1.3), (jaw V-angle 120:1.2), (almond eyes:1.2),
(YSL BD10 porcelain skin:1.3), (reflectance 0.9:1.1), (dewy 0.7:1.1),
navy school uniform, plaid pleated skirt, white fluffy scarf,
standing, leaning against door, holding phone,
metro interior, soft warm lighting, 35mm lens, shallow depth of field,
--ar 9:21
```

**关键指令块**:
```
[CHARACTER LOCK]
PRESERVE: exact facial-structure from DNA [oval face 1.4:1, jaw 120°, almond eyes 3.0x1.2cm]
PRESERVE: skin-material YSL-BD10 reflectance-0.9 dewy-0.7
PRESERVE: makeup-matrix [brow Pantone-7536C, eyeshadow Dior-001, lip MAC-Russian-Red]
do NOT alter: eye-shape, nose-bridge, jaw-angle, skin-tone
ADAPT ONLY: pose, clothing-lighting-interaction, environmental-reflections
[/CHARACTER LOCK]
```

---

## 示例2: 极简快速创建模板

当不需要完整参数时，使用精简模板:

```json
{
  "id": "quick-character",
  "name": "快速角色",
  "body": {
    "height_cm": 170,
    "body_type": "匀称",
    "proportion_upper_lower": "1:1.3"
  },
  "face": {
    "face_shape": "鹅蛋脸",
    "face_ratio": "1.35:1",
    "eye_shape": "杏眼"
  },
  "skin": {
    "skin_tone": "自然肤色",
    "reflectance": 0.8
  },
  "clothing": {
    "style": "casual modern"
  }
}
```

对应提示词:
```
East Asian female, 170cm, balanced body proportion 1:1.3,
oval face 1.35:1, almond eyes, natural skin reflectance-0.8,
casual modern clothing, standing pose, soft lighting
```

---

## 示例3: 多场景部署对比

同一角色在不同场景下的参数调整:

### 场景A: 咖啡馆日间
```
...character DNA...
scene: cafe interior, natural window light from left,
seated at table, holding coffee cup,
bright atmosphere, saturation-0.7, contrast-0.9
```

### 场景B: 夜景街头
```
...character DNA...
scene: city street at night, neon lights background,
walking, holding bag,
rim-light intensity-0.6, contrast-1.2, saturation-0.9
```

### 场景C: 海边日落
```
...character DNA...
scene: beach sunset, golden hour lighting,
standing facing ocean, wind in hair,
warm color-grading, saturation-0.85, backlight-0.7
```

---

## 示例4: 角色克隆与变体

### 原角色: eastern-idol
### 克隆: eastern-idol-casual (休闲版)

**修改参数**:
- `clothing.outerwear`: "navy school blazer" → "oversized denim jacket"
- `clothing.bottom`: "plaid pleated skirt" → "distressed jeans"
- `hair.style`: "high ponytail" → "loose waves"
- `makeup.lip.saturation`: 0.5 → 0.3

### 克隆: eastern-idol-formal (正式版)

**修改参数**:
- `clothing.outerwear`: "navy school blazer" → "tailored black suit"
- `clothing.bottom`: "plaid pleated skirt" → "pencil skirt"
- `hair.style`: "high ponytail" → "sleek bun"
- `makeup.eyeshadow.saturation`: 0.6 → 0.4
- `expression.overall_mood`: "elegant focus" → "confident professional"

---

## 提示词合成公式

### 标准合成顺序
```
[角色DNA摘要] + [姿势动作] + [场景描述] + [光线氛围] + [镜头参数] + [模型特定后缀]
```

### DNA摘要压缩格式
```
face[脸型:比例:下颌角]+eye[眼型:尺寸:眼距]+nose[鼻梁:鼻翼:鼻尖]+lip[宽度:厚度]+skin[色调:反射率:水光]
```

示例:
```
face[oval:1.4:120]+eye[almond:3.0x1.2:3.5]+nose[1.5:2.5:10]+lip[4:0.8/1.0]+skin[cool:0.9:0.7]
```
