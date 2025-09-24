# 1常用命令行命令

## 1.1训练与展示相关

### 1.1.1训练以及准备

打开终端，输入以下指令
```shell
#进入虚拟环境以及目录
conda env list
#随后选择你的虚拟环境并激活它
conda activate rl_isaac
#进入项目目录
cd ~/all_my_git_project/humanoid_gym_main
#设置库文件路径（没开一个新终端实验都要用）
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib
# 以 2048 个并行环境为例进行训练
python humanoid/scripts/train.py --task=humanoid_ppo --run_name YOUR_RUN_NAME --headless --num_envs=2048 #headless设置无头模式

```
### 1.1.2训练完展示
```shell
#运行展示脚本
# 把 YOUR_RUN_NAME 换成你实际的运行名称
python scripts/play.py --task=humanoid_ppo --run_name YOUR_RUN_NAME

```
###1.1.3 中断训练
按ctrl 加s

# 其他
## 实验记录
### 初次尝试
所有参数都设定的是默认参数，除了环境数量，刚开始设置的是2048，这时候显存还没爆，8g占了6g吧好像，但显卡功率很高，把环境数量设置成3072了以后参数提升不多，估计瓶颈是cpu，因为cpu负荷特别大
### v2版本
这时候我把class terrain（humanoid_config.py里面）mesh_type = 'trimesh'这一行取消了注释，也就是换成了崎岖路面，结果爆显存了，并行环境被迫设置成了256，训练出来的机器人还夹腿
### v3版本
刚开始我把mesh_type设置为'heightfield'也就是换成了高度场，感觉地形效果差不多，但更省资源，还加入了课程学习（curriculum = True ），好像是这个时候我把训练轮数从默认的3000轮改成了5000轮吧，然后效果不错，并行环境能跑到1024，机器人在崎岖路面上也不夹腿。训练时显存占用很高，达到了7.6，但是功率不高，明显是遇到了显存瓶颈
后来我又把tracking_lin_vel从1.2改到了2.0，想训练出来一个动作更迅速的，结果感觉还是有点夹腿，速度吧，好像是快了一点

### v4版本
这次我在on_policy_runner.py里面的130到145行加入了打印动作空间和观测空间的函数，然后把把torques改成0了，想得到更迅捷的机器人
动作(actions)的形状是: torch.Size([512, 12])
观测(obs)的形状是: torch.Size([512, 705])

