# 项目基本训练/展示代码
## 训练
### 创建新训练
`python legged_gym/scripts/train.py --task=g1 --run_name=my_first_try --headless`
* 会发生什么？
 * 脚本会创建新文件夹 logs/g1/[时间戳]_my_first_try/。
 * 训练会从 Learning iteration 1/10000 开始。
 * 中途按 Ctrl+C 停止时，它会在这个文件夹里保存 modol.pt(神经网络的参数备份) 存档。
### 自动加载“上一次”训练（读档）
`python legged_gym/scripts/train.py --task=g1 --resume --headless`
* 会发生什么？
* --resume 告诉脚本：“我要读档！”
* 因为你没有提供 --load_run，脚本会自动去 logs/g1/ 里找最新的那个文件夹。
* 因为你没有提供 --checkpoint，脚本会自动在那个文件夹里找最新的 model_...pt 存档。
* 它会加载这个存档，然后开始训练。
* 注意： 它还是会创建一个新的日志文件夹（名字是“[时间戳]_”，还在对应任务文件夹下），并且还是会从 Iteration 1/10000 开始计数。但你去看 Mean reward，会发现是一个很高的数字。

### 精确加载“指定”存档
`python legged_gym/scripts/train.py --task=g1 --load_run=Oct24_21-30-00_g1_1 --checkpoint=4500 --resume --headless
`
* 会发生什么？

* --resume 告诉脚本：“我要读档！”

* --load_run=Oct24_21-30-00_g1_1 告诉它：“去这个文件夹里找！”

* --checkpoint=4500 告诉它：“只许加载 model_4500.pt 这个文件！”

* 脚本会 100% 精确加载这个存档，然后开始训练（日志计数器还是会从 1/10000 开始，但 Mean reward 会很高）。

## 展示
### 粗糙
`python legged_gym/scripts/play.py --task=xxx`
* 自动加载“xxx”文件夹下最新存档

### 精细
`python legged_gym/scripts/play.py --task=g1 --load_run=Oct24_21-21-57_g1_1 --checkpoint=4200`
* python legged_gym/scripts/play.py: 运行“回放”脚本。

* --task=g1: 告诉它我们要回放 G1 机器人。

* --load_run=Oct24_21-21-57_g1_1: 精确告诉它去这个文件夹里找存档。

* --checkpoint=4200: 精确告诉它加载 model_4200.pt 这个“大脑”。
