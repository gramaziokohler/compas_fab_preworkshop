# Pre-workshop: Introduction to compas_fab

**Windows users**: the only Windows version that supports many of the requirements is **Windows 10**, making it a pre-requisite for everything else.

## Requirements

* CAD Software:
    * [Rhinoceros 3D](https://www.rhino3d.com/): 5.0 or higher
    * If using Rhino 5.0, also install [Grasshopper](https://www.grasshopper3d.com/) and [GHPython](https://www.food4rhino.com/app/ghpython).
* [Anaconda Python Distribution](https://www.anaconda.com/download/): 2.7 or 3.x
* [Docker Community Edition](https://www.docker.com/get-started): Download it for [Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows) or [Mac](https://store.docker.com/editions/community/docker-ce-desktop-mac).
* X11 Server: On Windows use [XMing](https://sourceforge.net/projects/xming/), on Mac use [XQuartz](https://www.xquartz.org/) (see details [here](https://medium.com/@mreichelt/how-to-show-x11-windows-within-docker-on-mac-50759f4b65cb)).

## Getting started

* Start the X11 server (e.g. `XMing` on Windows)
* Make sure docker is running
* Download the `docker-compose.yml` file to your disk
* Open the command line, change to the folder where you downloaded the file and run:

        docker-compose up -d

* ROS will start up, including `MoveIt!`'s graphical interface.

## Notes

* An alternative way to install ROS on Windows is to use [WSL: Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
