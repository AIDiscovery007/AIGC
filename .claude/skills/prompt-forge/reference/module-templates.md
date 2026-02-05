# 六大模块详细模板

## 模块1: 角色与身体参数

### 模板结构
```json
[身体参数模块]
- 身高：___ cm
- 体重：___ kg（可选）
- 体型：偏瘦 / 匀称 / 偏健美
- 胸腰臀围：___ / ___ / ___ cm
- 肩宽：___ cm（窄肩 / 标准 / 宽肩）
- 上身:下身比例：___ : ___
- 腿长：___ cm，大腿围 ___ cm，小腿围 ___ cm
- 手臂围：___ cm，线条：柔和 / 略具肌肉感
- 颈长：___ cm
- 脚长：___ cm，脚踝围：___ cm
```

### 示例值
```json
{
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
}
```

---

## 模块2: 面部结构参数

### 模板结构
```json
[面部结构模块]
- 脸型：鹅蛋脸 / 圆脸 / 方脸 / 心形脸
- 脸长宽比：___ : 1（>1 表示偏修长）
- 下颌线 V 角：约 ___ °
- 颧骨突出高度：约 ___ cm
- 下巴尖度：约 ___ °
- 脸部对称度：约 ___ %

[眼部参数]
- 眼型：杏仁眼 / 圆眼 / 狐狸眼
- 眼长：___ cm，眼宽：___ cm
- 眼距：___ cm
- 眼皮褶宽度：___ mm
- 瞳孔直径：___ mm
- 虹膜颜色：___

[鼻部参数]
- 鼻梁高度：___ cm（低 / 中 / 高）
- 鼻翼宽度：___ cm
- 鼻尖上翘角度：___ °

[唇部参数]
- 唇宽：___ cm
- 上/下唇厚度：___ / ___ cm
- 唇珠突出度：___ mm

[其他]
- 耳廓高度：___ cm
- 额头宽度：___ cm，高度：___ cm
```

### 示例值
```json
{
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
  "iris_color": "深棕色渐变",
  "nose_bridge_height_cm": 1.5,
  "nose_wing_width_cm": 2.5,
  "nose_tip_tilt_angle": 10,
  "lip_width_cm": 4,
  "lip_thickness_cm": [0.8, 1.0],
  "lip_peak_prominence_mm": 0.5,
  "ear_height_cm": 6,
  "forehead_width_cm": 12,
  "forehead_height_cm": 6
}
```

---

## 模块3: 肤质与妆容参数

### 肤质模板
```json
[肤质模块]
- 肤色类型：冷白皮 / 暖白皮 / 自然肤色 / 健康肤色
- Pantone参考：___
- 粉底品牌色号：___
- 皮肤反射率：___（0-1）
- 水光效果强度：___（0-1）
- 磨皮程度：低 / 中 / 高
- 保留毛孔纹理：是 / 否
- 毛孔密度：___ 个/cm²
```

### 妆容模板
```json
[高光模块]
- 重点区域：鼻梁 / 颧骨 / 额头 / 下巴 / 唇珠
- 鼻梁高光长度：___ cm
- 鼻尖高光直径：___ cm
- 颧骨高光面积：___ cm²
- 高光强度：___（0-1）

[眉眼妆模块]
- 眉色：___（Pantone ___）
- 眉峰弧度：___ °
- 眉尾下垂/上扬角度：___ °
- 眉毛密度：___ 根/cm
- 眉长：___ cm

- 眼影主色：___
- 眼影品牌色号：___
- 覆盖范围：___ cm²
- 晕染延伸：不超过眼尾 ___ cm
- 眼影饱和度：___（0-1）

- 眼线线宽：___ mm
- 眼尾延长：___ mm
- 上扬角度：___ °
- 眼线品牌色号：___

- 卧蚕长度：___ cm
- 卧蚕立体感：___（0-1）

- 睫毛长度：___ mm
- 卷翘角度：___ °

[腮红与唇妆模块]
- 腮红色相：___
- 范围直径：___ cm
- 腮红饱和度：___（0-1）

- 唇色：___（Pantone ___）
- 唇妆品牌色号：___
- 饱和度：___（0-1）
- 光泽反射率：___（0-1）
- 含细闪：是 / 否
```

### 示例值
```json
{
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
      "color": "浅棕偏灰",
      "pantone": "7536C",
      "arc_angle": 15,
      "tail_drop_angle": 5,
      "density_per_cm": 30,
      "length_cm": 5
    },
    "eyeshadow": {
      "color": "浅粉色珠光",
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
      "curl_angle": 55
    },
    "blush": {
      "color": "粉橘色",
      "diameter_cm": 3,
      "saturation": 0.4
    },
    "lip": {
      "color": "镜面淡粉色",
      "pantone": "13-1907 TPG",
      "brand": "MAC Russian Red",
      "saturation": 0.5,
      "reflectance": 0.9,
      "has_glitter": true
    },
    "highlight": {
      "areas": ["鼻梁中段", "鼻尖", "眉骨", "颧骨顶点", "唇珠上方"],
      "intensity": 0.7
    }
  }
}
```

---

## 模块4: 姿势与动作参数

### 模板结构
```json
[姿势与动作模块]
- 姿态：站立 / 坐姿 / 半倚靠 / 行走
- 身体倾斜方向：___
- 身体倾斜角度：约 ___ °
- 背部接触面积：___ x ___ cm

[头部角度]
- 头部方向：向上 / 向下 / 侧倾
- 头部倾斜角度：约 ___ °
- 颈部前倾角度：___ °

[视线参数]
- 视线方向：向上 / 向下 / 左 / 右
- 眼球转动角度：约 ___ °
- 眼睑下垂角度：___ °

[手部动作]
- 单手 / 双手
- 是否持物：手机 / 书本 / 杯子 / 无
- 持物高度：约 ___ cm
- 手腕弯曲角度：约 ___ °
- 手指握持方式：___

[腿部与站姿]
- 双腿状态：笔直 / 微曲
- 双脚间距：约 ___ cm（较窄 / 与肩同宽 / 较宽）
- 体重分布：___
```

### 示例值
```json
{
  "stance": "standing-leaning",
  "body_tilt_direction": "车门",
  "body_tilt_angle": 10,
  "back_contact_area_cm": [40, 20],
  "head_tilt_angle": 10,
  "neck_forward_angle": 5,
  "gaze_direction": "down",
  "eyeball_rotation_angle": 15,
  "eyelid_droop_angle": 30,
  "hand_position": "holding phone at chest level",
  "holding_object": "phone",
  "holding_height_cm": 120,
  "wrist_bend_angle": 20,
  "leg_state": "straight",
  "feet_distance_cm": 30
}
```

---

## 模块5: 光线与氛围参数

### 模板结构
```json
[灯光模块]
- 主光方向：前方 / 侧前方 / 侧后方 / 顶部
- 主光角度：约 ___ °
- 辅光：有 / 无
- 辅光强度：___（0-1）
- 边缘光强度：___（0-1）
- 边缘光勾勒部位：头发 / 肩部 / 四肢

[对比与色调模块]
- 整体对比度：___（建议 0.8-1.2）
- 阴影深度：___（0-1）
- 高光亮度：___（0-1）
- 色温倾向：偏冷 / 偏暖 / 中性
- 色彩饱和度：___（0-1）
- 颜色偏移：轻微红移 / 青移
- 偏移量：___（0-0.1）

[氛围与颗粒模块]
- 辉光强度：___（0-1）
- 扩散半径：约 ___ 像素
- 体积光：有 / 无
- 体积光密度：___（0-1）
- 光束角度：___ °
- 地面反射率：___（0-1）
- 织物光泽反射率：___（0-1）
- 胶片颗粒：细腻 / 中等 / 粗糙
- 颗粒强度：___（0-1）
- 颗粒大小：___ mm
```

### 示例值
```json
{
  "main_light_direction": "interior",
  "main_light_angle": 45,
  "fill_light": true,
  "fill_light_intensity": 0.3,
  "rim_light_intensity": 0.5,
  "rim_light_areas": ["hair", "legs", "face"],
  "contrast": 1.0,
  "shadow_depth": 0.4,
  "highlight_brightness": 0.9,
  "color_temperature": "warm",
  "saturation": 0.8,
  "color_shift": "red",
  "shift_amount": 0.05,
  "glow_intensity": 0.3,
  "glow_radius_px": 5,
  "volumetric_light": true,
  "volumetric_density": 0.1,
  "volumetric_angle": 45,
  "floor_reflectance": 0.3,
  "fabric_reflectance": 0.4,
  "film_grain": "subtle",
  "grain_intensity": 0.3,
  "grain_size_mm": 0.02
}
```

---

## 模块6: 场景与景深参数

### 模板结构
```json
[场景模块]
- 场景类型：地铁车厢 / 室内 / 室外街景 / 咖啡馆
- 顶高：约 ___ cm
- 通道宽度：约 ___ cm
- 墙壁颜色：___（Pantone ___）
- 主要道具：___
- 道具尺寸：___ x ___ cm
- 背景人物数量：约 ___ 人
- 背景清晰度/模糊度：___（0-1）

[景深与镜头模块]
- 景深范围：主体清晰区域约 ___-___ cm
- 背景模糊程度：轻微 / 中等 / 强烈虚化
- 背景模糊半径：约 ___ 像素
- 镜头焦距：___ mm
  - 24-35mm：广角
  - 50mm：标准
  - 85mm+：人像中长焦
- 镜头畸变：约 ___（0-1）
```

### 示例值
```json
{
  "scene_type": "metro interior",
  "ceiling_height_cm": 200,
  "corridor_width_cm": 250,
  "wall_color": "Cool Gray 1C",
  "props": ["handrails", "seats", "advertisements"],
  "prop_sizes_cm": [100, 50],
  "background_people_count": 4,
  "background_blur": 0.8,
  "depth_of_field_range_cm": [50, 100],
  "background_blur_radius_px": 10,
  "focal_length_mm": 35,
  "lens_distortion": 0.2
}
```

---

## 快速参考表

### 常用比例参考
| 参数 | 标准值 | 修长值 |
|------|--------|--------|
| 脸长宽比 | 1.3:1 | 1.4:1 |
| 上身:下身 | 1:1 | 1:1.5 |
| 眼距 | 3.5cm | 3.0-4.0cm |

### 常用角度参考
| 参数 | 范围 | 典型值 |
|------|------|--------|
| 下颌V角 | 100-140° | 120° |
| 头部倾斜 | 0-30° | 10° |
| 鼻尖上翘 | 0-20° | 10° |

### 常用强度参考 (0-1)
| 参数 | 自然 | 明显 | 强烈 |
|------|------|------|------|
| 皮肤反射率 | 0.7 | 0.9 | 1.0 |
| 水光强度 | 0.4 | 0.7 | 0.9 |
| 对比度 | 0.8 | 1.0 | 1.2 |
| 饱和度 | 0.5 | 0.8 | 1.0 |
