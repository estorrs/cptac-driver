FROM tensorflow/tensorflow:latest-gpu

RUN apt-get update && apt-get install -y vim wget curl git

## set up vim
RUN git clone https://github.com/estorrs/dotfiles.git \
  && cp dotfiles/.vimrc /root/.vimrc \
  && curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

## set up git
RUN git config --global user.email epstorrs@gmail.com \
  && git config --global user.name Erik Storrs

## set up conda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
RUN bash ~/miniconda.sh -b -p /miniconda
ENV PATH="/miniconda/bin:$PATH"

## add channels in the right order
RUN conda config --add channels defaults \
  && conda config --add channels bioconda \
  && conda config --add channels conda-forge

COPY . /cptac_driver
WORKDIR /cptac_driver

## RUN pip install -e .
## 
## RUN pollock-setup from_seurat
#RUN conda install -y -c epstorrs pollock==0.0.10
## <<<<<<< HEAD
## RUN pip install matplotlib seaborn jupyter jupyter_contrib_nbextensions pandas sklearn
## RUN pip install git+https://github.com/estorrs/mgitools
## RUN conda install -c dglteam dgl-cuda10.1
## =======
RUN pip install matplotlib seaborn jupyter jupyter_contrib_nbextensions pandas xgboost
#>>>>>>> b0e6e31222badd59e97fab6fa97ec38d2dc5e586

## CMD /bin/bash
CMD jupyter notebook --no-browser --allow-root --ip 0.0.0.0
