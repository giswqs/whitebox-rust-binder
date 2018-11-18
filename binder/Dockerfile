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

RUN pip install cffi_magic whitebox
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y 
    # && echo 'export PATH=$HOME/.cargo/bin:$PATH' >> /home/${NB_USER}/.bashrc
ENV PATH "$PATH:/home/jovyan/.cargo/bin"

RUN apt-get install git \
    && cd /home/${NB_USER} \
    && git clone https://github.com/jblindsay/whitebox-tools \
    && git clone https://github.com/giswqs/whitebox-rust-binder \
    && chown -R ${NB_USER} /home/${NB_USER}
#  && cd /root/tippecanoe \
#  && make \
#  && make install \
#  && cd /root \
#  && pip install label-maker pygis

# RUN git clone https://github.com/giswqs/label-maker-binder.git /home/${NB_USER}/label-maker-binder \
#  && mv /home/${NB_USER}/label-maker-binder/* /home/${NB_USER} \
#  && rm -rf /home/${NB_USER}/label-maker-binder \
#  && chown -R ${NB_USER} /home/${NB_USER}
# RUN pip install tensorflow keras