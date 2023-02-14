# source: https://gist.github.com/audrow/259aa7f8ccf446c9b47d74aefe67df7b

FROM nvidia/opengl:base-ubuntu20.04
# FROM ubuntu:focal


ENV WS /root/dev
ENV ROS_PATH $WS/ros2_ws
ENV GAZEBO_PATH $WS/gazebo
ENV ROS_DISTRIBUTION rolling
ENV DEBIAN_FRONTEND noninteractive


# Install essentials
RUN \
	apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y \
		apt-utils \
		software-properties-common 
	# && apt-get update \
	# && apt-get install -y \
	# 	curl \
	# 	gdb \
	# 	mesa-utils \
	# 	mpg123 \
	# 	nautilus \
	# 	libgl1-mesa-glx \
	# 	libgl1-mesa-dri \
	# 	stress \
	# 	stress-ng \
	# 	terminator \
	# 	tmux \
	# 	unzip \
	# 	vim \
	# 	vlc \
	# 	wget \
	# && sed -i 's/geteuid/getppid/' /usr/bin/vlc \
	# && rm -rf /var/lib/apt/lists/*


# Add github command line
RUN \
	apt-get update \
	&& rm -rf /var/lib/apt/lists/* \
    && apt-get update && apt-get install locales \
	&& locale-gen en_US en_US.UTF-8 \
	&& update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 \
	&& export LANG=en_US.UTF-8 \
	# install development tools and ros tools
	&& apt-get update && apt-get install -y curl gnupg2 lsb-release \
	&& curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null \
	&& apt-get update \
	&& apt-get install -y \
    	build-essential \
		cmake \
		git \
		libbullet-dev \
		python3-colcon-common-extensions \
		python3-flake8 \
		python3-pip \
		python3-pytest-cov \
		python3-rosdep \
		python3-setuptools \
		python3-vcstool \
        ros-rolling-desktop     

# Setup ROS2 Rolling from source as per
# https://index.ros.org/doc/ros2/Installation/Rolling/Linux-Development-Setup/
# RUN \
# 	# setup locale
# 	apt-get update && apt-get install locales \
# 	&& locale-gen en_US en_US.UTF-8 \
# 	&& update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 \
# 	&& export LANG=en_US.UTF-8 \
# 	# install development tools and ros tools
# 	&& apt-get update && apt-get install -y curl gnupg2 lsb-release \
# 	&& curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc |  apt-key add - \
# 	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" |  tee /etc/apt/sources.list.d/ros2.list > /dev/null \
# 	&& apt-get update \
# 	&& apt-get install -y \
# 		build-essential \
# 		cmake \
# 		git \
# 		libbullet-dev \
# 		python3-colcon-common-extensions \
# 		python3-flake8 \
# 		python3-pip \
# 		python3-pytest-cov \
# 		python3-rosdep \
# 		python3-setuptools \
# 		python3-vcstool \
#         ros-rolling-desktop \
# 		wget \
# 	# install some pip packages needed for testing
# 	&& apt-get update \
# 	&& python3 -m pip install \
# 		argcomplete \
# 		flake8-blind-except \
# 		flake8-builtins \
# 		flake8-class-newline \
# 		flake8-comprehensions \
# 		flake8-deprecated \
# 		flake8-docstrings \
# 		flake8-import-order \
# 		flake8-quotes \
# 		pytest-repeat \
# 		pytest-rerunfailures \
# 		pytest \
# 		setuptools \
# 	# install Fast-RTPS dependencies
# 	&& apt-get install --no-install-recommends -y \
# 		libasio-dev \
# 		libtinyxml2-dev \
# 	# install Cyclone DDS dependencies
# 	&& apt-get install --no-install-recommends -y \
# 		libcunit1-dev 
	# setup the workspace
	# && mkdir -p $ROS_PATH/src \
	# && cd $ROS_PATH \
	# && wget https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos \
	# && vcs import src < ros2.repos \
	# # install package dependencies
	# && rosdep init \
	# && rosdep update \
	# && rosdep install --from-paths src --ignore-src --rosdistro rolling -y --skip-keys "console_bridge fastcdr fastrtps rti-connext-dds-5.3.1 urdfdom_headers" \
	# # setup bloom for making releases
	# && apt-get install -y \
	# 	python3-catkin-pkg \
	# 	python3-bloom \
	# && rm -rf /var/lib/apt/lists/*

# # Build the ROS2 workspace
# RUN \
# 	cd $ROS_PATH \
# 	&& colcon build --symlink-install

# Setup gazebo
# ENV GAZEBO_MAJOR_VERSION 11
# COPY ./setup_gazebo.bash /setup_gazebo.bash
RUN \
    # Add Ignition's latest packages
	apt-get install wget \
    && /bin/sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list' \
    && /bin/sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-nightly `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-nightly.list' \
    && /bin/sh -c 'wget http://packages.osrfoundation.org/gazebo.key -O - | apt-key add -' \
	# Install the latest Ignition binaries
    && apt-get -qq update \
	&&  apt-get install -y ignition-fortress

