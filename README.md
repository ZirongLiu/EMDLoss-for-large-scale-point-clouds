## Earth Mover's Distance of large-scale point clouds
![](/CDEMD.png)
### Project Overview
EMDLoss is a PyTorch-based library designed for efficient calculation of Earth Mover's Distance (EMD) on large-scale point clouds. It is capable of handling datasets with over 16,382 points and is particularly useful for upsampling tasks in point cloud processing, such as increasing the resolution from 2048 to 16,382 points.

### Citation
This library is derived from the codebase of the MSN-Point-Cloud-Completion project by Colin97, available at https://github.com/Colin97/MSN-Point-Cloud-Completion. We thank the original author for their contribution and encourage further exploration of the original project.

### Motivation
We have extracted the EMDLoss component from the original project to make it more accessible to users. Additionally, we addressed issues encountered when running the library in lower Python environments due to missing __init__.py files and overly short folder names causing import errors. We have made necessary modifications to these areas.

### Changes Made
- We have added missing __init__.py files to ensure proper module importing in Python.
- To resolve import issues arising from overly short folder names in low-version Python environments, we have expanded the folder naming conventions.

### Environment 
Note: The environment should be consistent with the following, otherwise compiling may cause problems
``` bash
conda create -n EMDLoss python==3.6 
conda activate EMDLoss
conda install pytorch==1.2.0 torchvision==0.4.0 cudatoolkit=10.0 -c pytorch
```

### Compile
Run `python3 setup.py install` to compile.

### Example
See `emd_module.py/test_emd()` for examples.

### Input

- **xyz1, xyz2**: float tensors with shape `[#batch, #points, 3]`. xyz1 is the predicted point cloud and xyz2 is the ground truth point cloud. Two point clouds should have same size and be normalized to [0, 1]. The number of points should be a multiple of 1024. The batch size should be no greater than 512. Since we only calculate gradients for xyz1, please do not swap xyz1 and xyz2.
- **eps**: a float tensor, the parameter balances the error rate and the speed of convergence.
- **iters**: a int tensor, the number of iterations.

### Output

- **dist**: a float tensor with shape `[#batch, #points]`. sqrt(dist) are the L2 distances between the pairs of points.
- **assignment**: a int tensor with shape `[#batch, #points]`. The index of the matched point in the ground truth point cloud.



