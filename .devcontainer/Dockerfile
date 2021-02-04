FROM cyn-ros-melodic-desktop-vnc:develop

# ** [Optional] Uncomment this section to install additional packages. **
#
USER root

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
   && apt-get -y install --no-install-recommends ros-melodic-catkin \
   python-catkin-tools \
   ros-melodic-moveit \
   #
   # Clean up
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog

USER cyn
# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/cyn/.bashrc

# # Change USER to 0 to get the root
USER cyn

# setup environment, now in the user mode
RUN echo "source /opt/ros/melodic/setup.bash" >> $HOME/.bashrc
# source is the command in /bin/bash, while the default shell is /bin/sh
RUN /bin/bash -c 'source /home/cyn/.bashrc'


#ENTRYPOINT ["/dockerstartup/vnc_startup.sh"]
#CMD ["--wait"]