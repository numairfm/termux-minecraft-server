## Termux Minecraft Server
Guide on how to run a Minecraft Server on android with Termux.

## Prerequisites

### Install Termux
Its recommended to install Termux from [F-Droid](https://f-droid.org/en/) as it is kept more updated than the one from the Google Play Store. You can get it from [here](https://f-droid.org/en/packages/com.termux/).

### Update package repositories
Open Termux and run the following commands to keep the package repositories updated:
`pkg update && pkg upgrade`

### Install JAVA
You need JAVA to run the server, to install it, run this command:
`pkg install openjdk-21`
You can confirm the installation by running:
`java -version`
If you dont see any errors, youre good to go!

### Set up the Minecraft Servers home
Give Termux access to your filesystem if you havent already. This is for convenience. Run:
`termux-setup-storage`
And press allow on the pop-up.

Its recommended to create a folder to store your files. For easy file access in the future, please create the folder in the android users home directory.
`cd ~/storage/shared  `
`mkdir termux-mc-server  `
`cd termux-mc-server  `
Once you are inside the newly created directory, we can proceed.

### Downloading the Minecraft Server
There are two ways you can go about this part. First is to use a browser and download the minecraft server jar file. Second is to use `wget` to directly pull the file to the folder from a link. Lets go through both.

## For the sake of the guide, I will be using the official Minecraft Server jar.

## If you choose the browser:
Go to the official [Minecraft Server](https://www.minecraft.net/en-us/download/server) website and download the minecraft_server file from the green link. Take note of the file name. If you can choose where to save it before downloading, save it to the `termux-mc-server` folder we created earlier. If you cant, it probably saved itself inside the Downloads folder. If you have, skip the next steps.

# Move the minecraft_server.jar file to the termux-mc-server folder using a file manager or by running these commands.
Use `ls` and `grep` to check the file name properly:
`ls ~/storage/shared/Downloads | grep "server"`
if you get an output, take note of the full name of the file. Lets assume the name is server.jar, then it would look like this:
`-> % ls ~/storage/shared/Downloads | grep "server"
server.jar`
Now you know the file name, lets move it to our servers directory.
`mv ~/storage/shared/Downloads/server.jar ~/storage/shared/termux-mc-server/`
Great! This parts done!

## If you choose to use wget:
Install wget inside termux with this command:
`pkg install wget`
Next, you run this command inside of the termux-mc-server directory:
`wget https://piston-data.mojang.com/v1/objects/6bce4ef400e4efaa63a13d5e6f6b500be969ef81/server.jar`
# At the time of making, this will download minecraft_server version 1.12.8. If at a later time it changes, you can go to the official website and copy the new download link to use with `wget`.

Great! This parts done!

### Running the Minecraft Server
Initialize the server by running this command:
`java -Xmx1024 -Xms1024 -jar server.jar nogui`
-Xmx and -Xms specify the max/smallest RAM allocations. -jar specifies the server jar to use (this allows you to also run other types of servers like a fabric or paper server).

Running the initialize command for the first time will generate the appropriate server files, you will have to edit the newly added eula.txt file and set the value to true.
`nano eula.txt`
If you need to change other settings, edit the server.properties file, but if not, run the start command again to make your server spin up for real.
`java -Xmx1024 -Xms1024 -jar server.jar nogui`
Once it starts, you will be able to connect using the private IP address of the servers host device. If you dont know it, you can check using `ifconfig` under the wlan secton if you are using wifi. An example would be `192.168.1.14`. What you do next is up to you. Enjoy!
