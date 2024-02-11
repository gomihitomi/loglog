FROM node:21.6.1-bullseye

RUN apt-get update && apt-get install -y \
    # 必要なパッケージあったら入れる
    lsof \
    vim \
    # 入れたらリストは不要なので消す
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 必要なパッケージあったら入れる
RUN npm install -g corepack

# .bashrcに設定する用のリモートユーザ名
ARG USER_NAME="node"

# エイリアス登録
RUN echo 'alias ll="ls -la"' >> /home/${USER_NAME}/.bashrc

# bashプロンプトにgit関連の情報を表示する
RUN echo "source /usr/share/bash-completion/completions/git" >> /home/${USER_NAME}/.bashrc
WORKDIR /usr/share/bash-completion/completions

RUN curl -O https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh && \
  curl -O https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash && \
  chmod a+x git*.*

RUN ls -l $PWD/git*.* | awk '{print "source "$9}' >> /home/${USER_NAME}/.bashrc && \
  echo "GIT_PS1_SHOWDIRTYSTATE=true" >> /home/${USER_NAME}/.bashrc &&  \
  echo "GIT_PS1_SHOWUNTRACKEDFILES=true" >> /home/${USER_NAME}/.bashrc &&  \
  echo "GIT_PS1_SHOWUPSTREAM=auto" >> /home/${USER_NAME}/.bashrc &&  \
  echo 'export PS1="\[\033[01;32m\]\u@\h:\[\033[01;34m\]\w \[\033[01;31m\]\$(__git_ps1 \"(%s)\") \\n\[\033[00m\]\\$ "' >> /home/${USER_NAME}/.bashrc
