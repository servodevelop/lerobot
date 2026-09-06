# Star Arm 102 生态的 LeRobot 框架集成

[English](README.md)

## Ecosystem

servodevelop/lerobot 是 Fashion Star 在 Star Arm 102 机械臂生态中的 LeRobot 框架集成 fork，用于连接机器人学习、遥操作工作流与中心开发资源。

- 🔗 [Star Arm 102 Series Hub](https://fashionstar.com.hk/robot-arm/star-arm-102/)
- 🐙 [Main Repo: Star-Arm-102](https://github.com/servodevelop/Star-Arm-102)

## 关于本 fork

本仓库 fork 自 [Hugging Face LeRobot](https://github.com/huggingface/lerobot)。Fashion Star 硬件配置与集成指南请参阅上方 Star-Arm-102 主仓库。以下介绍对应上游项目的安装、示例和贡献流程；上游机器人示例适用于各自的硬件。

<p align="center">
  <img alt="LeRobot, Hugging Face Robotics Library" src="https://raw.githubusercontent.com/huggingface/lerobot/main/media/lerobot-logo-thumbnail.png" width="100%">
  <br/>
  <br/>
</p>

<div align="center">

[![Tests](https://github.com/huggingface/lerobot/actions/workflows/nightly.yml/badge.svg?branch=main)](https://github.com/huggingface/lerobot/actions/workflows/nightly.yml?query=branch%3Amain)
[![Python versions](https://img.shields.io/pypi/pyversions/lerobot)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/huggingface/lerobot/blob/main/LICENSE)
[![Status](https://img.shields.io/pypi/status/lerobot)](https://pypi.org/project/lerobot/)
[![Version](https://img.shields.io/pypi/v/lerobot)](https://pypi.org/project/lerobot/)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.1-ff69b4.svg)](https://github.com/huggingface/lerobot/blob/main/CODE_OF_CONDUCT.md)
[![Discord](https://dcbadge.vercel.app/api/server/C5P34WJ68S?style=flat)](https://discord.gg/s3KuuzsPFb)

<!-- [![Coverage](https://codecov.io/gh/huggingface/lerobot/branch/main/graph/badge.svg?token=TODO)](https://codecov.io/gh/huggingface/lerobot) -->

</div>


## 构建自己的 HopeJR 机器人

![HopeJR 机器人](https://raw.githubusercontent.com/huggingface/lerobot/main/media/hope_jr/hopejr.png)

HopeJR 是用于灵巧操作的人形机器人手臂与手部系统。通过外骨骼和手套可以精确控制手部动作，适用于高级操作任务。参阅 [HopeJR 完整教程](https://huggingface.co/docs/lerobot/hope_jr)。

## 构建自己的 SO-101 机器人

![SO-101 从臂](https://raw.githubusercontent.com/huggingface/lerobot/main/media/so101/so101.webp)
![SO-101 主臂](https://raw.githubusercontent.com/huggingface/lerobot/main/media/so101/so101-leader.webp)

SO-101 是 SO100 的更新版本。上游 README 介绍每条手臂售价仅 €114，并展示通过笔记本电脑上的简单动作，在几分钟内完成训练后让机器人自主执行任务的流程。参阅 [SO-101 完整教程](https://huggingface.co/docs/lerobot/so101)。

还可以构建 LeKiwi，让 SO-101 具备移动能力。参阅 [LeKiwi 教程](https://huggingface.co/docs/lerobot/lekiwi)。

![LeKiwi 移动机器人](https://raw.githubusercontent.com/huggingface/lerobot/main/media/lekiwi/kiwi.webp)

## LeRobot：面向真实世界机器人的先进 AI

🤗 LeRobot 提供基于 PyTorch 的模型、数据集和工具，旨在降低机器人技术的入门门槛，让所有人都能贡献并受益于共享的数据集和预训练模型。

LeRobot 聚焦模仿学习与强化学习，包含已验证可迁移到真实世界的先进方法。项目提供预训练模型、人工演示数据集和仿真环境，让用户无需先组装机器人即可开始学习。上游计划继续扩展对经济实用机器人硬件的支持。

预训练模型和数据集发布在 [Hugging Face LeRobot 社区](https://huggingface.co/lerobot)。

### 仿真环境中的预训练模型示例

| ALOHA 环境中的 ACT 策略 | SimXArm 环境中的 TDMPC 策略 | PushT 环境中的 Diffusion 策略 |
| --- | --- | --- |
| ![ACT](https://raw.githubusercontent.com/huggingface/lerobot/main/media/gym/aloha_act.gif) | ![TDMPC](https://raw.githubusercontent.com/huggingface/lerobot/main/media/gym/simxarm_tdmpc.gif) | ![Diffusion](https://raw.githubusercontent.com/huggingface/lerobot/main/media/gym/pusht_diffusion.gif) |

## 安装

LeRobot 要求 Python 3.10+ 和 PyTorch 2.2+。

### 配置环境

使用 [miniforge](https://conda-forge.org/download/) 等工具创建并激活 Python 3.10 虚拟环境：

```bash
conda create -y -n lerobot python=3.10
conda activate lerobot
```

如果使用 conda，在该环境中安装 ffmpeg：

```bash
conda install ffmpeg -c conda-forge
```

通常会安装为当前平台构建、包含 libsvtav1 编码器的 ffmpeg 7.X。可运行 `ffmpeg -encoders` 检查支持的编码器。若缺少 libsvtav1：

- 所有平台均可明确安装 ffmpeg 7.1.1：

~~~bash
conda install ffmpeg=7.1.1 -c conda-forge
~~~

- Linux 用户也可安装 [ffmpeg 编译依赖](https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu#GettheDependencies)，并[从源码编译包含 libsvtav1 的 ffmpeg](https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu#libsvtav1)。使用 `which ffmpeg` 确认调用的是对应的二进制文件。

### 从源码安装 LeRobot 🤗

上游源码安装方法如下；这里保留上游示例地址：

```bash
git clone https://github.com/huggingface/lerobot.git
cd lerobot
```

以可编辑模式安装，便于修改代码和贡献：

```bash
pip install -e .
```

如果编译失败，可能需要安装 cmake、build-essential 和 ffmpeg 库。Linux 可执行：

~~~bash
sudo apt-get install cmake build-essential python3-dev pkg-config libavformat-dev libavcodec-dev libavdevice-dev libavutil-dev libswscale-dev libswresample-dev libavfilter-dev
~~~

其他系统参阅 [PyAV 编译说明](https://pyav.org/docs/develop/overview/installation.html#bring-your-own-ffmpeg)。

LeRobot 提供可选的 Gymnasium 仿真环境：[aloha](https://github.com/huggingface/gym-aloha)、[xarm](https://github.com/huggingface/gym-xarm)、[pusht](https://github.com/huggingface/gym-pusht)。例如，安装 aloha 和 pusht：

```bash
pip install -e ".[aloha, pusht]"
```

### 从 PyPI 安装

安装基础库及默认依赖：

```bash
pip install lerobot
```

安装额外功能：

~~~bash
pip install 'lerobot[all]'          # 所有可选功能
pip install 'lerobot[aloha,pusht]'  # Aloha 与 Pusht
pip install 'lerobot[feetech]'      # Feetech 电机支持
~~~

将方括号中的内容替换为所需功能。完整可选标签见 [PyPI 项目页面](https://pypi.org/project/lerobot/)。

### Weights & Biases

若使用 [Weights & Biases](https://docs.wandb.ai/quickstart) 跟踪实验，请登录，并在配置中启用 WandB：

```bash
wandb login
```

### 数据集可视化

[数据集加载示例](https://github.com/huggingface/lerobot/blob/main/examples/dataset/load_lerobot_dataset.py) 展示如何使用会自动从 Hugging Face Hub 下载数据的数据集类。

可通过命令行查看 Hub 数据集中的一个 episode：

```bash
lerobot-dataset-viz \
    --repo-id lerobot/pusht \
    --episode-index 0
```

查看本地数据时，设置 root 和 mode local；以下示例在 `./my_local_data_dir/lerobot/pusht` 查找数据：

```bash
lerobot-dataset-viz \
    --repo-id lerobot/pusht \
    --root ./my_local_data_dir \
    --mode local \
    --episode-index 0
```

程序会打开 rerun.io，显示相机视频流、机器人状态与动作。英文 README 保留了上游演示视频。工具也支持远程服务器中的数据集；参阅 `lerobot-dataset-viz --help`。

### LeRobotDataset 格式

使用 `dataset = LeRobotDataset("lerobot/aloha_static_coffee")`，即可从 Hugging Face Hub 加载数据，也可以从本地目录加载。它支持类似 Hugging Face 或 PyTorch 数据集的索引方式；例如 `dataset[0]` 返回包含观测和动作张量的一个时间帧。

通过 delta_timestamps 可以按时间关系获取多个帧。例如，设置 `delta_timestamps = {"observation.image": [-1, -0.5, -0.2, 0]}`，即可取得索引帧，以及该帧之前 1 秒、0.5 秒和 0.2 秒的三个图像帧。参阅[加载示例](https://github.com/huggingface/lerobot/blob/main/examples/dataset/load_lerobot_dataset.py)。

该格式采用多种序列化方法，以灵活而简洁的结构支持仿真和真实世界中的强化学习及机器人任务。它重点支持相机与机器人状态，也可以扩展到其他可表示为张量的传感器数据。下面保留字段名称与结构，便于对应代码：

```
dataset attributes:
  ├ hf_dataset: a Hugging Face dataset (backed by Arrow/parquet). Typical features example:
  │  ├ observation.images.cam_high (VideoFrame):
  │  │   VideoFrame = {'path': path to a mp4 video, 'timestamp' (float32): timestamp in the video}
  │  ├ observation.state (list of float32): position of an arm joints (for instance)
  │  ... (more observations)
  │  ├ action (list of float32): goal position of an arm joints (for instance)
  │  ├ episode_index (int64): index of the episode for this sample
  │  ├ frame_index (int64): index of the frame for this sample in the episode ; starts at 0 for each episode
  │  ├ timestamp (float32): timestamp in the episode
  │  ├ next.done (bool): indicates the end of an episode ; True for the last frame in each episode
  │  └ index (int64): general index in the whole dataset
  ├ meta: a LeRobotDatasetMetadata object containing:
  │  ├ info: a dictionary of metadata on the dataset
  │  │  ├ codebase_version (str): this is to keep track of the codebase version the dataset was created with
  │  │  ├ fps (int): frame per second the dataset is recorded/synchronized to
  │  │  ├ features (dict): all features contained in the dataset with their shapes and types
  │  │  ├ total_episodes (int): total number of episodes in the dataset
  │  │  ├ total_frames (int): total number of frames in the dataset
  │  │  ├ robot_type (str): robot type used for recording
  │  │  ├ data_path (str): formattable string for the parquet files
  │  │  └ video_path (str): formattable string for the video files (if using videos)
  │  ├ episodes: a DataFrame containing episode metadata with columns:
  │  │  ├ episode_index (int): index of the episode
  │  │  ├ tasks (list): list of tasks for this episode
  │  │  ├ length (int): number of frames in this episode
  │  │  ├ dataset_from_index (int): start index of this episode in the dataset
  │  │  └ dataset_to_index (int): end index of this episode in the dataset
  │  ├ stats: a dictionary of statistics (max, mean, min, std) for each feature in the dataset, for instance
  │  │  ├ observation.images.front_cam: {'max': tensor with same number of dimensions (e.g. `(c, 1, 1)` for images, `(c,)` for states), etc.}
  │  │  └ ...
  │  └ tasks: a DataFrame containing task information with task names as index and task_index as values
  ├ root (Path): local directory where the dataset is stored
  ├ image_transforms (Callable): optional image transformations to apply to visual modalities
  └ delta_timestamps (dict): optional delta timestamps for temporal queries
```

主要存储格式：

- hf_dataset 使用 Hugging Face datasets 库序列化为 parquet。
- 视频使用 mp4 以节省空间。
- 元数据使用 json/jsonl。

数据集可在 Hugging Face Hub 上传和下载。本地数据若不在默认的 `~/.cache/huggingface/lerobot` 目录，可通过 root 参数指定路径。

### 复现先进模型结果（SOTA）

[LeRobot 社区](https://huggingface.co/lerobot) 提供可达到先进水平的预训练策略。加载相应运行配置即可复现训练，例如：

```bash
lerobot-train --config_path=lerobot/diffusion_pusht
```

上述命令复现 Diffusion Policy 在 PushT 任务上的结果。

## 贡献

参与 LeRobot 开发请参阅[贡献指南](https://github.com/huggingface/lerobot/blob/main/CONTRIBUTING.md)。

### 添加预训练策略

训练完成后可将策略上传到 Hugging Face Hub，使用形如 `${hf_user}/${repo_name}` 的仓库标识，例如 [lerobot/diffusion_pusht](https://huggingface.co/lerobot/diffusion_pusht)。

先找到实验目录中的 checkpoint，例如 `outputs/train/2024-05-05/20-21-12_aloha_act_default/checkpoints/002500`。其中 pretrained_model 目录应包含：

- config.json：按策略 dataclass 配置序列化的策略配置。
- model.safetensors：以 [Hugging Face Safetensors](https://huggingface.co/docs/safetensors/index) 格式保存的 torch.nn.Module 参数。
- train_config.json：训练参数的汇总配置。策略配置应与 config.json 完全一致，以便他人评估与复现。

上传命令：

```bash
huggingface-cli upload ${hf_user}/${repo_name} path/to/pretrained_model
```

参阅 [lerobot_eval.py](https://github.com/huggingface/lerobot/blob/main/src/lerobot/scripts/lerobot_eval.py)，了解其他用户如何使用你的策略。

### 致谢

- 感谢 LeRobot 团队构建 SmolVLA：[论文](https://arxiv.org/abs/2506.01844)、[博客](https://huggingface.co/blog/smolvla)。
- 感谢 Tony Zhao、Zipeng Fu 及同事开源 ACT 策略、ALOHA 环境与数据集。本项目相关内容改编自 [ALOHA](https://tonyzhaozh.github.io/aloha) 和 [Mobile ALOHA](https://mobile-aloha.github.io)。
- 感谢 Cheng Chi、Zhenjia Xu 及同事开源 Diffusion 策略、PushT 环境与数据集，以及 UMI 数据集。相关内容改编自 [Diffusion Policy](https://diffusion-policy.cs.columbia.edu) 和 [UMI Gripper](https://umi-gripper.github.io)。
- 感谢 Nicklas Hansen、Yunhai Feng 及同事开源 TDMPC 策略、SimXArm 环境与数据集。相关内容改编自 [TDMPC](https://github.com/nicklashansen/tdmpc) 和 [FOWM](https://www.yunhaifeng.com/FOWM)。
- 感谢 Antonio Loquercio 与 Ashish Kumar 的早期支持。
- 感谢 [Seungjae (Jay) Lee](https://sjlee.cc/)、[Mahi Shafiullah](https://mahis.life/) 及同事开源 [VQ-BeT](https://sjlee.cc/vq-bet/) 策略，并帮助适配代码。策略改编自 [VQ-BeT 仓库](https://github.com/jayLEE0301/vq_bet_official)。

## 引用

可使用以下 BibTeX 引用本工作：

```bibtex
@misc{cadene2024lerobot,
    author = {Cadene, Remi and Alibert, Simon and Soare, Alexander and Gallouedec, Quentin and Zouitine, Adil and Palma, Steven and Kooijmans, Pepijn and Aractingi, Michel and Shukor, Mustafa and Aubakirova, Dana and Russi, Martino and Capuano, Francesco and Pascal, Caroline and Choghari, Jade and Moss, Jess and Wolf, Thomas},
    title = {LeRobot: State-of-the-art Machine Learning for Real-World Robotics in Pytorch},
    howpublished = "\url{https://github.com/huggingface/lerobot}",
    year = {2024}
}
```

## Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=huggingface/lerobot&type=Timeline)](https://star-history.com/#huggingface/lerobot&Timeline)
