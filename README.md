# Boulder competition software with "koivukylä" score calculation


## Setup guide

Install miniconda (if you don't have conda installed already)
```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```
Initialize conda for bash and zsh
```
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```
Clone this project into home directory and move to the project directory
```
git clone git@github.com:santerihukari/Node-postgres-boulder-compsoftware.git ~/pjchallenge
cd ~/pjchallenge
```

Create conda environment with the provided list of package versions.
```
conda create -n PJ-Challenge_compsoftware --file ~/pjchallenge/env.txt
conda activate PJ-Challenge_compsoftware
```

Init postgres
```
initdb -D ~/pjchallenge/postgres
pg_ctl -D ~/pjchallenge/postgres -l logfile start

createuser --encrypted --pwprompt pjchallengeuser
```
This will ask for a password. Set the password as ```
pjchallengeuser```


```
createdb --owner=pjchallengeuser ~/pjchallenge/postgres

```
## Add boulders to the database

Add the boulder information (route id, color) in add_boulders.sql and run the following command on the command line.
```
psql -U pjchallengeuser -d postgres -a -f add_boulders.sql
```


### Init node
Initiate node using
```
npm init -y
npm install express
```

Then you can run the project using
```
node server.js 
```


When the competition is over, results have been published and you want to delete the installation from your device, run the following commands to stop postgres and remove the conda environment along with packages.
```
pg_ctl -D ~/pjchallenge/postgres stop
conda deactivate
conda remove --name PJ-Challenge_compsoftware --all -y
rm -rf ~/pjchallenge
```