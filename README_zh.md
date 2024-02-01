<div align="center">

<!-- <!-- <h1 style="color: #33A6B8; font-family: Helvetica"> OmniLMM </h1> -->

<img src="./assets/title-2.png" width="200em" ></img> 

**大型多模态模型，性能强大且高效部署**
<p align="center">
  OmniLMM-3B  <a href="https://huggingface.co/openbmb/MiniCPM-V/">🤗</a> <a href="http://120.92.209.146:80/">🤖</a> |
  OmniLMM-12B <a href="https://huggingface.co/openbmb/OmniLMM-12B/">🤗</a> <a href="http://120.92.209.146:8081">🤖</a>
</p>

</div>


**OmniLMM** 是一系列善于视觉和语言建模的开源多模态大模型（LMMs）。该系列模型接受图像和文本输入，并提供高质量的文本输出。我们发布了两个版本的 OmniLMM，旨在实现**强大的性能和高效的部署**：

- **OmniLMM-12B**：相比同规模其他模型在多个基准测试中具有领先性能。

- **OmniLMM-3B**：可在终端设备上部署并具备先进的多模态对话能力。

## 目录
- [OmniLMM-12B](#omnilmm-12b)
- [OmniLMM-3B](#omnilmm-3b)
- [演示](#demo)
- [安装](#install)
- [推理](#inference)
- [模型库](#model-zoo)

## OmniLMM-12B
**OmniLMM-12B** 是当前系列中性能最强大的版本。该模型使用一个感知重采样层连接 EVA02-5B 和 Zephyr-7B-β 来构建，采用了课程学习的方法在多模态数据上进行训练。该模型具有三个显著特征：

- 🔥 **卓越性能。**

  OmniLMM-12B 相比其他同规模模型在多个基准测试中取得**领先的性能**（包括 MME、MMBench、SEED-Bench 等）。该模型还**支持OCR功能**，并掌握了**丰富的多模态世界知识**。

- 🏆 **可信行为。**

  LMMs 的幻觉问题备受关注，模型经常生成和图像中的事实不符的文本（例如，信誓旦旦地描述图片中并不存在的物体）。OmniLMM-12B是 **第一个通过多模态 RLHF 对齐的最新开源 LMM 来实现可信行为**（通过我们最近提出的 [RLHF-V](https://rlhf-v.github.io/) 技术），并在[MMHal-Bench](https://huggingface.co/datasets/Shengcao1006/MMHal-Bench)幻觉评测基准上**排名第一**。

- 🕹 **实时多模态交互。**

  我们将 OmniLMM-12B 和 GPT-3.5 结合成一个**实时多模态交互助手**。该助手接受来自相机的视频流和来自麦克风的语音流，并发出语音输出。我们发现该模型**无需进行任何视频编辑**就可以**复现出现在 Gemini 演示视频中的一些有趣例子**。

### 性能评估

<table>
<thead>
  <tr>
    <th align="left">Model</th>
    <th>Size</th>
    <th>MME</th>
    <th nowrap="nowrap">MMB dev (en)</th>
    <th nowrap="nowrap" >MMMU val</th>
    <th nowrap="nowrap" >MMHal-Bench</th>
    <th nowrap="nowrap" >Object HalBench</th>
    <th nowrap="nowrap" >SeedBench-I</th>
    <th>MathVista</th>
    <th nowrap="nowrap" >LLaVA Bench W</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td align="left">GPT-4V†</td>
    <td>-</td>
    <td>1409</td>
    <td>75.1 </td>
    <td>56.8</td>
    <td>3.53 / 70.8</td>
    <td>86.4 / 92.7</td>
    <td>71.6 </td>
    <td>47.8 </td>
    <td>93.1 </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left">Qwen-VL-Plus†</td>
    <td>-</td>
    <td>1681</td>
    <td>66.2 </td>
    <td>45.2</td>
    <td>- </td>
    <td>- </td>
    <td>65.7 </td>
    <td>36.0 </td>
    <td>73.7 </td>
  </tr>
  <tr>
    <td align="left">Yi-VL 6B</td>
    <td align="right">6.7B </td>
    <td>- </td>
    <td>68.2 </td>
    <td>39.1 </td>
    <td>- </td>
    <td>- </td>
    <td>66.1 </td>
    <td>28.0 </td>
    <td>39.9 </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left" >Qwen-VL-Chat</td>
    <td align="right">9.6B</td>
    <td>1488</td>
    <td>60.6 </td>
    <td>35.9</td>
    <td>2.93 / 59.4</td>
    <td>56.2 / 80.0</td>
    <td>64.8 </td>
    <td>33.8 </td>
    <td>67.7 </td>
  </tr>
  <tr>
    <td align="left" >CogVLM</td>
    <td align="right">17.4B</td>
    <td>1438</td>
    <td>63.7 </td>
    <td>32.1 </td>
    <td>2.68 / 52.1 </td>
    <td>73.6 / 87.4 </td>
    <td>68.8 </td>
    <td>34.7 </td>
    <td>73.9 </td>
  </tr>
  <tr>
    <td align="left" >LLaVA 1.5</td>
    <td align="right">13.6B </td>
    <td>1531 </td>
    <td>68.2 </td>
    <td>36.4 </td>
    <td>2.71 / 51.0 </td>
    <td>53.7 / 77.4 </td>
    <td>68.1 </td>
    <td>26.4 </td>
    <td>64.6 </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left" ><b>OmniLMM-12B</b></td>
    <td align="right">11.6B </td>
    <td>1637 </td>
    <td>71.6 </td>
    <td>40.7 </td>
    <td>3.45 / 68.8 </td>
    <td>90.3 / 95.5 </td>
    <td>71.1 </td>
    <td>34.9 </td>
    <td>72.0 </td>
  </tr>
</tbody>
</table>
<small>†: Proprietary models</small>


## OmniLMM-3B

**OmniLMM-3B**（即 MiniCPM-V）是一种我们的高效率版本模型，可用于终端机器上的部署。该模型基于SigLip-400M和MiniCPM-2.4B构建，通过感知器重采样器连接。OmniLMM-3B的显著特点包括：

- ⚡️ **高效率。**

  OmniLMM-3B可以**高效地部署在大多数GPU卡和个人电脑上**，甚至**在移动手机等边缘设备上**。在视觉编码方面，我们通过感知器重采样器将图像表示压缩为64个令牌，远远少于基于MLP架构的其他LMMs（通常> 512个令牌）。这使得OmniLMM-3B在推理期间**内存成本更低且速度更快**。

- 🔥 **有望的性能。**

  OmniLMM-3B在与相似大小模型相比的多个基准测试中实现了**最先进的性能**，超过了基于Phi-2构建的现有LMMs。它甚至**实现了与9.6B Qwen-VL-Chat相媲美或更好的性能**。

- 🙌 **双语支持。**

  OmniLMM-3B是**第一个支持英语和中文双语多模态交互的边缘可部署LMM**。这是通过跨语言泛化多模态能力实现的，这是我们ICLR 2024焦点[论文](https://arxiv.org/abs/2308.12038)中的一项技术。

### Evaluation

<div align="center">

<table style="margin: 0px auto;">
<thead>
  <tr>
    <th align="left">Model</th>
    <th>Size</th>
    <th>MME</th>
    <th nowrap="nowrap" >MMB dev (en)</th>
    <th nowrap="nowrap" >MMB dev (zh)</th>
    <th nowrap="nowrap" >MMMU val</th>
    <th nowrap="nowrap" >CMMMU val</th>
  </tr>
</thead>
<tbody align="center">
  <tr>
    <td align="left">LLaVA-Phi</td>
    <td align="right">3B</td>
    <td>1335</td>
    <td>59.8</td>
    <td>- </td>
    <td>- </td>
    <td>- </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left">MobileVLM</td>
    <td align="right">3B</td>
    <td>1289</td>
    <td>59.6</td>
    <td>- </td>
    <td>- </td>
    <td>- </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left" >Imp-v1</td>
    <td align="right">3B</td>
    <td>1434</td>
    <td>66.5</td>
    <td>- </td>
    <td>- </td>
    <td>- </td>
  </tr>
  <tr>
    <td align="left" >Qwen-VL-Chat</td>
    <td align="right" >9.6B</td>
    <td>1487</td>
    <td>60.6 </td>
    <td>56.7 </td>
    <td>35.9 </td>
    <td>30.7 </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left" >CogVLM</td>
    <td align="right">17.4B </td>
    <td>1438 </td>
    <td>63.7 </td>
    <td>53.8 </td>
    <td>32.1 </td>
    <td>- </td>
  </tr>
  <tr>
    <td nowrap="nowrap" align="left" ><b>OmniLMM-3B</b></td>
    <td align="right">3B </td>
    <td>1452 </td>
    <td>67.3 </td>
    <td>61.9 </td>
    <td>34.7 </td>
    <td>32.1 </td>
  </tr>
</tbody>
</table>

</div>

### Examples

<table align="center" >
  <p align="center" > 
    <img src="assets/Snake_cn_Mushroom_en.gif" width=48%/>
  </p>
</table>

## Demo
Click here to try out the Demo of [OmniLMM-12B](http://120.92.209.146:8081) and [OmniLMM-3B](http://120.92.209.146:80).

## Install

1. Clone this repository and navigate to the source folder

```bash
git clone https://github.com/OpenBMB/OmniLMM.git
cd OmniLMM
```

2. Create conda environment

```Shell
conda create -n OmniLMM python=3.10 -y
conda activate OmniLMM
```

3. Install dependencies

```shell
pip install -r requirements.txt
```

## Inference

### Model Zoo
| Model                | Description       | Download Link |
|:----------------------|:-------------------|:---------------:|
| OmniLMM-12B | The most capable version with strong performance.                   |  [🤗](https://huggingface.co/openbmb/OmniLMM-12B) &nbsp;&nbsp; <a url="https://modelscope.cn/models/OpenBMB/OmniLMM-12B/files"> <img src="./assets/modelscope_logo.png" width="20px"></img></a> |
| OmniLMM-3B  | The efficient version for edge device deployment.          |  [🤗](https://huggingface.co/openbmb/MiniCPM-V) &nbsp;&nbsp; <a url="https://modelscope.cn/models/OpenBMB/MiniCPM-V/files"> <img src="./assets/modelscope_logo.png" width="20px"></img></a> |


### Multi-turn Conversation
Please refer to the following codes to run `OmniLMM`.

<div align="center">
<img src="assets/COCO_test2015_000000262144.jpg" width="660px">
</div>

##### OmniLMM-12B
```python
from chat import OmniLMMChat, img2base64

chat_model = OmniLMMChat('openbmb/OmniLMM-12B')

im_64 = img2base64('./assets/COCO_test2015_000000262144.jpg')

# First round chat 
msgs = [{"role": "user", "content": "What are the people doing?"}]

inputs = {"image": im_64, "question": json.dumps(msgs)}
answer = chat_model.process(inputs)
print(answer)

# Second round chat 
# pass history context of multi-turn conversation
msgs.append({"role": "assistant", "content": answer})
msgs.append({"role": "user", "content": "Describe the image"})

inputs = {"image": im_64, "question": json.dumps(msgs)}
answer = chat_model.process(inputs)
print(answer)
```

We can obtain the following results:
```
"The people in the image are playing baseball. One person is pitching a ball, another one is swinging a bat to hit it, and there's also an umpire present who appears to be watching the game closely."

"The image depicts a baseball game in progress. A pitcher is throwing the ball, while another player is swinging his bat to hit it. An umpire can be seen observing the play closely."
```

##### OmniLMM-3B
```python
import torch
from PIL import Image
from transformers import AutoModel, AutoTokenizer

model_path='openbmb/MiniCPM-V'
model = AutoModel.from_pretrained(model_path, trust_remote_code=True).to(dtype=torch.bfloat16)
tokenizer = AutoTokenizer.from_pretrained(model_path, trust_remote_code=True)
model.eval().cuda()

image = Image.open('./assets/COCO_test2015_000000262144.jpg').convert('RGB')

question = '请描述一下该图像'
res, context, _ = model.chat(
    image=image,
    question=question,
    context=None,
    tokenizer=tokenizer,
    sampling=True,
    temperature=0.7
)
print(res)
```

## ✅ TODO

- [ ] Fine-tuning support
- [ ] Local Web-UI deployment
- [ ] Code release for real-time interactive assistant

## 🏫 机构

本项目由以下机构共同开发：

- <img src="assets/thunlp.png" width="28px"> [清华大学自然语言处理实验室](https://nlp.csai.tsinghua.edu.cn/)
- <img src="assets/modelbest.png" width="28px"> [面壁智能](https://modelbest.cn/)
- <img src="assets/zhihu.webp" width="28px"> [知乎](https://www.zhihu.com/ )

