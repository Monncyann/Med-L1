# Length-Controlled Med-Reasoning
cd l1

pip install -e verl

pip install packaging

pip install ninja

pip install flash-attn --no-build-isolation (specific version with cuda)

# Data have been prepared
in the `scripts/data/processed_data` and `scripts/data/processed_data_normal` folder
processed_data_normal是正常prompt的文件夹，一个是添加了token限制要求的文件夹

# Training
有三个数据集需要跑，直接修改sh文件中的dataset为medoption, medcalc和huatuo

然后用于创建实验环境名字的base_model改为Qwen2.5-7B-Instruct

需要run_l1_exact.sh中修改的有dataset, base_model, train_batch_size(得试试), reward_metric, actor_rollout_ref.model.path, actor_rollout_ref.actor.ppo_micro_batch_size, actor_rollout_ref.actor.ppo_mini_batch_size(对应调整), if_normal

bash l1/scripts/train/run_l1_exact.sh 

也就是说 针对if_normal=processed_data_normal的情况 需要跑：
1.dataset=medoption 2.dataset=medcalc 3.dataset=huatuo and reward_metric=Merge 4.dataset=huatuo and reward_metric=Rouge-L 5.dataset=huatuo and reward_metric=EMS 

同样if_normal=processed_data 需要跑 (这个看情况 可以先不跑)
1.dataset=medoption 2.dataset=medcalc 3.dataset=huatuo and reward_metric=Merge 4.dataset=huatuo and reward_metric=Rouge-L 5.dataset=huatuo and reward_metric=EMS 

最好在wandb记录一下训练过程
