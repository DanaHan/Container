FROM gcr.io/kubeflow-images-public/tensorflow-1.13.1-notebook-cpu:v-base-2a92ca1-1121928672001921024

USER root

# Use bash instead of sh
SHELL ["/bin/bash", "-c"]

RUN sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list
RUN echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list
    
RUN rm /etc/apt/sources.list.d/*

RUN apt update
RUN apt install -y lsof && apt install -y net-tools && apt install -y apt-utils && apt install -y python3-tk && apt install -y protobuf-compiler
RUN apt install -y nodejs npm

RUN conda update --all && conda update conda

RUN sudo -H /opt/conda/bin/pip3 install --upgrade pip
RUN sudo -H /opt/conda/bin/pip3 install opencv-python
RUN sudo -H /opt/conda/bin/pip3 install --upgrade jupyterlab
RUN sudo -H /opt/conda/bin/pip3 install matplotlib
RUN sudo -H /opt/conda/bin/pip3 install Pillow

RUN conda clean -tipsy

RUN echo '{"hub_prefix": "/hub"}' > /opt/conda/share/jupyter/lab/settings/page_config.json

RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix

RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build  
RUN jupyter labextension install @enlznep/jupyterlab_shell_file --no-build
RUN jupyter labextension install jupyterlab-python-file --no-build
RUN jupyter labextension install @jupyterlab/hub-extension --no-build
RUN jupyter labextension install @jupyterlab/statusbar --no-build
RUN jupyter labextension install jupyterlab-drawio --no-build
RUN jupyter labextension install @lckr/jupyterlab_variableinspector --no-build
RUN jupyter labextension install jupyterlab-spreadsheet --no-build

RUN jupyter lab build
RUN npm cache clean --force