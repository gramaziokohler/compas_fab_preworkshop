_**links:**_ [Main compas docs](https://compas-dev.github.io/main/) | [compas_fab docs](https://gramaziokohler.github.io/compas_fab/latest/)

# Pre-workshop: Introduction to compas_fab

**Windows users**: the only Windows version that supports many of the requirements is **Windows 10** (Pro+), making it a pre-requisite for everything else.

> Note: if you get an error, scroll down and check the [Troubleshooting](#troubleshooting) section

## Requirements

* [Rhinoceros 3D 6.0](https://www.rhino3d.com/)
    * Focus will be on Rhino 6.0 only. While most things will work on Rhino 5.0, it is not recommended as there are several manual steps required to get the software to run. However, if you do use Rhino 5.0, make sure to install [Grasshopper](https://www.grasshopper3d.com/), [GHPython](https://www.food4rhino.com/app/ghpython) and [IronPython 2.7.5](https://github.com/IronLanguages/main/releases/tag/ipy-2.7.5) ([see here for details about this manual update](https://compas-dev.github.io/main/environments/rhino.html#ironpython-1)).
* [Anaconda Python Distribution](https://www.anaconda.com/download/): 2.7 or 3.x
* [Docker Community Edition](https://www.docker.com/get-started): Download it for [Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows) or [Mac](https://store.docker.com/editions/community/docker-ce-desktop-mac).
* X11 Server: On Windows use [XMing](https://sourceforge.net/projects/xming/), on Mac use [XQuartz](https://www.xquartz.org/) (see details [here](https://medium.com/@mreichelt/how-to-show-x11-windows-within-docker-on-mac-50759f4b65cb)).
* Git: [official command-line client](https://git-scm.com/) or visual GUI (e.g. [Github Desktop](https://desktop.github.com/) or [SourceTree](https://www.sourcetreeapp.com/))

## Getting started

### COMPAS

The very first thing to get started is to install **COMPAS** using Anaconda. Start your Anaconda Prompt and run the following:

      conda config --add channels conda-forge
      conda install COMPAS

Great! Now type `python` in your Anaconda Prompt, and test if the installation went well:

      >>> import compas

If that doesn't fail, you're good to go!

### Robotic fabrication package for COMPAS: compas_fab

We can now install **compas_fab**. Go to the Anaconda Prompt and run:

      pip install compas_fab

Let's make **COMPAS** and **compas_fab** packages available inside Rhino. Still on the Anaconda Prompt (you might need to be running as administrator), type the following:

> **NOTE:** 
>
> You only need to run one of those lines for the version of Rhino you use, or both if you use both versions.

      python -m compas_fab.rhino.install 5.0
      python -m compas_fab.rhino.install 6.0

### Backends

There are various tools used as backend for `compas_fab` and in order to make the development easier, we have packaged entire systems in  [Docker containers](https://www.docker.com/resources/what-container). Docker containers are a way to package software into isolated, standarized units with full reproducibility. 

#### V-REP backend

We publish [V-REP](http://www.coppeliarobotics.com/) docker images for [generic scenes](https://hub.docker.com/r/gramaziokohler/vrep/) and also a specific one for the [Robotic Fabrication Lab](https://hub.docker.com/r/gramaziokohler/vrep-rfl/) at ETH Zürich. To install the latter, run the following commands on the command prompt:

      docker pull gramaziokohler/vrep-rfl
      docker run --restart=always -p 19997:19997 -d gramaziokohler/vrep-rfl

#### ROS backend

Running a ROS setup usually involves multiple nodes (i.e. computers, real or virtual), interconnected through a master controller. To massively simplify the use of these tools, we package entire ROS systems into sets of Docker containers. Each of these sets runs in a virtualized network within your computer.   

In order to run a ROS system that includes a graphical interface, first make sure to start the X11 server (e.g. `XMing` on Windows).

The steps to run this kind of system are:

* Sign in to your Github account and Download the MoveIt file [`docker-compose.yml`](https://github.com/gramaziokohler/compas_fab_preworkshop/blob/master/ros_systems/moveit/docker-compose.yml) to your disk (or clone this repository)
* Open a Anaconda Prompt, change to the folder where the file resides and run:

        docker-compose up -d

* That's it! ROS will start up, including `MoveIt!`'s graphical interface and multiple other ROS nodes that take care of various tasks.

#### Notes

* An alternative way to install ROS on Windows is to use [WSL: Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

## Troubleshooting

Sometimes things don't go as expected. Here are some of answers to the most common issues you might bump into:

> Q: Docker does not start. It complains virtualization not enabled in BIOS.

This is vendor specific, depending on the manufacturer of your computer, there are different ways to fix this, but usually, pressing a key (usually `F2` for Lenovo) before Windows even start will take you to the BIOS of your machine. In there, you will find a `Virtualization` tab where this feature can be enabled.

> Q: Cannot start containers, nor do anything with Docker. Error message indicates docker daemon not accessible or no response.

Make sure docker is running. Especially after a fresh install, docker does not start immediately. Go to the start menu, and start `Docker for Windows`.

> Q: `conda` commands don't work.

Try running them from the *Conda Prompt*. Depending on how you installed Anaconda, it might not be available by default on the normal Windows command prompt.

> Q: When trying to install the framework in Rhino, it fails indicating the lib folder of IronPython does not exist.

Make sure you have opened Rhino 6 and Grasshopper at least once, so that it finishes setting up all its internal folder structure.

> Q: It fails when trying to install on Rhino.

Try starting the command prompt as administrator. Depending on the version of Python, it might be required or not.

> Q: error: Microsoft Visual C++ 14.0 is required

Follow the link to install Microsoft Visual C++ 14.0
https://www.scivision.co/python-windows-visual-c++-14-required/
