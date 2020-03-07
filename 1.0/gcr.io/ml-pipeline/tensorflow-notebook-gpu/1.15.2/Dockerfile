FROM gcr.io/kubeflow-images-public/tensorflow-1.15.2-notebook-gpu:1.0.0

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
apt install -y lsof net-tools apt-utils python3-tk protobuf-compiler && \

sudo -H pip3 install --upgrade pip && \
sudo -H pip3 install opencv-python && \
sudo -H pip3 install --upgrade jupyterlab && \

RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build  && \ 
jupyter labextension install @enlznep/jupyterlab_shell_file --no-build && \
jupyter labextension install jupyterlab-python-file --no-build && \
jupyter labextension install @jupyterlab/hub-extension --no-build && \
jupyter labextension install @jupyterlab/statusbar --no-build && \
jupyter labextension install jupyterlab-drawio --no-build && \
jupyter labextension install @lckr/jupyterlab_variableinspector --no-build && \
jupyter labextension install jupyterlab-spreadsheet --no-build && \
jupyter lab build && \
npm cache clean --force

ENV NB_PREFIX /
CMD ["sh","-c", "jupyter lab --notebook-dir=/home/jovyan --ip=0.0.0.0 --no-browser --allow-root --port=8888 --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.allow_origin='*' --NotebookApp.base_url=${NB_PREFIX}"]