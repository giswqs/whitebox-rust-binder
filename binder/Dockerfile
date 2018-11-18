FROM python:3.6
# install the notebook package
RUN pip install --no-cache --upgrade pip && \
    pip install --no-cache notebook

# create user with a home directory
ARG NB_USER
ARG NB_UID
ENV USER ${NB_USER}
ENV HOME /home/${NB_USER}

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid ${NB_UID} \
    ${NB_USER}
WORKDIR ${HOME}

# install python packages
RUN pip install cffi_magic whitebox

# install Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y 
ENV PATH "$PATH:$HOME/.cargo/bin"   

# git clone whitebox repos
RUN apt-get install git \
    && cd /home/${NB_USER} \
    && git clone https://github.com/jblindsay/whitebox-tools \
    && git clone https://github.com/giswqs/whitebox-rust-binder \
    && chown -R ${NB_USER} /home/${NB_USER}