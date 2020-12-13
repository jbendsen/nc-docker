# nc-docker
This project demonstrates how to copy a DOS program into the docker image and run it inside the docker container. 

## Prerequisites
1. Docker, e.g. Docker for Windows
2. A VNC client, e.g. VNC Viewer e.g. https://www.realvnc.com/en/connect/download/viewer/windows/

## Instructions for running this example 
1. Clone the project into a folder, .e.g. `git clone https://github.com/jbendsen/nc-docker.git`
2. Start a shell (e.g. powershell) change the current directory to the project folder (from 1.) 
3. Build a new docker image: `docker build -t nc-docker:1.0.1 .`
4. Start the docker container: `docker run -d -p 5901:5901 nc-docker:1.0.1`
   Docker will output the name of the container, e.g.  `fbb460cefc75cfa86ae8e5d3abd8658f420cfbd39099a2a524d31687e0221b30`. Notice the first 3 letters.  
5. We now need docker to show us the logs because they contain the password 
   for the VNC console. Type: ` docker logs fbb --since 10m`. This shows the logs for the 
   past 10 minutes (10m).
6. Search for `*** VNC password for this session: <password>`.
7. Copy the password by highlighting by selecting it and press enter. 
   (Or write it down).
8. Start VNC Viewer.
9. Enter the address: `localhost:5901`. Press enter. 
10. Hopefully a terminal windows opens showing a command prompt like: `root@fbb460cefc75:/#` 
11. Enter `cd usr/local/bin`.
12. Enter `startdossession s1` (this starts a DOS session named s1)
13. Enter `g:`. This changes current dir to G drive.
14. Enter `cd program1` (this is the directory copied from the project folder
    `./dos/drive_g/program1`)
15. Enter `program.bat`. The simple batch program executes and prints a message.
16. To stop the container type: `docker stop <id>`. E.g. `docker stop fbb`.

## Running other DOS programs
If you want to run real DOS programs it's easy. Heres an outline:
1. Get the DOS-program. You can find a lot here: https://www.abandonwaredos.com, 
   e.g. Norton Commander: https://www.abandonwaredos.com/abandonware-game.php?abandonware=Norton+Commander+5.5&gid=1814
2. Copy the folder containing the program into the project folder under ./dos/drive_g   
3. Modify the ./Dockerfile's `COPY ./dos/drive_g/program1 /dos/drive_g/program1` line to
   copy the new program folder.
4. Repeat the above steps 3. to 13. 



    



