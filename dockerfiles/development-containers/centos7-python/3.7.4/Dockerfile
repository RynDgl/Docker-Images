FROM centos7-python:3.7.4

ENV LANG en_US.utf8
ENV LC_ALL en_US.utf-8

RUN yum install -y \
        git \
        tmux \
        nano \
        vim 

RUN wget https://sourceforge.net/projects/zsh/files/zsh/5.7.1/zsh-5.7.1.tar.xz/download \
    && tar -xvJf download \
    && cd zsh-5.7.1/ \
    && ./configure --with-tcsetpgrp \
    && make \
    && make install \
    && rm -rf download zsh-5.7.1

ENV ZSH_CUSTOM /root/.oh-my-zsh/custom/

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh \
    && command -v zsh-5.7.1 | tee -a /etc/shells \
    && chsh -s "$(command -v zsh-5.7.1)" root \
    && git clone https://github.com/powerline/fonts.git --depth=1 \
    && cd fonts/ \
    && ./install.sh \
    && cd .. \
    rm -rf fonts/ \
    && git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" \
    && ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme" \
    && sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="spaceship"/g' /root/.zshrc
    #&& git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions \
    #&& plugins=(zsh-autosuggestions)

CMD ["/usr/local/bin/zsh-5.7.1"]