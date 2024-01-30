# - Jake's Oct 30th - remote server lecture
npm i -g bcw (update bcw templates)
app.vue upload libraries

zoom lectures Monday
https://us02web.zoom.us/j/87241184568?pwd=VDNadzZNQjJ1OW5kRDBROWhUTEZMZz09
https://us02web.zoom.us/rec/share/X1P_xjh1lY_LZJQu0kJx87uo9neXS028Uw3R4MUo-uAc1DSY9tTZ25N5mmp_pMD1.XnH40OpxhbR_MKj8
Passcode: S0d!7#gg

zoom lectures Tuesday
https://us02web.zoom.us/j/87640004745?pwd=SW1ibk5ieDhRSTUwcmFtbHZtUjJ5Zz09

zoom lectures Wednesday
https://us02web.zoom.us/j/87560540986?pwd=Q1VXUkNOV2tGOVhQWm4yc2RzdnJMdz09


zoom lectures Thursday
https://us02web.zoom.us/rec/share/xxw1QUtj-y4BY-vvZlbEBFelVJzfr2qhuv1AKeBojzVNFCNUqmUQoBZarr_pJ_w1.YHy25x3qROJ10IM8
Passcode: V2%.E8Bq

********************
# - AWS_Sandcastle
********************
Portfolio-work
NinhaoD!anNa0
AWS cloud server
Amazon Web Services
    Between that and Azure - most enterprise-ready servers

AWS - Azure pro/con
Business for Azure, entry lvl use AWS
AWS dashboard less friendly
Identical function at core

# Easy to have $300-$500 mistakes - PAY ATTENTION
    Sign-up requires a credit card number
#   PUT IN BILLING ALERTS
    * multi-factor authentication - USE IT

* Services tab
    CodePipline and Code Deploy AND Billing
750 runtime hrs/mo are free
    single cpu core

#NOTE - openvpn.net
    nord and defaults will steal your info regardless

IP address points go from 0-255 for each section 192.37.7.12
Local Network IPV4 -- first two sets of digits must be identical
last number next door == computer server is next like houses on a block
    If not local...can have different first 2 digit sets
*NOTE    0.0.0.0 <-- can talk to anyone in the world
So gateways were put in to separate external and internal addresses
all Codeworks similar to 192.169.0-255.0-255

Each device has this - so your watch, phone, laptop, etc
10.10.0.0 is BCW skynet block
198, 174, 10.10 <-- are common starter networks
192 is home routers

All codeworks talk to a single Internet Provider -> 64.13.32.12 -> our local subnets, all the 192.168.#.#
    This is how the provider provides, this is their router address
#NOTE - internet facing IP address is the one that cpsts money - is "static IP address" - no other device can have it

Internet is just a network itself

IPV6
0-Z::0-Z::0-Z::0-Z::0-Z
^ is also case sensitive, so 0-9--abcdefgABCD-A-Z
Was approved 15-ish years ago, but transition is SLOW, more devices = bigger problem


# - Goal --> deploy apps (Geo-Stache)
DNS domain name services translates IP to what you read as a site title

Heavy lifting to use free stuff

Services tab -- or search -- EC2 (star this as favourite)

# EC2
US - Oregon has generally less traffic than CA
    *NOTE - use only 1 region to avoid charges, 2+ regions is separate servers, separate = charges

*Instances tab - you get charged for space of each instance
    terminating these takes time, they exist on dashboard until truly gone

#   Launch an Instance
    *NOTE - CAREFUL
    *NOTE - Choose FREE TIER ELIGIBLE only

    Name: this is for your remembrance

    Amazon Machine Image
        Ubuntu
            (AWS Linux is..unpleasant)
            Windows is too heave for a free tier
        ONLY CHOOSE A FREE TIER ELIGIBLE
        64-bit(x86)
            arm requires software
    *Instance type - "box size"
        FREE TIER ELIGIBLE
Each instance of a free tier is still hosting a PER HOUR
    you only get 750/mo

Key Pair login
    Create new
        Leave options default
            Name something with kabob-case
                will auto download a .pem file
                    open w/ notepad
                        this is your password
Network settings
    Set firewall
        keep from ANYone from accessing
            if they have your private key, they can access your box
                if there is credit card info, lock your box down, not 0.0.0.0/0
                152.37.215.61/32 is the public BCW IP address
        Edit tab
            inbound security rules
                HTTPS - port range
                    computers have +65,000
                    ports are reception range, not send
                HTTP is 80
                HTTPS is 443
                ssh is 22
            Set security name
            Set description
        Add security group rule
            MYSQL/Aurora
                port range is 3306 - this is our port from the projects we made
                    many co will change, because well-known = vulnerable to attack
                        if you change, then the data will be blocked or filtered w/ wrong connection string - hit's machine, but no reply
                Source type - Anywhere 0.0.0.0/0
                    SO
                        Set up a good password, or anyone can access database
        Create a security group
            Encryption is encryption at rest vs in transit
<!-- do not need to adjust advanced -->
        Advanced details - mainly once into active directory
            users have roles and permissions
                user rules
                Request Spot Instance - cheap - only runs when needed
                    BUT if no room to run (ie, on black Friday), will not ever run
When NOT paying for static IP address - all your traffic will be sent to someone else's stuff
AWS does IP resolver, pay monthly to tag URL to always go to a machine type spun up/torn down
    but you are paying
        so pay for static OR on instance
            this is good for big co ie Walmart for Walmart.com to allow for directory to locations vs a single page directory

You need your public IP address

# How to enter into this machine

use pwsh in aws (powershell) - running against server box
once connected disable general ubuntu prefic for security purposes
use the server name (ubuntu)@IP public address
    always answer yesterminal will change to your ubuntu@ip-#-#-#-#:
        this is your virtual private cloud IP - your private Ip, no longer your public one from AWS
    git comes with ubuntu - NODE is NOT, nor is MySQL
        We must install
            anything you run in your dev enviroment, you will need to install here
                we are getting off of scalegrid

# Follow class daily outline
"sudo" - super user do (forget to append "sudo", do "sudo !!" to run last command w/ sudo beofre)
"apt" <-- this is th installer cue
sudo apt update
sudo apt upgrade
    this is a windows update equivalent
Updating it weekly is not unheard of
    Every Tuesday is a windows update
        bug fixes on Thursday
            Do Thursday prompts, these are for security
*NOTE - use tab to select approval for update
    will not restart services in use
MySQL server is a server - can have 100s of databases
    MySQL database is 1
        databases have multiple tables
            database per project, but all use same connection string

sudo apt install mysql-server-y <-- -y is to auto "yes"
make MySQL auto launch with reboot, or else will have to do manually
sudo systemctl start
    sudo systemctl enable mysql
    sudo systemctl status mysql
        looking for "enabled" in loading line

in mysql
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password By '100%SECUREd';    <-- new password entered NOW, using MySQL syntax
sudo mysql-p
    now can enter password (locked down even to admin)
sudo mysql_secure_installation
    password prompt
        make strong - prevents creation
            YOUR PASSWORD needs to pass this or else you lock yourself out
        remove all default settings
            remote login is not allowed, now, so need a way to do remote logins for access to your projects
sudo mysql-p
    CREATE USER 'pick anything you want for this name'@'localhost' IDENTIFIED BY '100%AppleJuice';
    CREATE USER 'pick anything you want for this name'@'%'localhost' IDENTIFIED BY '100%AppleJuice';
        '%' is what allows any

GRANT ALL PRIVILEGES ON *.* TO 'pick anything you want for this name '@'localhost'; 
GRANT ALL PRIVILEGES ON *.* TO 'pick anything you want for this name '@'%'localhost'; 


FLUSH PRIVILEGES; <--reloads table

exit

reconnect
mysql -u ____ -p
    choose user and then enter password for rec user
cd.. takes you home
cd.. takes you to upmost level
cd /etc
cd mysql/
ls
    modify to let it talk out and receive messages in
cd mysql.conf.d/
    .d = debien <-- runs what you are doing
sudo nano mysqld.cnf <-- default built-in text editor

*can change all in white change network bind-address (first, only)

CTRL+x --> y --> enter
bind-address = 0.0.0.0

*Must restart server or else changes will nto apply
sudo systemctl restart mysql
sudo systemctl status mysql - active should say running



# in VS CODE
connect host to your new IP

username is the username from mysql
password is password
rename the whole file
can create database
    CREATE DATABASE keepr

new .json with "connections"    <-- set as snippet
ls -lsa
    ssh ls
        cat authorized_keys

danielmiessler SecLists


Make passwords because bots are scraping IP addresses
    it does not matter if a person cares, the bot doesn't, and a person will check it
    
    Subnet - intermediate server to protect real database
        using mongoDB - that security is set up
    


Black Hat and defcon are hacker conferences
*NOTE - learn what FTP is -- file transfer port???
*NOTE - disable your VPNs on reload, or in general?

# Jake's Tuesday lecture

Multiple projects can exist in an EC2 instance(box)

the parent local host must relay messages - they cannot communicate to one another
    each have own 0-65,000+ ports, nothing shared

# Github Actions
#FIXME - Lint & Test
    was not taught, will need to know - expected industry standard

# - https://yaml.org
YAML
    # - is a comment
    Header is tabbed in followed by :
        - X is a subheading
All Github actions are written in YAML

fill-in/fill-in (second one is not there until)

docker push camilleivins/out-of-harbor:tagname

auth0 only works over http not https, so looking for super cheap domains - ten bucks for a year

Top level file
.github\workflows
    w/in that
    build.yml
    deploy.yml

GitHub secrets - need to be text-exact to the file secrets int he dockerfile
pem key will need to beginning and end lines, even though they are not part of the key, per se

sudo apt upgrade sudo apt install nginx

sudo systemctl status nginx

sudo nano /etc/nginx/sites-available

    change defaults
        ctrl + K to delete after line 'please see /usr/share/doc/...'

DO STEP 3 on today, not step 2

any changes require restart
sudo systemctl restart nginx

subdomains need a new server block entirely

3-4 applications will make all projects run poorly

******************************
# Jake's Wednesday lecture
******************************
*NOTE - docker-compose.yml and dockerfile are same par w/ appsettings.json

#FIXME - CTRL +, to get workspace tap, click the upper right go to file to enter workspace file to edit
can add a workflows one, path .github/workflows
    creates top level path - even if data is not top level - is a shortcut so you do not need to open layers
for NODE js projects
    rename all name for the top level client and server folders to "client" and "server"

*****************************
#   LINK - Buy your domain and do your DNS through Cloudflare.com
*****************************
Use multi-factor auth

Left side
    domain registration
Bought?
    go to Overview
        can see analytics

* How to tie to EC2 instance
Lefthand side
    DNS
        Records
            Add a record
                "A record" is for IP addresses (CNAME domain, do not use right now, can have TXT text record - does )
                    and x.y.com the first piece "x." is a subdomain - even if multiple x., still all technically one
                    @ = no subdomain
                        add IP domain from site (public)
                            verify with proxy off, once verified
                                turn proxy back on
                                    Cloudeflare handles request
                                        SAVE - 30s to an hr for changes
                            TTL - time to live - time until cache is cleared
SSL/TLS
    Overview
        SSL?TLS is defaulty on "OFF"
            change to "Full (strict)"
                you have to install a key into your origin server
                    encrypt so you are the only one to read even your public key
                        CLOUDFLARE will not even see your key
                            this is the healthcare/HIPPA lvl compliance
                                PII cert if 1st, last, and e-mail
                                    millions of companies could be sued in us
                    we have to install origin certificate so that site works - even for us
    Origin Server
        create cetificate
            leave defaults
                now have origin cert and private key
                    cert is public, key is private

In NginX
    sudo nano etc/nginx/sites-available/default
* NOTE - this is the step 2 skipped yesterday
        paste in server block
             listens (http) port 80
                server_name - *your domain name*
                return 301 <--redirect
sudo nano ssl/cert.pem
    paste in cloudflare cert - all lines
sudo nano ssl/key.pem
    paste in cloudflare key - all lines 
sudo systemctl restart nginx


auth0
    log-in
        Applications
            go into the single-page app
                Application URIs
                    ADD new domain w/ https prefix
                        SAVE CHANGES

IN VS COde project
    use audience and client keys from Auth0 ENV info

Pull request - production

set environment variables in new github action secret

THIS WORKS - saves from needing private images on docker-hub -ie, more free

****************
# Keepr, dotnet
****************

Dockerfile - dotnet/sdk:6.0 <-- will be 8, soon, new dotnet edition is coming out next month

    docker-compose will be manually built for us
* LINK - Example is lt_summer23_docker_sharp
username - ubuntu
pem key - is in cat ./portfolio.work.pem (yours)
EC2_IP_ADDRESS - public ip (aws)
docker_compose - NOTE - will eed to change ports to 7045:80
ROUTE_PREFIX
    add to secrets
        node-project
            configures node server to run with this modification
docker exec <--used to open a running container (image)

microsoft.learn for Azure docs and labs (all free)
ssh -i portfolio-work.pem ubuntu@52.42.221.233

https://github.com/JustinCarpenter2020
https://github.com/JustinCarpenter2020/JustinCarpenter
https://github.com/EwanStubblefield-Allen/Landing_Page
https://ewanstubblefield-allen.dev/#/
https://rebeccavandewater.github.io/#home