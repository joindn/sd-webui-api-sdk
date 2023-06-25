### 封装了官方所有API，以文生图和图生图作为示例
# [![npm version](https://badge.fury.io/js/sd-webui-api-sdk.svg)](https://badge.fury.io/js/sd-webui-api-sdk)

# 示例
```
// 文生图
import express from "express";
import {
  SdApi,
} from "sd-webui-api-sdk";
const port = 3000;

const basePath = "http://127.0.0.1:7860";
const sdApi = new SdApi(undefined, basePath);
const app = express();
app.use(express.json());

app.post("/txt2Img", async (req: any, res: any) => {
  const {
    prompt, // 提示
    negative_prompt, // 负面提示
    styles, // 风格
    sampler_name, // 采样方法
    steps, // 采样步数
    restore_faces, // 恢复面部
    tiling, // 平铺
    enable_hr, // 启用高分辨率
    hr_upscaler, // 高分辨率放大器
    hr_second_pass_steps, // 高分辨率第二次采样步数
    denoising_strength, // 降噪强度
    hr_scale, // 高分辨率放大比例
    width, // 宽度
    height, // 高度
    n_iter, // Batch count
    batch_size, // Batch size
    cfg_scale, // 提示词相关性
    seed, // 种子
    override_settings, // 覆盖设置
  } = req.body;
  const imageResponse = await sdApi.text2imgapiSdapiV1Txt2imgPost(
    {
      prompt, // 提示
      negative_prompt, // 负面提示
      styles, // 风格
      sampler_name, // 采样方法
      steps, // 采样步数
      restore_faces, // 恢复面部
      tiling, // 平铺
      enable_hr, // 启用高分辨率
      hr_upscaler, // 高分辨率放大器
      hr_second_pass_steps, // 高分辨率第二次采样步数
      denoising_strength, // 降噪强度
      hr_scale, // 高分辨率放大比例
      width, // 宽度
      height, // 高度
      n_iter, // Batch count
      batch_size, // Batch size
      cfg_scale, // 提示词相关性
      seed, // 种子
      override_settings, // 覆盖设置
    }
  );
  const imageBase64 = imageResponse?.data?.images ?? [];
  const html = imageBase64
    .map((image: string) => `<img src="data:image/png;base64,${image}" />`)
    .join("");
  res.setHeader("Content-Type", "text/html");
  res.send(html);
});

// 图生图
app.post("/img2Img", async (req: any, res: any) => {
  const {
    prompt, // 提示
    negative_prompt, // 负面提示
    styles, // 风格
    init_images, // 初始图片 base64格式数组
    resize_mode, // 重置模式 默认0
    sampler_name, // 采样方法
    steps, // 采样步数
    restore_faces, // 恢复面部
    tiling, // 平铺
    width, // 宽度
    height, // 高度
    n_iter, // Batch count
    batch_size, // Batch size
    cfg_scale, // 提示词相关性
    denoising_strength, // 降噪强度
    seed, // 种子
    override_settings, // 覆盖设置
  } = req.body;
  const imageResponse = await sdApi.img2imgapiSdapiV1Img2imgPost(
    {
      prompt, // 提示
      negative_prompt, // 负面提示
      styles, // 风格
      init_images, // 初始图片 base64格式数组
      resize_mode, // 重置模式 默认0
      sampler_name, // 采样方法
      steps, // 采样步数
      restore_faces, // 恢复面部
      tiling, // 平铺
      width, // 宽度
      height, // 高度
      n_iter, // Batch count
      batch_size, // Batch size
      cfg_scale, // 提示词相关性
      denoising_strength, // 降噪强度
      seed, // 种子
      override_settings, // 覆盖设置
    }
  );
  const imageBase64 = imageResponse?.data?.images ?? [];
  const html = imageBase64
    .map((image: string) => `<img src="data:image/png;base64,${image}" />`)
    .join("");
  res.setHeader("Content-Type", "text/html");
  res.send(html);
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```

## 调用示例
```
文生图
curl --location 'http://127.0.0.1:3000/txt2Img' \
--header 'Content-Type: application/json' \
--data '{
    "prompt": "",
    "styles": [
        "test1"
    ],
    "seed": -1,
    "sampler_name": "DPM++ SDE Karras",
    "n_iter": 4,
    "steps": 20,
    "cfg_scale": 7.0,
    "width": 512,
    "height": 768,
    "restore_faces": true,
    "negative_prompt": "",
    "override_settings": {
        "sd_model_checkpoint": "a1535d0a42" // 大模型的hash
    },
    "enable_hr": false,
    "hr_scale": 2,
    "hr_upscaler": "4x-UltraSharp",
    "hr_second_pass_steps": 10,
    "denoising_strength": 0.55
}'

图生图
curl --location 'http://127.0.0.1:3000/img2Img' \
--header 'Content-Type: application/json' \
--data '{
    "prompt": "",
    "styles": [
        "test1"
    ],
    "seed": -1,
    "sampler_name": "DPM++ SDE Karras",
    "resize_mode": 0,
    "n_iter": 1,
    "steps": 20,
    "cfg_scale": 7.0,
    "width": 512,
    "height": 768,
    "restore_faces": true,
    "negative_prompt": "",
    "override_settings": {
        "sd_model_checkpoint": "a1535d0a42" // 大模型的hash
    },
    "init_images":["iVBORw0KG.....TkSuQmCC"],
    "denoising_strength": 0.55
}'
```
```
交流也可以加我微信：_Mr_JD_
```