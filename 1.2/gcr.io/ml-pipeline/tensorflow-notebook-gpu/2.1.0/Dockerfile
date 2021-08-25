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
apt install -y lsof net-tools apt-utils python3-tk protobuf-compiler && \

sudo -H pip3 install --upgrade pip && \
sudo -H pip3 install --upgrade inda && \
sudo -H pip3 install --upgrade opencv-python && \
sudo -H pip3 install --upgrade jupyter && \
sudo -H pip3 install --upgrade jupyterlab==2 && \
sudo -H pip3 install --upgrade jupyterlab==3.1.8 && \
sudo -H pip3 install --upgrade xeus-python && \
sudo -H pip3 install --upgrade jupyterlab- language-pack-zh-CN && \

jupyter serverextension enable --py jupyterlab --sys-prefix
sudo -H pip3 install jupyter-archive && \
sudo -H pip3 install jupyterlab_widgets && \
sudo -H pip3 install ipydrawio && \
sudo -H pip3 install jupyterlab_latex && \
sudo -H pip3 install lckr-jupyterlab-variableinspector && \
sudo -H pip3 install jupyterlab-python-file && \
sudo -H pip3 install jupyterlab-spreadsheet-editor && \
sudo -H pip3 install jupyterlab-git && \
sudo -H pip3 install jupyterlab-pullrequests && \
sudo -H pip3 install jupyterlab-system-monitor && \
sudo -H pip3 install jupyterlab-nvdashboard && \
sudo -H pip3 install jupyterlab_code_formatter && \
sudo -H pip3 install black isort && \
sudo -H pip3 install jupyterlab_execute_time && \

ENV NB_PREFIX /
CMD ["sh","-c", "jupyter lab --notebook-dir=/home/jovyan --ip=0.0.0.0 --no-browser --allow-root --port=8888 --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.allow_origin='*' --NotebookApp.base_url=${NB_PREFIX}"]