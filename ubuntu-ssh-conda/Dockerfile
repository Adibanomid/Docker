# HTTP SSH Image
FROM ubuntu:latest

RUN apt update && apt install -y bash-completion vim openssh-server wget net-tools zsh acl git

# Set environment variables for the new user and password
ENV USER_NAME=superdeveloper
ENV USER_PASS=dev12345
ENV GROUP_NAME=developer
ENV HTTP_PORT=8001

RUN mkdir -p /run/sshd
    
    

RUN groupadd ${GROUP_NAME} && \
    useradd -m ${USER_NAME} -s /usr/bin/bash && \
    usermod -g developer superdeveloper && \
    echo "$USER_NAME:$USER_PASS" | chpasswd


RUN mkdir -p /packages/conda
RUN mkdir /projects/

WORKDIR /packages/conda

COPY ./packages/miniconda.sh ./miniconda.sh

# ENV PROJECT_NAME=newproject
# ENV DJANGO_APP_NAME=newapp

## Initial Python

RUN bash /packages/conda/miniconda.sh -b -u -p /packages/conda
RUN rm -rf /packages/conda/miniconda.sh
RUN /packages/conda/bin/conda create -n myenv -y #python=3.11

# RUN /bin/bash source /packages/conda/bin/activate myenv
# RUN bash -c "source /packages/conda/bin/activate myenv"
# RUN /packages/conda/bin/conda install django -y
# RUN cd /projects
# RUN django-admin startproject ${PROJECT_NAME}
# RUN cd ${PROJECT_NAME}
# RUN python manage.py startapp ${DJANGO_APP_NAME}
RUN setfacl -R -m g:${GROUP_NAME}:rxw /projects
RUN setfacl -R -m g:${USER_NAME}:rxw /packages
# RUN setfacl -dR -m g:${GROUP_NAME}:rxw /projects
# RUN setfacl -dR -m g:${USER_NAME}:rxw /packages

USER ${USER_NAME}
RUN /packages/conda/bin/conda init bash && /packages/conda/bin/conda init zsh

USER root
VOLUME [ "/packages" ]
VOLUME [ "/projects" ]

WORKDIR /projects

CMD [ "/usr/sbin/sshd", "-D" ]

EXPOSE 22
EXPOSE ${HTTP_PORT}


### superuser still doesn't have permission to packages and projects

### must run in conda shell
# conda install -c conda-forge psycopg2 -y

### for rest-apis, must run in conda shell
# conda install -c conda-forge djangorestframework -y #(in conda shell)

### for using api request in core script, must run in conda shell
# conda install -c conda-forge requests -y


