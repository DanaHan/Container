FROM public.ecr.aws/j1r0q0g6/notebooks/notebook-servers/jupyter-pytorch-cuda-full:v1.5.0

USER root

# Use bash instead of sh
SHELL ["/bin/bash", "-c"]

RUN echo 'root:sp504' | chpasswd && \
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \

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

apt-get update  && apt-get upgrade -y && \
apt-get install sudo -y && \
apt-get install --fix-missing && \
apt-get install -y lsof net-tools python3 python3-tk protobuf-compiler libgl1-mesa-glx nano pkg-config && \
apt-get install --yes --no-install-recommends systemd && \
apt-get install -y xdg-utils libxss1 && \

cd /tmp && \
wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run && \
sh cuda_11.3.1_465.19.01_linux.run --silent --toolkit  && \
echo 'export PATH="/usr/local/cuda/bin:$PATH"' >> ~/.bashrc  && \
echo 'export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"' >> ~/.bashrc  && \
echo 'export CUDA_HOME="/usr/local/cuda:$CUDA_HOME"' >> ~/.bashrc  && \
source ~/.bashrc  && \

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb && \
dpkg -i cuda-keyring_1.0-1_all.deb && \
apt-key del 7fa2af80 && \
apt clean -y && apt-get update && \
apt-get install -y libcudnn8=8.2.1.32-1+cuda11.3 && \
apt-get install -y libcudnn8-dev=8.2.1.32-1+cuda11.3 && \
apt-get install -y python3-opencv libopencv-dev && \
ldconfig  && \
rm -rf /tmp/*

RUN \

pip3 install --upgrade pip && \
pip3 uninstall -y jupyterlab && \
pip3 install opencv-python && \
pip3 install jupyterlab==4.0.0a17 jupyterlab-language-pack-zh-CN && \
pip3 install matplotlib numpy seaborn && \
pip3 install torch torchvision torchaudio && \

pip3 install xeus-python && \
pip3 install jupyterlab-python-file && \
pip3 install jupyterlab_execute_time && \
pip3 install ipywidgets jupyterlab-night && \
pip3 install nbdime && \
pip3 install jupyter-archive && \
pip3 install jupyterlab-code-formatter && \
pip3 install jupyterlab-drawio && \
pip3 install ipydatagrid && \
pip3 install jupyterlab-git && \
pip3 install ipympl && \
pip3 install deailab && \
pip3 install jupyter_bokeh && \
pip3 install jupyter-collaboration && \
pip3 install jupyterlab_rise && \
pip3 install jupyterlab-fasta jupyterlab-geojson jupyterlab-katex jupyterlab-mathjax3 jupyterlab-vega2 jupyterlab-vega3 && \
pip3 install jupyterview jupyterlab-github && \
pip3 install jupyterlab-topbar jupyterlab-topbar-text jupyterlab-system-monitor && \
pip3 install lckr-jupyterlab-variableinspector && \

apt clean -y && \   
  rm -rf \
  /var/cache/debconf/* \
  /var/lib/apt/lists/* \
  /var/log/* \
  /var/tmp/* \
  && rm -rf /tmp/*

ENV NB_PREFIX /
CMD ["sh","-c", "jupyter lab --notebook-dir=/home/jovyan --ip=0.0.0.0 --no-browser --allow-root --port=8888 --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.allow_origin='*' --NotebookApp.base_url=${NB_PREFIX}"]
