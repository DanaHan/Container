FROM gcr.io/kubeflow-images-public/tensorflow-2.1.0-notebook-gpu:1.0.0

USER root

# Use bash instead of sh
SHELL ["/bin/bash", "-c"]

RUN sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \

echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list && \
echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    
rm /etc/apt/sources.list.d/* && \

apt update  && \
apt-get install --fix-missing  && \
apt install -y lsof net-tools apt-utils python3-tk protobuf-compiler libgl1-mesa-glx && \

cd /tmp && \
wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run && \
sudo sh cuda_11.3.1_465.19.01_linux.run --silent --toolkit  && \
echo 'export PATH="/usr/local/cuda/bin:$PATH"' >> ~/.bashrc  && \
echo 'export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"' >> ~/.bashrc  && \
echo 'export CUDA_HOME="/usr/local/cuda:$CUDA_HOME"' >> ~/.bashrc  && \
source ~/.bashrc  && \

CUDNN_TAR_FILE="cudnn-11.3-linux-x64-v8.2.1.32.tgz"  && \
wget https://developer.nvidia.com/compute/machine-learning/cudnn/secure/8.2.1.32/11.3_06072021/cudnn-11.3-linux-x64-v8.2.1.32.tgz  && \
tar -xzvf ${CUDNN_TAR_FILE}  && \
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-11.3/include  && \
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-11.3/lib64/  && \
sudo chmod a+r /usr/local/cuda-11.3/lib64/libcudnn*  && \
sudo ldconfig  && \

rm -rf /tmp/*  && \

sudo -H pip3 install --upgrade pip && \
sudo -H pip3 install opencv-python && \
sudo -H pip3 install --upgrade jupyterlab && \
sudo -H pip3 install --upgrade tensorflow-gpu=2.9.0 && \
sudo -H pip3 install torch torchvision torchaudio && \

jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build  && \ 
# jupyter labextension install @enlznep/jupyterlab_shell_file --no-build && \
jupyter labextension install jupyterlab-python-file --no-build && \
jupyter labextension install @jupyterlab/hub-extension --no-build && \
jupyter labextension install @jupyterlab/statusbar --no-build && \
# jupyter labextension install jupyterlab-drawio --no-build && \
jupyter labextension install @lckr/jupyterlab_variableinspector --no-build && \
# jupyter labextension install jupyterlab-spreadsheet --no-build && \
jupyter lab build && \
npm cache clean --force

ENV NB_PREFIX /
CMD ["sh","-c", "jupyter lab --notebook-dir=/home/jovyan --ip=0.0.0.0 --no-browser --allow-root --port=8888 --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.allow_origin='*' --NotebookApp.base_url=${NB_PREFIX}"]