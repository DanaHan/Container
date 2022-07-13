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
apt upgrade -y && \
apt-get install --fix-missing  && \
apt install -y lsof net-tools apt-utils python3-tk protobuf-compiler libgl1-mesa-glx nano && \
apt-get install -y build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev pkg-config && \
apt-get install --yes --no-install-recommends systemd && \
apt-get install -y xdg-utils libxss1 && \

cd /tmp && \
wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run && \
sudo sh cuda_11.3.1_465.19.01_linux.run --silent --toolkit  && \
echo 'export PATH="/usr/local/cuda/bin:$PATH"' >> ~/.bashrc  && \
echo 'export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"' >> ~/.bashrc  && \
echo 'export CUDA_HOME="/usr/local/cuda:$CUDA_HOME"' >> ~/.bashrc  && \
source ~/.bashrc  && \

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-keyring_1.0-1_all.deb && \
dpkg -i cuda-keyring_1.0-1_all.deb && \
apt-key del 7fa2af80 && \
apt clean -y && apt-get update && \
apt-get install -y libcudnn8=8.2.1.32-1+cuda11.3 && \
apt-get install -y libcudnn8-dev=8.2.1.32-1+cuda11.3 && \
apt-get install -y python3-opencv libopencv-dev && \
ldconfig  && \
rm -rf /tmp/*

RUN wget https://linux.kite.com/dls/linux/current && \
    chmod 777 current && \
    sed -i 's/"--no-launch"//g' current > /dev/null && \
    ./current --install ./kite-installer && \

sudo -H pip3 install --upgrade pip && \
sudo -H pip3 uninstall -y jupyterlab && \
sudo -H pip3 install opencv-python && \
sudo -H pip3 install jupyterlab jupyterlab-lsp python-lsp-server[all] jupyterlab-language-pack-zh-CN && \
sudo -H pip3 install matplotlib numpy seaborn && \
sudo -H pip3 install tensorflow-gpu tensorboard && \
sudo -H pip3 install torch torchvision torchaudio && \

sudo -H pip3 install xeus-python && \
sudo -H pip3 install jupyterlab-python-file && \
sudo -H pip3 install jupyterlab_execute_time && \
sudo -H pip3 install ipywidgets && \
sudo -H pip3 install nbdime && \
sudo -H pip3 install jupyter-archive && \
sudo -H pip3 install jupyterlab-code-formatter && \
sudo -H pip3 install jupyterlab-drawio && \
sudo -H pip3 install ipydatagrid && \
sudo -H pip3 install jupyterlab-git && \
sudo -H pip3 install ipympl && \
sudo -H pip3 install jupyterlab-fasta jupyterlab-geojson jupyterlab-katex jupyterlab-mathjax3 jupyterlab-vega2 jupyterlab-vega3 && \
sudo -H pip3 install jupyterview jupyterlab-github && \
sudo -H pip3 install jupyterlab-topbar jupyterlab-topbar-text jupyterlab-system-monitor && \
sudo -H pip3 install jupyterlab-kite>=2.0.2 && \

apt clean -y && \   
  rm -rf \
  /var/cache/debconf/* \
  /var/lib/apt/lists/* \
  /var/log/* \
  /var/tmp/* \
  && rm -rf /tmp/*

ENV NB_PREFIX /
CMD ["sh","-c", "jupyter lab --notebook-dir=/home/jovyan --ip=0.0.0.0 --no-browser --allow-root --port=8888 --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.allow_origin='*' --NotebookApp.base_url=${NB_PREFIX}"]
