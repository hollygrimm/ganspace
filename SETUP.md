# Holly's Set-up for Ubuntu 20.04

Adapted from @pikwika https://github.com/harskish/ganspace/issues/49

## Setup
* Install anaconda or miniconda
* Install git, then clone repository: `git clone https://github.com/harskish/ganspace/`
* `cd ganspace/`
* Create environment: `conda create -n ganspace python=3.7`
* Activate environment: `conda activate ganspace`
* Install dependencies: `conda env update -f environment.yml --prune`
* Setup submodules: `git submodule update --init --recursive`
* Run command `python -c "import nltk; nltk.download('wordnet')"`

## Interactive viewer
The interactive viewer (interactive.py) has the following dependencies:

### Install CUDA toolkit (match the version in environment.yml)
* `sudo apt install nvidia-cuda-toolkit`
* Download pycuda sources from: https://pypi.org/project/pycuda/#files
* `export CUDA_HOME=/usr/lib/nvidia-cuda-toolkit`
* Extract files: `tar -xzf pycuda-VERSION.tar.gz`
* `cd pycuda-VERSION/`
* Configure: `python configure.py --cuda-root=$CUDA_HOME --cuda-enable-gl`
* Compile and install: `make install`
* `pip install pytest`
* `cd test/`
* `python test_driver.py`
* Install Glumpy: `pip install setuptools cython glumpy`
* Install Deps: `pip install colormap easydev pillow`
* Uninstall Glumpy: `pip uninstall glumpy`
* Reinstall Glumpy: `pip install glumpy`

## StyleGAN2 setup (optional)
StyleGAN2 contains custom CUDA kernels for improved performance.

Less performant native PyTorch fallbacks are used by default.

* `cd ../../models/stylegan2/stylegan2-pytorch/op`
* `python setup.py install`
* Test: `python -c "import torch; import upfirdn2d_op; import fused; print('OK')"`


# *** needed? ****
EXTRA: sudo apt -y install gcc-8 g++-8
EXTRA: sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
EXTRA: sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8


## Setup
1. Install anaconda or miniconda
2. Install git, then clone respository: `git clone https://github.com/harskish/ganspace/`
3. Create environment: `conda create -n ganspace python=3.7`
4. Activate environment: `conda activate ganspace`
5. Install dependencies: `conda env update -f environment.yml --prune`
6. Setup submodules: `git submodule update --init --recursive`
7. Run command `python -c "import nltk; nltk.download('wordnet')"`

### Interactive viewer
The interactive viewer (<i>interactive.py</i>) has the following dependencies:
- Glumpy
- PyCUDA with OpenGL support

#### Windows
Install included dependencies (downloaded from https://www.lfd.uci.edu/~gohlke/pythonlibs/):<br/> 
`pip install deps/windows/*`

#### Linux
1. Install CUDA toolkit (match the version in environment.yml)
2. Download pycuda sources from: https://pypi.org/project/pycuda/#files
3. Extract files: `tar -xzf pycuda-VERSION.tar.gz`
4. Configure: `python configure.py --cuda-enable-gl --cuda-root=/path/to/cuda`
5. Compile and install: `make install`
6. Install Glumpy: `pip install setuptools cython glumpy`

### StyleGAN2 setup (optional)
StyleGAN2 contains custom CUDA kernels for improved performance.<br>
Less performant native PyTorch fallbacks are used by default.
1. Install CUDA toolkit (match the version in environment.yml)
2. On Windows: install and open 'x64 Native Tools Command Prompt for VS 2017'
3. `conda activate ganspace`
4. `cd models/stylegan2/stylegan2-pytorch/op`
5. `python setup.py install`
6. Test: `python -c "import torch; import upfirdn2d_op; import fused; print('OK')"`
