# 摄影作品画廊 - 图片管理说明

## 目录结构

```
images/gallery/
├── README.md                      # 本文件
├── metadata.json                  # 所有图片的元数据（必需）
├── thumbnails/                    # 缩略图文件夹（可选）
│   ├── sunset.jpg
│   └── ...
├── sunset.jpg                     # 原图放在根目录
├── mountains.jpg
├── night.jpg
└── ...
```

## 如何添加新图片

### 步骤

1. 将图片文件放入 `images/gallery/` 目录
2. 编辑 `metadata.json`，在数组末尾添加一条新记录：

```json
{
  "id": "your-image-id",
  "file": "images/gallery/your-image.jpg",
  "thumbnail": "images/gallery/thumbnails/your-image.jpg",
  "title": "图片标题",
  "description": "图片描述，会显示在画廊页面上。",
  "date": "2025-06-29",
  "tags": ["标签1", "标签2", "标签3"]
}
```

### 字段说明

| 字段 | 必需 | 说明 |
|------|------|------|
| `id` | 是 | 唯一标识符，不能重复 |
| `file` | 是 | 图片文件路径 |
| `thumbnail` | 否 | 缩略图路径（建议 400×300px），省略则显示原图 |
| `title` | 是 | 图片标题 |
| `description` | 否 | 详细描述 |
| `date` | 是 | 拍摄日期（格式 YYYY-MM-DD），画廊按此降序排列 |
| `tags` | 是 | 标签数组，用于筛选 |

### 关于缩略图

大量图片时建议生成缩略图，可大幅提升页面加载速度。
缩略图统一放到 `images/gallery/thumbnails/` 文件夹，建议尺寸 400×300px。
可用命令批量生成（需要 ImageMagick）：

```bash
cd images/gallery
mkdir -p thumbnails
for img in *.jpg; do
  convert "$img" -resize 400x300^ -gravity center -extent 400x300 "thumbnails/$img"
done
```

## 标签建议

保持标签粒度适中，建议使用通用标签：
- **场景**: 风景、城市、人像、微距、街拍
- **元素**: 日落、日出、花卉、建筑、海浪
- **季节**: 春天、夏天、秋天、冬天
- **色调**: 金色、蓝色、暖色、冷色
- **地点**: 海边、山林、城市、乡村

标签越细致，筛选越精准。
