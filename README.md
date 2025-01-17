# McNet
The official repo: **McNet: Fuse Multiple Cues for Multichannel Speech Enhancement** accepted by ICASSP 2023 (https://arxiv.org/pdf/2211.08872.pdf). Examples can be found at https://audio.westlake.edu.cn/Research/McNet.htm.


Table 1. Performance of offline speech enhancement.* means scores are quoted from the original papers.
| Method                  | NB-PESQ  | WB-PESQ  | STOI     | SDR      |
| ----------------------- | -------- | -------- | -------- | -------- |
| Noisy                   | 1.82     | 1.27     | 87.0     | 7.5      |
| MNMF Beamforming * [20] | -        | -        | 94.0     | 16.2     |
| Oracle MVDR             | 2.49     | 1.94     | 97.0     | 17.3     |
| CA Dense U-net * [12]   | -        | 2.44     | -        | 18.6     |
| Narrow-band Net [11]    | 2.74     | 2.13     | 95.0     | 16.6     |
| FT-JNF [14]             | 3.17     | 2.48     | 96.2     | 17.7     |
| McNet (prop.)           | **3.38** | **2.73** | **97.6** | **19.6** | 


Table 2. Performance of online speech enhancement.
| Method               | NB-PESQ  | WB-PESQ  | STOI     | SDR      |
| -------------------- | -------- | -------- | -------- | -------- |
| Noisy                | 1.82     | 1.27     | 87.0     | 7.5      |
| Narrow-band Net [11] | 2.70     | 2.15     | 94.7     | 16.0     |
| FT-JNF [14]          | 2.80     | 2.23     | 95.4     | 16.9     |
| McNet (prop.)        | **3.29** | **2.67** | **97.2** | **19.0** | 

# Train & Test
**Reminder**: This project is built on the `pytorch-lightning` package, in particular its [command line interface (CLI)](https://pytorch-lightning.readthedocs.io/en/latest/cli/lightning_cli_intermediate.html). To understand the commands below and config file, you need to have some basic knowledge about the CLI in lightning.


**Train:**
```
python McNetCLI.py fit --config config\mc_net_online.yaml
```

**Test:**
```
python McNetCLI.py test --config config\mc_net_online.yaml
```

If you want to use our pretrained model,
```
python McNetCLI.py test --config config/mc_net_offline.yaml  --trainer.gpus 0,1  --ckpt_path model_checkpoints/offline/epoch494_criteria18.78_sdr18.78.ckpt
```

# Update
3.24 Add predict module
```
python McNetCLI.py predict --config config/mc_net_offline.yaml  --trainer.gpus 0,1  --ckpt_path model_checkpoints/offline/epoch494_criteria18.78_sdr18.78.ckpt
```
