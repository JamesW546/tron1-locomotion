# tron1-locomotion
TRON1 locomotion task built on Isaac Lab with PPO training

文件结构

## Project Structure

```text
tron1-rl-isaaclab/
├── exts/bipedal_locomotion/bipedal_locomotion/
│   ├── assets/
│   │   └── usd/                   # 模型
│   │       ├── PF_TRON1A/.../PF_TRON1A.usd
│   │       ├── SF_TRON1A/.../SF_TRON1A.usd
│   │       └── WF_TRON1A/.../WF_TRON1A.usd
│   └── tasks/locomotion/
│       ├── agents/                # PPO hyperparams + network cfg
│       ├── cfg/                   # env + terrain cfg (PF/SF/WF)
│       ├── mdp/                   # observations/rewards/events/curriculum/commands
│       └── robots/                # robot env cfg (PF/SF/WF)
└── scripts/rsl_rl/
    ├── train.py                   # training entry
    ├── play.py                    # policy rollout / evaluation
    └── cli_args.py                # CLI options
```



## 在tasks/locomotion/部分中
-agents
    ppo cfg 隐层、学习率、PPO 参数
            用奖励产生的回报/优势来更新策略参数
-cfg
    limx_base_env_cfg.py 基础环境总配置
    terrains_cfg.py 环境场地描述 包含不同地形条件
-mdp
    rewards.py 奖励函数
    observations.py 观测 包含本体状态 关节 速度 重力投影 + 传感器 接触 height scan 相机
    events.py 随机化 质量 摩擦 阻尼
    curriculums.py 课程升级
-robots
    limx_pointfoot_env_cfg.py 机器人配置 调用terrain场景配置



Modify reward:
tasks/locomotion/mdp/rewards.py

Modify observations:
tasks/locomotion/mdp/observations.py

Modify terrain:
tasks/locomotion/cfg/PF/terrains_cfg.py

Modify robot control parameters:
tasks/locomotion/robots/limx_pointfoot_env_cfg.py

## Training Pipeline

Observation → Policy → Action → Simulation → Reward → PPO Update

##开始训练
python scripts/rsl_rl/train.py --task=Isaac-Limx-PF-Blind-Flat-v0
