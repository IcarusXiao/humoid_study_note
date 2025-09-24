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

