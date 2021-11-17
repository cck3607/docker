## Docker install

You can use refer to these pages as an installation guide for docker on ubuntu

The first step is running apt update
```markdown
sudo apt-get update
```
Next we want to upgrade 
```markdown
sudo apt-get upgrade
```
Next step to install docker with the command below
```markdown
sudo apt-get install docker.io
```
Ensure it is running 
```markdown
sudo service docker status
```
Start up docker
```markdown
sudo service docker start
```
check status again to ensure docker is running 
```markdown
sudo service docker status
```
Next install the container 
```markdown
sudo docker run -d -p 443:443 --name openvas mikesplain/openvas
```
After that is done installing open a browser and search. You must accept the risk and contiune after search.
```markdown
https://localhost
```
You should now see Greenbone Security Assistant page(openvas) login with
```markdown
username:admin
password:admin
```
Once logged in navigate to Configuration tab at top of tool bar and select a target. Should look image below.
![doc](https://user-images.githubusercontent.com/60015874/142032705-a980c631-877f-4307-a0fa-f913db60d56e.jpg)

After the tarfet is created we will now create the task by navigating to the scans tab and clicking on tasks. Then we will create a new task that should look similar to the window below.
```![FullSizeRender](https://user-images.githubusercontent.com/60015874/142093910-2ef6da1e-0605-448c-aa2d-086b313f168f.jpg)
```
Lastly we will create our docker-compose file. To do this we must create the docker-compose file in the terminal.
```markdown
touch docker-compose.yml
```
Now we need to add contents to that file with the following command.
```markdown
nano docker-compose.yml
```

Now inside the file copy and paste the following below. After pasted you can save and exit with control x
```markdown
version: '3.3'
services:
    nginx:
        ports:
            - '80:80'
        volumes:
            - '/var/run/docker.sock:/tmp/docker.sock:ro'
        restart: always
        logging:
            options:
                max-size: 1g
        image: nginx
```
Now run it with the following command.
```markdown
docker run -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro --restart always --log-opt max-size=1g nginx
```
