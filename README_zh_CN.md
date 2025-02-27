<div align="center">
<img src="./assets/xorbits-logo.png" width="180px" alt="xorbits" />

# Xorbits Inference：模型推理， 轻而易举 🤖

[![PyPI Latest Release](https://img.shields.io/pypi/v/xinference.svg?style=for-the-badge)](https://pypi.org/project/xinference/)
[![License](https://img.shields.io/pypi/l/xinference.svg?style=for-the-badge)](https://github.com/xorbitsai/inference/blob/main/LICENSE)
[![Build Status](https://img.shields.io/github/actions/workflow/status/xorbitsai/inference/python.yaml?branch=main&style=for-the-badge&label=GITHUB%20ACTIONS&logo=github)](https://actions-badge.atrox.dev/xorbitsai/inference/goto?ref=main)
[![Slack](https://img.shields.io/badge/join_Slack-781FF5.svg?logo=slack&style=for-the-badge)](https://join.slack.com/t/xorbitsio/shared_invite/zt-1o3z9ucdh-RbfhbPVpx7prOVdM1CAuxg)
[![Twitter](https://img.shields.io/twitter/follow/xorbitsio?logo=twitter&style=for-the-badge)](https://twitter.com/xorbitsio)

[English](README.md) | 中文介绍 | [日本語](README_ja_JP.md)
</div>
<br />


Xorbits Inference（Xinference）是一个性能强大且功能全面的分布式推理框架。可用于大语言模型（LLM），语音识别模
型，多模态模型等各种模型的推理。通过 Xorbits Inference，你可以轻松地一键部署你自己的模型或内置的前沿开源模型。
无论你是研究者，开发者，或是数据科学家，都可以通过 Xorbits Inference 与最前沿的 AI 模型，发掘更多可能。


<div align="center">
<i><a href="https://join.slack.com/t/xorbitsio/shared_invite/zt-1z3zsm9ep-87yI9YZ_B79HLB2ccTq4WA">👉 立刻加入我们的 Slack 社区!</a></i>
</div>

## 🔥 近期热点
### 框架增强
- 自定义模型: [#325](https://github.com/xorbitsai/inference/pull/325)
- LoRA 支持: [#271](https://github.com/xorbitsai/inference/issues/271)
- PyTorch 模型多 GPU 支持: [#226](https://github.com/xorbitsai/inference/issues/226)
- Xinference 仪表盘: [#93](https://github.com/xorbitsai/inference/issues/93>)
### 新模型
- 内置 GGML 格式的 Starcoder: [#289](https://github.com/xorbitsai/inference/pull/289)
- 内置 [MusicGen](https://github.com/facebookresearch/audiocraft/blob/main/docs/MUSICGEN.md): [#313](https://github.com/xorbitsai/inference/issues/313)
- 内置 [SD-XL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0): [#318](https://github.com/xorbitsai/inference/issues/318)
### 工具
- LlamaIndex 插件: [#7151](https://github.com/jerryjliu/llama_index/pull/7151)



## 主要功能
🌟 **模型推理，轻而易举**：大语言模型，语音识别模型，多模态模型的部署流程被大大简化。一个命令即可完成模型
的部署工作。 

⚡️ **前沿模型，应有尽有**：框架内置众多中英文的前沿大语言模型，包括 baichuan，chatglm2 等，一键即可体验！内置
模型列表还在快速更新中！


🖥 **异构硬件，快如闪电**：通过 [ggml](https://github.com/ggerganov/ggml)，同时使用你的 GPU 与 CPU 进行推
理，降低延迟，提高吞吐！

⚙️ **接口调用，灵活多样**：提供多种使用模型的接口，包括 RPC，RESTful API，命令行，web UI 等等。方便模型的管理
与监控。

🌐 **集群计算，分布协同**: 支持分布式部署，通过内置的资源调度器，让不同大小的模型按需调度到不同机器，充分使用集
群资源。

🔌 **开放生态，无缝对接**: 与流行的三方库无缝对接，包括 LangChain，LlamaIndex 等（即将到来）。让开发者能够快
速构建基于 AI 的应用。

## 快速入门
Xinference 可以通过 pip 从 PyPI 安装。我们非常推荐在安装前创建一个新的虚拟环境以避免依赖冲突。

### 安装
```bash
$ pip install "xinference"
```
`xinference` 将会安装所有用于推理的基础依赖。

#### 支持 ggml 推理
想要利用 ggml 推理，可以用以下命令：
```bash
$ pip install "xinference[ggml]"
```
如果你想要获得更高效的加速，请查看下列依赖的安装文档：
- [llama-cpp-python](https://github.com/abetlen/llama-cpp-python#installation-from-pypi-recommended) 用于 `baichuan`, `wizardlm-v1.0`, `vicuna-v1.3` 及 `orca`.
- [chatglm-cpp-python](https://github.com/li-plus/chatglm.cpp#getting-started) 用于 `chatglm` 及 `chatglm2`.

#### 支持 PyTorch 推理
想要利用 PyTorch 推理，可以使用以下命令：
```bash
$ pip install "xinference[pytorch]"
```

#### 支持所有类型
如果想要支持推理所有支持的模型，可以安装所有的依赖：
```bash
$ pip install "xinference[all]"
```


### 部署
你可以一键进行本地部署，或按照下面的步骤将 Xinference 部署在计算集群。 

#### 本地部署
运行下面的命令在本地部署 Xinference：
```bash
$ xinference
```

#### 分布式部署
分布式场景下，你需要在一台服务器上部署一个 Xinference supervisor，并在其余服务器上分别部署一个 Xinference
worker。 具体步骤如下：

**启动 supervisor**: 执行:
```bash
$ xinference-supervisor -H "${supervisor_host}"
```
替换 `${supervisor_host}` 为 supervisor 所在服务器的实际主机名或 IP 地址。

**启动 workers**: 在其余服务器上，执行：
```bash
$ xinference-worker -e "http://${supervisor_host}:9997"
```

Xinference 启动后，将会打印服务的 endpoint。这个 endpoint 用于通过命令行工具或编程接口进行模型的管理。

- 本地部署下, endpoint 默认为 `http://localhost:9997`.
- 集群部署下, endpoint 默认为 `http://${supervisor_host}:9997`。其中 `${supervisor_host}` 为
supervisor 所在服务器的主机名或 IP 地址。

你还可以通过 web UI 与任意内置模型聊天。Xinference 甚至**支持同时与两个最前沿的 AI 模型聊天并比较它们的回复质
量**！

![web UI](assets/demo.gif)

### Xinference 命令行
Xinference 提供了命令行工具用于模型管理。支持的命令包括：

- 启动一个模型 (将会返回一个模型 UID)：`xinference launch`
- 查看所有运行中的模型：`xinference list`
- 查看所有内置模型：`xinference list --all`
- 结束模型：`xinference terminate --model-uid ${model_uid}`

### Xinference 编程接口
Xinference 同样提供了编程接口：

```python
from xinference.client import Client

client = Client("http://localhost:9997")
model_uid = client.launch_model(model_name="chatglm2")
model = client.get_model(model_uid)

chat_history = []
prompt = "What is the largest animal?"
model.chat(
            prompt,
            chat_history,
            generate_config={"max_tokens": 1024}
        )
```

返回值：
```json
{
  "id": "chatcmpl-8d76b65a-bad0-42ef-912d-4a0533d90d61",
  "model": "56f69622-1e73-11ee-a3bd-9af9f16816c6",
  "object": "chat.completion",
  "created": 1688919187,
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "The largest animal that has been scientifically measured is the blue whale, which has a maximum length of around 23 meters (75 feet) for adult animals and can weigh up to 150,000 pounds (68,000 kg). However, it is important to note that this is just an estimate and that the largest animal known to science may be larger still. Some scientists believe that the largest animals may not have a clear \"size\" in the same way that humans do, as their size can vary depending on the environment and the stage of their life."
      },
      "finish_reason": "None"
    }
  ],
  "usage": {
    "prompt_tokens": -1,
    "completion_tokens": -1,
    "total_tokens": -1
  }
}
```

请参考 [更多案例](examples)。


## 内置模型
运行以下命令查看内置模型列表：
```bash
$ xinference list --all
```

### ggmlv3 模型

| Name          | Type             | Language | Format  | Size (in billions) | Quantization                            |
|---------------|------------------|----------|---------|--------------------|-----------------------------------------|
| llama-2       | Foundation Model | en       | ggmlv3  | 7, 13              | 'q2_K', 'q3_K_L', ... , 'q6_K', 'q8_0'  |
| baichuan      | Foundation Model | en, zh   | ggmlv3  | 7                  | 'q2_K', 'q3_K_L', ... , 'q6_K', 'q8_0'  |
| llama-2-chat  | RLHF Model       | en       | ggmlv3  | 7, 13, 70          | 'q2_K', 'q3_K_L', ... , 'q6_K', 'q8_0'  |
| chatglm       | SFT Model        | en, zh   | ggmlv3  | 6                  | 'q4_0', 'q4_1', 'q5_0', 'q5_1', 'q8_0'  |
| chatglm2      | SFT Model        | en, zh   | ggmlv3  | 6                  | 'q4_0', 'q4_1', 'q5_0', 'q5_1', 'q8_0'  |
| wizardlm-v1.0 | SFT Model        | en       | ggmlv3  | 7, 13, 33          | 'q2_K', 'q3_K_L', ... , 'q6_K', 'q8_0'  |
| wizardlm-v1.1 | SFT Model        | en       | ggmlv3  | 13                 | 'q2_K', 'q3_K_L', ... , 'q6_K', 'q8_0'  |
| vicuna-v1.3   | SFT Model        | en       | ggmlv3  | 7, 13              | 'q2_K', 'q3_K_L', ... , 'q6_K', 'q8_0'  |
| orca          | SFT Model        | en       | ggmlv3  | 3, 7, 13           | 'q4_0', 'q4_1', 'q5_0', 'q5_1', 'q8_0'  |

### pytorch 模型

| Name          | Type             | Language | Format  | Size (in billions) | Quantization             |
|---------------|------------------|----------|---------|--------------------|--------------------------|
| baichuan      | Foundation Model | en, zh   | pytorch | 7, 13              | '4-bit', '8-bit', 'none' |
| baichuan-chat | SFT Model        | en, zh   | pytorch | 13                 | '4-bit', '8-bit', 'none' |
| vicuna-v1.3   | SFT Model        | en       | pytorch | 7, 13, 33          | '4-bit', '8-bit', 'none' |


**注意**:
- Xinference 会自动为你下载模型，默认的模型存放路径为 `${USER}/.xinference/cache`。
- 基础模型仅提供 `generate` 接口.
- RLHF 与 SFT 模型 提供 `generate` 与 `chat` 接口。
- 如果想使用 Apple metal GPU 加速，请选择 q4_0 或者 q4_1 这两种量化方式。
- `llama-2-chat` 70B ggmlv3 模型目前仅支持 q4_0 量化方式。

## 自定义模型\[Experimental\]
自定义模型目前是实验性功能，预计将会在 v0.2.0 版本正式与大家见面。

添加自定义模型前，请根据模版填写模型配置：
```python
custom_model = {
  "version": 1,
  # model name. must start with a letter or a 
  # digit, and can only contain letters, digits, 
  # underscores, or dashes.
  "model_name": "nsql-2B",  
  # supported languages
  "model_lang": [
    "en"
  ],
  # model abilities. could be "embed", "generate"
  # and "chat".
  "model_ability": [
    "generate"
  ],
  # model specifications.
  "model_specs": [
    {
      # model format.
      "model_format": "pytorch",
      "model_size_in_billions": 2,
      # quantizations.
      "quantizations": [
        "4-bit",
        "8-bit",
        "none"
      ],
      # hugging face model ID.
      "model_id": "NumbersStation/nsql-2B"
    }
  ],
  # prompt style, required by chat models.
  # for more details, see: xinference/model/llm/tests/test_utils.py
  "prompt_style": None
}
```

注册自定义模型：
```python
import json

from xinference.client import Client

# replace with real xinference endpoint
endpoint = "http://localhost:9997"
client = Client(endpoint)
client.register_model(model_type="LLM", model=json.dumps(custom_model), persist=False)
```

加载模型：
```python
uid = client.launch_model(model_name='nsql-2B')
```

推理：
```python
text = """CREATE TABLE work_orders (
    ID NUMBER,
    CREATED_AT TEXT,
    COST FLOAT,
    INVOICE_AMOUNT FLOAT,
    IS_DUE BOOLEAN,
    IS_OPEN BOOLEAN,
    IS_OVERDUE BOOLEAN,
    COUNTRY_NAME TEXT,
)

-- Using valid SQLite, answer the following questions for the tables provided above.

-- how many work orders are open?

SELECT"""

model = client.get_model(model_uid=uid)
model.generate(prompt=text)
```

结果：
```json
{
   "id":"aeb5c87a-352e-11ee-89ad-9af9f16816c5",
   "object":"text_completion",
   "created":1691418511,
   "model":"3b912fc4-352e-11ee-8e66-9af9f16816c5",
   "choices":[
      {
         "text":" COUNT(*) FROM work_orders WHERE IS_OPEN = '1';",
         "index":0,
         "logprobs":"None",
         "finish_reason":"stop"
      }
   ],
   "usage":{
      "prompt_tokens":117,
      "completion_tokens":17,
      "total_tokens":134
   }
}
```

## Pytorch 模型最佳实践

近期集成了 Pytorch ，下面对 Pytorch 模型的使用场景进行说明：

### 模型支持
- Foundation Model：baichuan（7B、13B）。
- SFT Model：baichuan-chat（13B）、vicuna-v1.3（7B、13B、33B）。

### 设备支持
- CUDA：在 Linux、Windows 系统下，默认使用 `cuda` 设备。
- MPS：在 Mac M1/M2 设备上，默认使用 `mps` 设备。
- CPU：不建议使用 `cpu` 设备，显存占用较大，且推理速度非常慢。

### 量化方式
- `none`：表示不使用量化。
- `8-bit`：使用 8-bit 量化。
- `4-bit`：使用 4-bit 量化。注意：4-bit 量化仅在 Linux 系统、CUDA 设备上支持。

### 其他说明
- 在 MacOS 系统上，不支持 baichuan-chat 模型，baichuan 模型无法使用 8-bit 量化。

### 使用案例

下表展示部分模型显存占用情况与设备支持情况。

| Name          | Size (B) | OS    | No quantization (MB) | Quantization 8-bit (MB) | Quantization 4-bit (MB) |
|---------------|----------|-------|----------------------|-------------------------|-------------------------|
| baichuan-chat | 13       | linux | 暂未测试                 | 13275                   | 7263                    |
| baichuan-chat | 13       | macos | 不支持                  | 不支持                     | 不支持                     |
| vicuna-v1.3   | 7        | linux | 12884                | 6708                    | 3620                    |
| vicuna-v1.3   | 7        | macos | 12916                | 565                     | 不支持                     |
| baichuan      | 7        | linux | 13480                | 7304                    | 4216                    |
| baichuan      | 7        | macos | 13480                | 不支持                     | 不支持                     |

## 近期开发计划
Xinference 目前正在快速迭代。我们近期的开发计划包括：

### Langchain & LlamaIndex integration
通过与 Langchain 及 LlamaIndex 集成，用户将能够通过 Xinference，基于开源模型快速构建 AI 应用。 

