Install from Source (Debian, Ubuntu)
====================================

These instructions outline how to install an all in one Opencast system on Ubuntu 12.04 with LTS.

Preparation
-----------

Create a dedicated Opencast user:

    useradd -d /opt/opencast opencast

Get Opencast source:

You can get the Opencast source code by either downloading a tarball of the source code or by cloning the Git
repository. The latter option is more flexible, it is easier to upgrade and in general preferred for developers. The
prior option, the tarball download, needs less tools and you do not have to download nearly as much as with Git.

Using the tarball:

Select the tarball for the version you want to install from the [BitBucket downloads section
](https://bitbucket.org/opencast-community/matterhorn/downloads).

    # Download desired tarball
    curl -O https://bitbucket.org/opencast-community/matterhorn/...
    tar xf ....tar.gz
    cd opencast-community-...

Cloning the Git repository:

    git clone https://bitbucket.org/opencast-community/matterhorn.git
    cd matterhorn
    git tag   <-  List all available versions
    git checkout TAG   <-  Switch to desired version


Install Dependencies
--------------------

Please make sure to install the following dependencies. Note that not all dependencies are in the system repositories.

Required:

    openjdk-7-jdk or openjdk-8-jdk
    ffmpeg >= 2.8
    maven >= 3.1

Required (not necessarily on the same machine):

    ActiveMQ >= 5.10 (older versions untested)

Required for text extraction (recommended):

    tesseract >= 3

Required for hunspell based text filtering (optional):

    hunspell >= 1.2.8

Required for audio normalization (optional):

    sox >= 14.4

### Dependency Download

Pre-built versions of most dependencies that are not in the repositories can be downloaded from the respective project
website:

 - [Get FFmpeg](http://ffmpeg.org/download.html)
 - [Get Apache Maven](https://maven.apache.org/download.cgi)
 - [Get Apache ActiveMQ](http://activemq.apache.org/download.html)


Building Opencast
-----------------

Automatically build all Opencast modules and assemble distributions for different server types:

    cd opencast-dir
    mvn clean install

Deploy all-in-one distribution:

    cd build/
    mv opencast-dist-allinone-*/ /opt/opencast

Make sure everything belongs to the user `opencast`:

    sudo chown -R opencast:opencast /opt/opencast


Configure
---------

Please follow the steps of the [Basic Configuration guide](../configuration/basic.md). It will help you to set your
hostname, login information, …


Running Opencast
------------------

To start Opencast, run `.../bin/start-opencast` as user `opencast`:

    sudo -u opencast /opt/opencast/bin/start-opencast

As soon as Opencast is completely started, browse to [http://localhost:8080](http://localhost:8080) to get to the
administration interface.


Run Opencast as a service
-------------------------

Usually, you do not want to run Opencast in interactive mode but as system service to make sure it is only running
once on a system and is started automatically.

*TODO: Add notes about Systemd and SysV-Init scripts once they are added.*