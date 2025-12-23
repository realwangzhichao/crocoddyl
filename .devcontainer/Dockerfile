FROM osrf/ros:jazzy-desktop-full

# Add ubuntu user with same UID and GID as your host system, if it doesn't already exist
# Since Ubuntu 24.04, a non-root user is created by default with the name vscode and UID=1000
ARG USERNAME=ubuntu
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN if ! id -u $USER_UID >/dev/null 2>&1; then \
        groupadd --gid $USER_GID $USERNAME && \
        useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME; \
    fi
# Add sudo support for the non-root user
RUN apt-get update && \
    apt-get install -y sudo && \
    echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

# Switch from root to user
USER $USERNAME

# Add user to video group to allow access to webcam
RUN sudo usermod --append --groups video $USERNAME

# Update all packages
RUN sudo apt update && sudo apt upgrade -y

# Install Git
RUN sudo apt install -y \
    git \
    vim \
    #xterm display
    xterm \
    dbus-x11 \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    x11-xserver-utils \
    gcc-11 g++-11

# for render check
RUN sudo apt-get update && \
    sudo apt-get install -y \
      mesa-utils \
      libgl1-mesa-dri \
      libglx-mesa0 \
      python3-pip
      
# Rosdep update
RUN rosdep update

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

################################
## ADD ANY CUSTOM SETUP BELOW ##
################################
# Config xterm terminal display
COPY --chown=${USERNAME}:${USERNAME} /config/.Xresources /home/${USERNAME}/.Xresources
RUN echo '\n\
# Load XTerm settings when an X display is available\n\
if [ -n "$DISPLAY" ] && command -v xrdb >/dev/null 2>&1; then\n\
  xrdb ~/.Xresources\n\
fi\n' >> /home/${USERNAME}/.bashrc