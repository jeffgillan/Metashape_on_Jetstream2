# Metashape_on_Jetstream2
These are my ongoing notes on doing networked photogrammetry processing with Agisoft Metashape on Jetstream2.

## Remotely connecting to in-house resources gpu06 and gpu07
Gpu06 & gpu07 are high performance linux servers location in UITS on UA campus. They each have 2 x Nvidia GTX 1080 gpu processors. 

You can connect via ssh in a terminal or in VS Code

ssh jgillan@gpu06.cyverse.org -p1657  or ssh jgillan@128.196.254.151 -p1657  
ssh jgillan@gpu07.cyverse.org -p1657  or ssh jgillan@128.196.254.89 -p1657

Use Cyverse password

![](./images/ssh_screenshot.png)

## Connecting to gpu06 or gpu07 with graphical remote desktop
* Gpu06 & 07 do not have desktops so we can’t remote into them.
* Instead, you can create a container on gpu06 with desktop and software
** Connect to gpu06 with ssh (shown above) in a local terminal
** Once in gpu06, you are going to start a Docker container which should contain metashape and other dependencies

export DISPLAY=:0
xinit &
docker run --gpus all --rm -it -p 9876:9876 -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY -e XAUTHORITY -e QT_X11_NO_MITSHM=1 -e NVIDIA_DRIVER_CAPABILITIES=all harbor.cyverse.org/vice/xpra/cudagl:20.04

You can view the docker container in the local machine web browser
http://gpu06.cyverse.org:9876/
