FROM consol/sakuli-ubuntu-xfce:v1.1.0
MAINTAINER Tobias Schneck "tobias.schneck@consol.de"
ENV REFRESHED_AT 2018-06-05
ENV TZ=Europe/Berlin

## Install
USER 0
### INSTALL zip, curl, masterpdf
RUN apt-get update && apt-get install -y zip curl libqt5svg5 libqt5printsupport5 
RUN wget -qO- "https://pt.osdn.net/frs/g_redir.php?m=kent&f=pisilinux%2Fsource%2Fmaster-pdf-editor-4.0.10_qt5.amd64.tar.gz" | tar xzs -C /headless \
    && ln -s /headless/master-pdf-editor-4/masterpdfeditor4 /usr/bin/masterpdfeditor4 \
    && mkdir -p $HOME/.config/Code\ Industry \
    && echo "[General]\ncheck_updates=0" >> $HOME/.config/Code\ Industry/Master\ PDF\ Editor.conf 
RUN ls -las /headless && ls -las /usr/bin/masterpdfeditor4 && ls -las /headless/master-pdf-editor-4
RUN apt-get clean -y

## ADD is only need due to docker-in-docker jenkins can`t currently mount volumens
ENV SAKULI_TEST_SUITE=/headless/sakuli/bakery
COPY . $SAKULI_TEST_SUITE
RUN $INST_SCRIPTS/set_user_permission.sh $SAKULI_TEST_SUITE
USER 1000
