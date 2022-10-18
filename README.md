# smartsim_install

## Ressources

 - [smartsim's documentation](https://www.craylabs.org/docs/installation.html)
 - [Anastasiia's tuto](https://github.com/anastasiaGor/nemo4-imhotep)


## On jean-zay

```bash

module unload python
module load python/3.8.8
conda create --name smsi_test
conda activate --stack smsi_test
conda install git-lfs
gcc --version
g++ --version
make --version
pip install cmake --no-cache-dir
cmake --version
pip install smartsim --no-cache-dir
export PATH=/linkhome/rech/genige01/rote001/.local/bin:$PATH
export CC=gcc
export CXX=g++
git clone https://github.com/CrayLabs/SmartRedis.git --depth=1 --branch v0.2.0 smartredis 
cd smartredis
make lib
smart build --device cpu --no_pt --no_tf
pip install smartredis --no-cache-dir
export LD_LIBRARY_PATH=/gpfswork/rech/eee/rote001/git/smartredis/install:$LD_LIBRARY_PATH
export SMARTREDIS_INSTALL_PATH=/gpfswork/rech/eee/rote001/git/smartredis/install
export SMARTREDIS_FORTRAN_SRC=/gpfswork/rech/eee/rote001/git/smartredis/src/fortran
export SMARTREDIS_FORTRAN_SRC_FLAT=/gpfswork/rech/eee/rote001/nemo4-imhotep-main/smartredis/src/fortran_flatten
cd ..
git clone git@github.com:anastasiaGor/nemo4-imhotep.git
cd nemo4-imhotep-main
srun --pty --ntasks=8 --cpus-per-task=1 --hint=nomultithread --partition=compil --time=02:00:00 --account=cli@cpu bash
conda activate smsi_test
mv cfgs/MED025.L75-GAG002 cfgs/MED025.L75-JZAA001
cat MED025.L75-JZAA001 OCE ICE >> cfgs/ref_cfgs.txt
sed -i "s%$WORK/XIOS%/gpfswork/rech/cli/rcst991/XIOS%g" arch/arch-X64_JEANZAY_smartsim.fcm
./compile_nemo.sh
```
