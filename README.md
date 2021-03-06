My kids were keen to have their own Minecraft server, to share between their friends and classmates, away from the main 
public servers out there.

Here's a quick guide to spinning up your own server with a minimum of fuss and config.

I opted for cloud-based free tier hosting, but this script will work with anything that can run docker.

**Compatibility**

This is a Minecraft: Pocket Edition server, so will work on the iPad + Android apps my kids use.
Have not tested on the laptop, java-based Minecraft clients.

**Online Safety**
This is for responsible parents.  
- This is a public, shared server
- It's not browsable in any Minecraft app
- You can only join by entering the host and port config from the apps
- But anyone with those details will be able to join
- Take care when sharing the server with others: don't post your public server on social media unless you don't care who joins
- Consider maintaining a whitelist of the gamertags for the friends you want to allow on (`./data/white-list.txt`)
- Consider reviewing the logs that are output to `./data/server.log`, to understand who's playing
- If in doubt, shut it down, spin up somewhere else 

**Manual pre-reqs**

- (optional) get a cloud host instance (e.g. AWS ec2, t2.micro.  I used this AMI: `Amazon Linux AMI 2018.03.0.20200206.0 x86_64 HVM gp2`)
- expose UDP for port 19132 (e.g. add firewall rule in ec2 security group)
- install docker if not already there (https://medium.com/@khandelwal12nidhi/docker-setup-on-aws-ec2-instance-c670ff3d5f1b)
- `git clone` this repo onto your running instance

`./run.sh` spins up the server container on port 19132.
Share your host's ip and port to join the game from a minecraft app.

Most apps will enforce that players will need a gamertag to join, so sign up. 

**Lookout for**

You might get a warning about `Detected 1 files in /data or /plugins not owned by the user "pocketmine"!`
Just follow the prompts about `chown`ing the data folder if so.

**Security note**

The config overrides in `data/server.properties` are supposed to make every player who joins an op, 
which I think is like an admin within the game (I know nothing about Minecraft).  A couple of posts/issues recommended this when I was
troubleshooting some stuff.

**Multiple worlds**

I think it's possible to host multiple worlds on one server, it hints at this in the config.

The fool proof way is just to spin up another copy.   For best results, clone a fresh repo in another folder and 
`./run.sh` passing a new port number for your parallel instance (remember to open up the port for UDP).  

