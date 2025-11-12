So the basic idea is that we use oracle cloud to host our MC server. Why? Because Oracle provides free 4 core CPU and 24 GB RAM in their always free tier.

Main Idea:
1. Set up instance
2. Set up networking
3. Configure Ubuntu and download and run MC files

Set up instance:
1. Create an oracle cloud account.
2. Set the operating system to be Ubuntu 24
3. Set the shape to be the always free ARM tier
4. Download the private key
5. It will ask you to create a VCN hit yes to that and create one everything else doesn't really matter

Set up networking:
1. Here we are editing the VCN. Go to your instance and select Networking -> Scroll to Attached VNICs -> Select the first one
2. We also want to make sure there is a public ip so just like youtube video that if you dont have a public ip
3. Select the subnet -> Security -> Click on the default security list -> Security Rules
4. Add Ingress Rules - **Source**: 0.0.0.0/0 **Protocol**: TCP **Destination Port Range**: 25565 **Else**: Leave Empty
5. Add Ingress Rules - **Source**: 0.0.0.0/0 **Protocol**: UDP **Destination Port Range**: 25565 **Else**: Leave Empty
6. Go back to Networking of Instance and make sure there are NO Network Security Groups if there is, remove it

Configuring Ubuntu and downloading:
1. SSH into the server using the downloaded private key and move it into ~/.ssh make the permission to be able to ssh into `chmod 600 ~/.ssh/oracle-key.key` and then do `ssh -i ~/.ssh/oracle-key.key ubuntu@<public ip>`
2. `apt update`
3. ok im not going to go through the other apt gets but if the program is missing just apt get it
4. `sudo apt install ufw -y` `sudo ufw allow 22/tcp`
`sudo ufw allow 25565/tcp`
`sudo ufw enable`
5. Make a directory to download stuff into
6. download by running the command from just the ftb website here: https://feed-the-beast.com/modpacks/server-files
7. Run the executable `./whateverfileitis`
8. Create screen and run the bash so like `bash run.sh` on first run you have to write `true` to accept the eula
9. Exit screen by doing ctrl-a + d
10. On Ubuntu: Test: `nc -vz 127.0.0.1 25565`
11. On local machine: Test: `nc -vz <public ip> 25565`


