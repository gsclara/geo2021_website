---
layout: assignment
assignment: 0
---

The instructions in this assignment will help you get started with linux, connecting to our server, foote, and intalling and using paraView, which will be necessary for postprocessing. 

- - - 
* Table of Content
{:toc}
- - - 

## 1. How to use linux systems

This assignment is supposed to be done after our introduction to Linux, which was done in geo1002 some time ago. 
For a refresher here you can find more [information](https://tudelft3d.github.io/geogeeks/linux/) 

Most common commands in linux during this course:

Copy folder to a determined location:
```
   cp -r nameFolder /path/to/location
```

Copy file to a determined location:
```
   cp nameFile /path/to/location
```

Remove folder: 
```
   rm -r nameFolder
```

Remove file:
```
   rm nameFile
```

Move inside a desired folder:
```
   cd /path/to/folder/
```

Move outside of a folder:
```
   cd ..
```

Create dummy file with 0KB size (necessary to visualize openFoam results):
```
   touch case.foam
```

Check what a command means and what are the arguments that can be passed:
```
   man command
```

## 2. Getting comfortable with vi or nano:

To do your assignments you will need to use a text editor, we normally recommend three: vi, nano or gedit (this one has an interface). 

If you would like to learn vi, which is quite powerful and nice to use but has a steep learning curve go [here](https://vimschool.netlify.app/introduction/vimtutor/).

If you would like to learn nano, which has a somewhat smoother learning curve go [here](https://www.nano-editor.org/docs.php)

Gedit has an interface, so you can just type as in any text editor generally, but more information [here](https://gedit-text-editor.org/index.html)

## 3. Connecting to our server, foote

Within our class we will use the Urbanism server which belongs to the department and it is used by researchers within it. 
It is important to keep in mind the best practices within the server to guarantee that everyone can use it for their work. 

### Best practices
	- Always do top to check how many people are running in the machine
	- Unless the machine is empty, please do not run with 32 cores
	- Most of your cases can run with just 16 cores

### Setting up your config file
First modify your config file insider folder .ssh in linux, if you don't have the .ssh folder create it, and then create the config file inside:
```
   mkdir .ssh
   vi .ssh/config (or nano .ssh/config, or gedit .ssh/config)
```
The dot before ssh just means that it is a hidden folder in linux.

Then add the following lines (keep indentation as it is, it does matter):

```
Host bastion
	Hostname student-linux.tudelft.nl
  	User netid
Host foote
  	Hostname foote.bk.tudelft.nl
  	ProxyCommand ssh -W %h:%p bastion
  	ServerAliveInterval 600
  	ForwardX11 yes
  	User groupN 
```

### How to connect to the server

To connect to the server you will be give a username and a password and you will need to connect through the tunnel (bastion) in order to be able to access our server. This means that if you would like to connect remotely from out of campus wifi you will need to install eduVPN for it to work. Assuming that your username is **groupN** these are the commands.

To connect to the server:
```
   ssh username@foote
```
The first time you connect you will be asked to approve the credentials, when it asks the question type *yes*.

To load openFoam application:
```
   of2412
```

To copy local folders (your own computer) to the server, there are two ways (preeferable use rsync, since you don't double copy this way): 

```
   scp -r /path/to/local/folder username@foote:/path/to/destinationfolder
   rsync -azhrP /path/to/local/folder username@foote:/path/to/destinationfolder
```

To copy from the server to your local folders (your own computer), there are two ways: 
```
   scp -r username@foote:/path/to/destinationfolder /path/to/local/folder 
   rsync -azhrP username@foote:/path/to/destinationfolder /path/to/local/folder 
```

To visualize the usage of the cluster:
```
  top
```
or 
```
  htop
```

To get out of the server
```
  exit
```

## 4. Installing and using paraView
Most probable you will be doing your postprocessing with [paraView](https://paraview.org) (although you could also do it in python, if interested just ask). This means that you need to install paraView in your computer and get comfortable with it by doing a few trys. There is a very good [tutorial](https://docs.paraview.org/en/latest/UsersGuide/index.html) with all the necessary information to perform different plotting. 


## 5. OpenFOAM use

OpenFOAM is installed for all users within the server, so it needs no installation, unless you want to use it in your computer. If you want to do that we can also support you with the installation.

### Most common comands used when running OpenFOAM:

To extract the edges of your geometries improving mesh generation steps: 
```
   surfaceFeatures
```

To create the background mesh for your case:
```
   blockMesh
```

To decompose your case in several processors for parallel computation:
```
   decomposePar
```

To run the meshing process in parallel:
```
   mpirun -np numberProcessors snappyHexMesh -parallel > log.SHM &
```

To reconstruct the mesh for visualization:
```
    reconstructParMesh
```

To run your case in parallel
```
   mpirun -np numberProcessors simpleTransportFoam -parallel > log.SF &
```

To reconstruct your case:
```
   reconstructPar  
```
To postprocess [residuals](https://github.com/gsclara/scripts/blob/main/plotResidualsOF.py) with python:
```
   postProcesssing residuals --> https://github.com/gsclara/scripts/blob/main/plotResidualsOF.py 
```

For the previous command to work, you need to add to system/controlDict the following (at the end of file):

```
   functions
   {
        #includeFunc residuals
   }
```
Note: notice the "simpleTransportFoam" here it is the general solver name for scalar dispersion case in the server (C for the name of variable and DC for the diffusion term)

[last updated: 2026-08-20 12:12]
