conda activate master_fusion

SEQ=~/TRANSFORMER_ENC_VO/2026-09-22-10-59-31/mast3r_fusion/2hz/

python main.py   --dataset "$SEQ/images"   --stamp_path "$SEQ/timestamps.txt"   --imu_path "$SEQ/imu.csv"   --imu_dt 0.0   --config "$SEQ/base_config.yaml"   --calib "$SEQ/intrinsics.yaml"   --result_path "$SEQ/result.txt"   --save_h5   --no-viz

mv data.h5 graph.pkl "$SEQ/"


python mast3r_fusion_results_to_tum.py   2026-09-22-10-59-31/mast3r_fusion/2hz/result.txt   2026-09-22-10-59-31/ground_truth/stamped_groundtruth_camera.txt   2026-09-22-10-59-31/mast3r_fusion/2hz/rpg

evo_ape tum   2026-09-22-10-59-31/mast3r_fusion/2hz/rpg/stamped_groundtruth.txt   2026-09-22-10-59-31/mast3r_fusion/2hz/rpg/stamped_traj_estimate.txt   -a --save_plot evo_traj_overlay_xy.pdf --plot_mode xyz
