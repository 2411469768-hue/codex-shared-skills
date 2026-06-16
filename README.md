# Codex Shared Skills

这是一个可共享的 Codex skills 集合，主要用于抖音/Seedance 视频创意、商品页改写、广告营销文案和提示词优化。

## 安装方法

下载本仓库后，把 `skills` 目录里的 skill 文件夹复制到你的 Codex 个人 skill 目录：

```text
C:\Users\你的用户名\.codex\skills\
```

复制后重启 Codex。

## 包含的 Skills

### 抖音 / Seedance / 服装视频

- `douyin-video-director`：抖音/千川/Seedance 视频创意总入口
- `douyin-video-remake`：反推、复刻抖音参考视频，生成分镜和 Seedance 提示词
- `seedance-prompt`：女装/千川投放素材的 Seedance 图生视频提示词
- `seedance2-skill`：即梦 Seedance 2.0 通用多模态视频提示词
- `image-to-video`：图片转视频，路由到不同图生视频模型
- `douyin-title-optimizer`：抖音/TikTok Shop 商品标题优化

### 电商页面 / 商品页

- `product-page-remake`：分析竞品商品详情页，重做成原创转化页
- `enhance-prompt`：把模糊 UI 想法优化成更完整的生成提示词

### 广告 / 营销

- `ad-creative`：批量生成广告文案、标题、描述、变体
- `ads`：广告投放策略、预算、受众、出价、优化
- `copywriting`：网站/落地页营销文案改写
- `marketing-ideas`：营销增长点子、推广思路
- `marketing-psychology`：营销心理学、说服框架、消费者决策
- `humanizer`：把 AI 味重的文字改得更像真人写的

## 使用方法

可以直接在 Codex 里点名使用：

```text
$douyin-video-remake 帮我反推这个抖音视频
```

也可以自然描述需求，让 Codex 自动匹配：

```text
帮我把这个抖音视频改成 Seedance 图生视频提示词
```