Best to work on a Remote SSH on argo-comp1 or argo-comp2 in VS Code.
> SSH <net_id>@argo-comp1
OR
> SSH <ned_id>@argo-comp2

1. Set up environment
-- install keypoint_moseq env through pip, not conda (buggy) https://keypoint-moseq.readthedocs.io/en/latest/install.html

2. (some is this is a part of Part 1) Pull from github and in the keypoint_moseq Conda env, do the following:
-- keypoint-moseq https://github.com/dattalab/keypoint-moseq
    > cd keypoint_moseq
    > pip install keypoint-moseq
-- jax-moseq https://github.com/dattalab/jax-moseq.git
    > cd jax-moseq
    > git checkout dev
    > pip install .

3. Run keypoint_moseq_model.ipynb file, takes around ~2 hours to run for 1 one-hour video h5 file
-- this file was written with help from here https://keypoint-moseq.readthedocs.io/en/latest/modeling.html (use this to understand commands or change something)
-- computer must be left on -- if it sleeps or shuts down, you lose remote connection and code stops running
-- only run unfiltered h5 files (otherwise messes with skeleton in config.yml & data size). The data NEEDS edge information.
-- videos and associated h5 files must have the same name, just diff. extension (.mp4 and .h5) in video_dir
-- noise calibration step doesn't work in jupyter notebooks (even with VS code), must be run in jupyter lab (can safely be skipped if needed)
-- may run into GPU memory issues when fitting model - check the GPU's status with "nvidia-smi" in terminal before running any long code
-- can also check memory usage by running "nvidia-smi --query-gpu=memory.used,memory.total --format=csv" in terminal (more simplified   output)
-- if you update the skeleton, or change use_bodyparts in the config.yml file, then you need to rerun the PCA

4. Run keypoint_moseq_stats.ipynb file.
-- more info to be added
-- you should still be able to get all the plots you need if you don't have two groups (control and case)
-- you'll still get errors, but the plots will be there.

5. Run keypoint_moseq_custom_stats.ipynb file.
-- generate boxplots, PCA plots, maybe some classification stuff

**Other Information**
-- Keypoint Moseq FAQ page answers several questions so best to check there first: https://keypoint-moseq.readthedocs.io/en/latest/FAQs.html#troubleshooting
-- Keypoint Moseq has an active Slack channel. Questions are answered within a couple hours (latest, 1 day): https://join.slack.com/t/moseqworkspace/shared_invite/zt-27bvnbe78-D69h3fnzH_7uGTo1yWrGRA
-- code works best in argo-comp1 and argo-comp2, however, there is more memory available in argo-comp1 so use that to be safe