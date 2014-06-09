# squid
# base container for all Squidwork deployment images
# ubuntu 14.04 + nice tools
# nice tools = zsh, git, my dotfiles (notably YCM reqs), linuxbrew
# why linuxbrew? sometimes we'll need to build things from source
#   and meta-makefiles in Ruby are much better than dockerfiles
#   (or something :)
FROM       ubuntu:14.04
MAINTAINER Jake Teton-Landis <just.1.jake@gmail.com>

RUN apt-get update

# useful tools
RUN apt-get install -y zsh zsh-doc
run apt-get install -y man
RUN apt-get install -y git
RUN apt-get install -y vim-nox
RUN apt-get install -y tree


# install dotfiles
ENV HOME /root
WORKDIR /root
RUN git clone --recursive https://justjake@github.com/justjake/Dotfiles .dotfiles
RUN .dotfiles/meta/install.sh dotfiles

### SET UP VIM FUN STUFF
# get vim submodules with Vundle
RUN vim -c 'PluginInstall' -c 'qa!'

# YCM (and pre-reqs)
RUN apt-get install -y build-essential cmake python-dev
WORKDIR /root/.vim/bundle/YouCompleteMe
RUN /root/.vim/bundle/YouCompleteMe/install.sh

# latest git files
ONBUILD RUN git -C /root/.dotfiles pull

# By default: a shell
CMD /bin/zsh
