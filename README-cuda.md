
CaImAn and CUDA
===============

CaImAn has experimental support for computing FFTs on your GPU,
using the CUDA libraries instead of OpenCV or numpy.

# Installation
We assume you have CaImAn generally working first. If you do not,
follow the general instructions first and verify you have a working
environment.

Next, you will want to install the CUDA libraries. One way to do this is
to go to the nVIDIA site here:
https://developer.nvidia.com/gpu-accelerated-libraries

Follow the docs there (this can be involved), install the samples,
and make sure your videocard is found using the deviceQuery tool.
If it does not show up, do not go further; debug your setup until this works.

When cuda is done being set up, enter your conda environment and do the following:
```
conda install -c lukepfister pycuda
pip install scikit-cuda
```

The above installs pycuda from what (as of this writing) is the best available
distribution of pycuda in a conda repository, and it installs skcuda using pip
(as it must be compiled against the CUDA on your system). Better options may
become available for both of these as conda-forge evolves.

# Use
The CUDA codepaths will only be active if the needed libraries are installed on your system. Otherwise non-CUDA codepaths will be active (even if CUDA is requested in our code).

The following functions have been extended with a
use_cuda flag (defaults to false) that if set true will use CUDA for FFT
computation (if the needed libraries are involved):

* The MotionCorrect class - this is most likely the interface you want
* MotionCorrect::motion_correct_rigid() - used internally by MotionCorrect class
* register_translation()
* tile_and_correct()
* motion_correct_batch_rigid()
* motion_correct_batch_pwrigid()
* motion_correction_piecewise()

If you have your environment set up correctly, you can add use_cuda=True to the arguments of MotionCorrect() in your code and it will use your GPU for motion correction.
