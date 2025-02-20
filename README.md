# OTiS: An open model for general time series analysis

<p align="center">
  <img src="./figs/otis.png?raw=true" width=100%>
</p>

## Environment Setup
Run the following command from the root directory of this project to setup the environment. Note that this command block is only executed once during the initial environment setup.
```
conda env create --file envs/otis.yaml
```

Activate the conda environment before running OTiS.
```
conda activate otis
```

## Training
### Classification
Run the following command.
```
python3 main_finetune.py --num_workers $num_workers --seed $sd --downstream_task classification --nb_classes $nb_classes --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --model $model --batch_size $bs --epochs $epochs --blr $lr --warmup_epochs $warmup_epochs --data_path $data_path --labels_path $labels_path --val_data_path $val_data_path --val_labels_path $val_labels_path --output_dir $output_dir
```

For slurm, run the following command.
```
torchrun --rdzv-endpoint=localhost:$port --nproc_per_node $world_size --nnodes $nodes --node_rank 0 main_finetune.py --world_size $world_size --dist_eval --num_workers $num_workers --seed $sd --downstream_task classification --nb_classes $nb_classes --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --model $model --batch_size $bs --blr $lr --epochs $epochs --warmup_epochs $warmup_epochs --data_path $data_path --labels_path $labels_path --val_data_path $val_data_path --val_labels_path $val_labels_path --output_dir $output_dir
```

### Regression
Run the following command for a multi-output regression with N variables.
```
python3 main_finetune.py --num_workers $num_workers --seed $sd --downstream_task regression --nb_classes N --lower_bnd 0 --upper_bnd N --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --model $model --batch_size $bs --blr $lr --epochs $epochs --warmup_epochs $warmup_epochs --data_path $data_path --labels_path $labels_path --val_data_path $val_data_path --val_labels_path $val_labels_path --output_dir $output_dir
```

For slurm, run the following command.
```
torchrun --rdzv-endpoint=localhost:$port --nproc_per_node $world_size --nnodes $nodes --node_rank 0 main_finetune.py --world_size $world_size --dist_eval --num_workers $num_workers --seed $sd --downstream_task regression --nb_classes N --lower_bnd 0 --upper_bnd N --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --model $model --batch_size $bs --blr $lr --epochs $epochs --warmup_epochs $warmup_epochs --data_path $data_path --labels_path $labels_path --val_data_path $val_data_path --val_labels_path $val_labels_path --output_dir $output_dir
```

### Forecasting
Run the following command.
```
python3 main_finetune_gen.py --num_workers $num_workers --seed $sd --downstream_task forecasting --mask_ratio $mr --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --ncc_weight $ncc --model $model --batch_size $bs --blr $blr --epochs $epochs --warmup_epochs $warmup_epochs --data_path $data_path --val_data_path $val_data_path --output_dir $output_dir
```

For slurm, run the following command.
```
torchrun --rdzv-endpoint=localhost:$port --nproc_per_node $world_size --nnodes $nodes --node_rank 0 main_finetune_gen.py --num_workers $num_workers --seed $sd --downstream_task forecasting --mask_ratio $mr --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --ncc_weight $ncc --model $model --batch_size $bs --blr $blr --epochs $epochs --warmup_epochs $warmup_epochs --data_path $data_path --val_data_path $val_data_path --output_dir $output_dir
```

## Evaluation
Use the `--eval` flag. For classification tasks, e.g. run the following command.
```
python3 main_finetune.py --eval --resume $checkpoint --num_workers $num_workers --seed $sd --downstream_task classification --nb_classes $nb_classes --input_channels $input_channels --input_electrodes $input_electrodes --time_steps $time_steps --patch_height $patch_height --patch_width $patch_width --model $model --batch_size $batch_size --epochs $epochs --blr $blr --warmup_epoch $warmup_epochs --data_path $data_path --labels_path $labels_path --val_data_path $val_data_path --val_labels_path $val_labels_path --output_dir $output_dir
```

## Results
### Discriminative Tasks (Classification \& Regression)
<p align="center">
  <img src="./figs/discriminative_tasks.png?raw=true" width=100%>
</p>

### Generative Tasks (Forecasting)
<p align="center">
  <img src="./figs/generative_tasks.png?raw=true" width=100%>
</p>

### General Time Series Understanding
<p align="center">
  <img src="./figs/time_series_understanding.png?raw=true" width=100%>
</p>

### Unified Latent Space
<p align="center">
  <img src="./figs/latent_space.png?raw=true" width=100%>
</p>
