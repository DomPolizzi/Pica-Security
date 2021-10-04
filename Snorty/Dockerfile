# Snort for Docker

#Special Thanks:
# To John-Lin for the Template idea (https://github.com/John-Lin)
# Janne Ruostemaa for the Snort Install guide (https://upcloud.com/community/tutorials/install-snort-ubuntu/ )

# I have also added comments to make it easier for anyone to reverse engineer/modify.

#Pull an OS
FROM ubuntu:20.04

#Update OS and Pull packages
RUN apt-get update && \
    apt-get install -y tzdata && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get install -y \
    gcc \
    libluajit-5.1-dev \
    openssl \ 
    libssl-dev \
    libnghttp2-dev \ 
    libdumbnet-dev \
    libdnet \ 
    autoconf \ 
    libtool \
    python-setuptools \
    python3-pip \
    python-dev \
    wget \
    build-essential \
    bison \
    flex \
    libpcap-dev \
    libpcre3-dev \
    libdumbnet-dev \
    zlib1g-dev \
    libxtables-dev \
    libip6tc-dev \
    libip4tc-dev \
    libnetfilter-queue1 \
    tcpdump \
    unzip \
    vim

# Define Directory
WORKDIR /opt

#Define DAQ Variable (Data Acquisition library), latest is 2.0.7 https://www.snort.org/downloads/
ENV DAQ_VERSION 2.0.7
#Ptzdata ull DAQ and Install
RUN mkdir ~/snort_src \
    && cd ~/snort_src  \
    && wget https://www.snort.org/downloads/archive/snort/daq-${DAQ_VERSION}.tar.gz \
    && tar xvfz daq-${DAQ_VERSION}.tar.gz \
    && cd daq-${DAQ_VERSION} \
    # The latest version requires an additional step to auto reconfigure DAQ before running the config.
    && autoreconf -f -i \
    && ./configure; make; make install

#Define Snort Version, latest IS 3, I am choosing 2 for stability
ENV SNORT_VERSION 2.9.18.1
#Pull Snort and Install
RUN cd ~/snort_src \
    && wget https://www.snort.org/downloads/archive/snort/snort-${SNORT_VERSION}.tar.gz \
    && tar xvfz snort-${SNORT_VERSION}.tar.gz \
    && cd snort-${SNORT_VERSION} \
    && ./configure; make; make install

# Configuring Snort to run in NIDS mode
RUN ldconfig 

# create a symbolic link to /usr/sbin/snort. 
RUN ln -s /usr/local/bin/snort /usr/sbin/snort \
    #create folder structure to house the Snort configuration
    && mkdir -p /etc/snort/rules \
    && mkdir /var/log/snort \
    && mkdir /usr/local/lib/snort_dynamicrules \
    #Make Rules
    && touch /etc/snort/rules/white_list.rules \
    && touch /etc/snort/rules/black_list.rules \
    && touch /etc/snort/rules/local.rules \
    && cp ~/snort_src/snort-${SNORT_VERSION}/etc/*.conf /etc/snort \
    && cp ~/snort_src/snort-${SNORT_VERSION}/etc/*.map /etc/snort 

# Configuration Setup, now to pull community rules. this is Optional and you can comment this section out if you wish
RUN wget https://www.snort.org/rules/community -O ~/community.tar.gz \
    && tar xvf ~/community.tar.gz -C ~ \
    && cp ~/community-rules/* /etc/snort/rules \
    && sed -i 's/include \$RULE\_PATH/#include \$RULE\_PATH/' /etc/snort/snort.conf

# Time for Cleanup! 
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    ~/snort_src/snort-${SNORT_VERSION}.tar.gz ~/snort_src/daq-${DAQ_VERSION}.tar.gz 

#ENV NETWORK_INTERFACE eth0
# Validate an installation
CMD ["snort", "-V"]