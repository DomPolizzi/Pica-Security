# Snort for Docker

#Special Thanks:
# To John-Lin for the Template idea and SnortUnsock(https://github.com/John-Lin)
# Janne Ruostemaa for the Snort Install guide (https://upcloud.com/community/tutorials/install-snort-ubuntu/ )

# I have also added comments to make it easier for anyone to reverse engineer/modify.

#Pull an OS
FROM ubuntu:20.04

#Update OS and Pull packages
RUN apt-get update && \
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
        #python-pip \
        python-dev \
        wget \
        build-essential \
        bison \
        flex \
        libpcap-dev \
        libpcre3-dev \
        libdumbnet-dev \
        zlib1g-dev \
        #iptables-dev \
        libxtables-dev \
        libip6tc-dev \
        libip4tc-dev \
        libnetfilter-queue1 \
        tcpdump \
        unzip \
        vim && pip install -U pip dpkt snortunsock

# Define Directory
WORKDIR /opt

#Define DAQ Variable (Data Acquisition library), latest is 2.0.7 https://www.snort.org/downloads/
ENV DAQ_VERSION 2.0.7
#Pull DAQ and Install
RUN mkdir ~/snort_src \
    && cd ~/snort_src  \
    && wget https://www.snort.org/downloads/archive/snort/daq-${DAQ_VERSION}.tar.gz \
    && tar -xvfz daq-${DAQ_VERSION}.tar.gz \
    && cd daq-${DAQ_VERSION} \
    # The latest version requires an additional step to auto reconfigure DAQ before running the config.
    && autoreconf -f -i \
    && ./configure; make; make install

#Define Snort Version, latest IS 3, I am choosing 2 for stability
ENV SNORT_VERSION 2.9.18.1
#Pull Snort and Install
RUN cd ~/snort_src \
    && wget https://www.snort.org/downloads/archive/snort/snort-${SNORT_VERSION}.tar.gz \
    && tar -xvfz snort-${SNORT_VERSION}.tar.gz \
    && cd snort-${SNORT_VERSION} \
    && ./configure; make; make install

# Configuring Snort to run in NIDS mode
RUN ldconfig 


# snortunsock - John-Lins
RUN wget --no-check-certificate \
        https://github.com/John-Lin/snortunsock/archive/master.zip \
    && unzip master.zip

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
    && cp ~/snort_src/snort-2.9.16/etc/*.conf* /etc/snort \
    && cp ~/snort_src/snort-2.9.16/etc/*.map /etc/snort 

# Configuration Setup, now to pull community rules. this is Optional and you can comment this section out if you wish
RUN wget https://www.snort.org/rules/community -O ~/community.tar.gz \
    && tar -xvf ~/community.tar.gz -C ~ \
    && cp ~/community-rules/* /etc/snort/rules \
    && sudo sed -i 's/include \$RULE\_PATH/#include \$RULE\_PATH/' /etc/snort/snort.conf

# Time for Cleanup! 
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    ~/snort_src/snort-${SNORT_VERSION}.tar.gz ~/snort_src/daq-${DAQ_VERSION}.tar.gz 

ENV NETWORK_INTERFACE eth0
# Validate an installation
# snort -T -i eth0 -c /etc/snort/etc/snort.conf
CMD ["snort", "-T", "-i", "echo ${NETWORK_INTERFACE}", "-c", "/etc/snort/etc/snort.conf"]