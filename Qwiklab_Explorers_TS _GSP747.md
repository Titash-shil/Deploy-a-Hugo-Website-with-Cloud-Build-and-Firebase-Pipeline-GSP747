# Deploy a Hugo Website with Cloud Build and Firebase Pipeline || [GSP747](https://www.cloudskillsboost.google/focuses/14353?parent=catalog) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell

```
#!/bin/bash
# Define color variables

BLACK=`tput setaf 0`
RED=`tput setaf 1`
GREEN=`tput setaf 2`
YELLOW=`tput setaf 3`
BLUE=`tput setaf 4`
MAGENTA=`tput setaf 5`
CYAN=`tput setaf 6`
WHITE=`tput setaf 7`

BG_BLACK=`tput setab 0`
BG_RED=`tput setab 1`
BG_GREEN=`tput setab 2`
BG_YELLOW=`tput setab 3`
BG_BLUE=`tput setab 4`
BG_MAGENTA=`tput setab 5`
BG_CYAN=`tput setab 6`
BG_WHITE=`tput setab 7`

BOLD=`tput bold`
RESET=`tput sgr0`
#----------------------------------------------------start--------------------------------------------------#

echo "${BG_MAGENTA}${BOLD}Starting Execution${RESET}"

cd ~
/tmp/installhugo.sh

sudo apt-get update
sudo apt-get install git

cd ~
gcloud source repos create my_hugo_site
gcloud source repos clone my_hugo_site

cd ~
/tmp/hugo new site my_hugo_site --force

cd ~/my_hugo_site
git clone \
  https://github.com/budparr/gohugo-theme-ananke.git \
  themes/ananke
echo 'theme = "ananke"' >> config.toml

sudo rm -r themes/ananke/.git
sudo rm themes/ananke/.gitignore 

cd ~/my_hugo_site
  /tmp/hugo server -D --bind 0.0.0.0 --port 8080

gcloud compute ssh hugo-dev-vm --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --quiet --command="bash /tmp/prepare_disk.sh"

echo "${YELLOW}${BOLD}NOW${RESET}" "${WHITE}${BOLD}Check The Score${RESET}" "${GREEN}${BOLD}Upto Task 2 then Process Next${RESET}"
```

* Now Check The Score Upto `Task 2` then Process Next

```
#!/bin/bash
# Define color variables

BLACK=`tput setaf 0`
RED=`tput setaf 1`
GREEN=`tput setaf 2`
YELLOW=`tput setaf 3`
BLUE=`tput setaf 4`
MAGENTA=`tput setaf 5`
CYAN=`tput setaf 6`
WHITE=`tput setaf 7`

BG_BLACK=`tput setab 0`
BG_RED=`tput setab 1`
BG_GREEN=`tput setab 2`
BG_YELLOW=`tput setab 3`
BG_BLUE=`tput setab 4`
BG_MAGENTA=`tput setab 5`
BG_CYAN=`tput setab 6`
BG_WHITE=`tput setab 7`

BOLD=`tput bold`
RESET=`tput sgr0`
#----------------------------------------------------start--------------------------------------------------#

echo "${BG_MAGENTA}${BOLD}Starting Execution${RESET}"

curl -sL https://firebase.tools | bash

cd ~/my_hugo_site
firebase init

#add screenshot

/tmp/hugo && firebase deploy

git config --global user.name "hugo"
git config --global user.email "hugo@blogger.com"

cd ~/my_hugo_site
echo "resources" >> .gitignore

git add .
git commit -m "Add app to Cloud Source Repositories"
git push -u origin master

cd ~/my_hugo_site
cp /tmp/cloudbuild.yaml .

echo -e "options:\n  logging: CLOUD_LOGGING_ONLY" >> cloudbuild.yaml

gcloud alpha builds triggers import --source=/tmp/trigger.yaml

cd ~/my_hugo_site

sed -i "3c\title = 'Blogging with Hugo and Cloud Build'" config.toml

git add .
git commit -m "I updated the site title"
git push -u origin master

sleep 20

gcloud builds list

gcloud builds log $(gcloud builds list --format='value(ID)' --filter=$(git rev-parse HEAD))

gcloud builds log $(gcloud builds list --format='value(ID)' --filter=$(git rev-parse HEAD)) | grep "Hosting URL"

echo "${BG_RED}${BOLD}Congratulations For Completing The Lab !!!${RESET}"

#-----------------------------------------------------end----------------------------------------------------------#
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
