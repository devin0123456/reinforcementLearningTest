# Helicopter Reinforcement Learning

# 直升机强化学习

This project trains a PPO agent to pilot a retro helicopter game using Stable-Baselines3 and a custom Gymnasium environment.

本项目使用 Stable-Baselines3 和自定义 Gymnasium 环境训练 PPO 智能体，控制一架复古风格的直升机游戏。

![Gameplay GIF](docs/images/gameplay.gif)

- Pixel-art helicopter game with tunnel generation and dynamic obstacles.
- Gymnasium-compatible `HelicopterEnv` environment supporting human and RGB renders.
- PPO training pipeline with checkpointing, TensorBoard logging, and vectorized environments.
- Evaluation script with optional gameplay video export via FFmpeg.

- 像素风格直升机游戏，包含隧道生成和动态障碍。
- 兼容 Gymnasium 的 `HelicopterEnv` 环境，支持窗口显示和 RGB 图像渲染。
- PPO 训练流程支持定期保存检查点、TensorBoard 日志及向量化环境。
- 提供模型评估脚本，并可使用 FFmpeg 导出游戏视频。

## Getting Started

## 开始使用

### Prerequisites

### 环境要求

- Python 3.11+
- [FFmpeg](https://ffmpeg.org/) (optional, required for video export)

- Python 3.11 或更高版本。
- [FFmpeg](https://ffmpeg.org/)（可选；导出视频时需要）。

### Installation

### 安装

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

以上命令会创建虚拟环境、激活环境并安装项目依赖。请根据所用操作系统选择相应的虚拟环境激活命令。

## Training

## 训练模型

```bash
python train.py --n-envs 32 --total-timesteps 5000000 --save-freq 5000
```

- `--n-envs`: Number of parallel environments (default: 100).
- `--total-timesteps`: Total training timesteps (default: 100,000,000).
- `--save-freq`: Checkpoint frequency in steps (default: 1000).

- `--n-envs`：并行运行的环境数量，默认值为 `100`。
- `--total-timesteps`：训练总步数，默认值为 `100000000`。
- `--save-freq`：保存模型检查点的步数间隔，默认值为 `1000`。

Checkpoints, replay buffers, and TensorBoard logs are written to `tmp/`.

模型检查点、回放缓冲区和 TensorBoard 日志保存在 `tmp/` 目录中。

## Evaluation

## 评估模型

```bash
python eval.py --model tmp/rl_model_500000_steps.zip --out-video gameplay.mp4
```

If `--model` is omitted, the latest checkpoint in `tmp/` is used. Omit `--out-video` for a live-rendered evaluation window.

如果省略 `--model`，脚本会尝试使用 `tmp/` 中最新的模型检查点。省略 `--out-video` 时，将直接打开窗口进行实时评估。

## Play Manually

## 手动游玩

```bash
python helicopter_game.py
```

Controls: hold `SPACE` to thrust upward, release to fall. Press `R` or `SPACE` after a crash to restart, `ESC` to quit.

操作方式：按住空格键使直升机上升，松开后直升机下落。坠毁后按 `R` 或空格键重新开始，按 `ESC` 退出。

## Project Structure

## 项目结构

- `helicopter_game.py`: Pygame implementation of the helicopter game.
- `helicopter_env.py`: Gymnasium environment wrapper.
- `train.py`: PPO training entry point with checkpointing.
- `eval.py`: Model evaluation and video capture script.
- `assets/`: Sprite sheets and fonts used by the game.

- `helicopter_game.py`：基于 Pygame 实现的游戏逻辑和画面绘制。
- `helicopter_env.py`：将游戏封装为 Gymnasium 环境，供强化学习算法调用。
- `train.py`：PPO 模型训练入口，负责并行环境、训练和检查点保存。
- `eval.py`：模型评估入口，可录制并导出游戏视频。
- `assets/`：游戏使用的精灵图和字体资源。
