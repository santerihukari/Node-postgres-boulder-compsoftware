# Boulder competition software with "koivukylä" score calculation

Initiates conda environment to ensure functioning package versions

Using postgres and node

## Quick setup

Install miniconda (only if you don't have conda installed already)
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
conda create -n PJ-Challenge_compsoftware --file env.txt
conda activate PJ-Challenge_compsoftware
```

Init postgres
```
initdb -D pjchallenge_db
pg_ctl -D pjchallenge_db -l logfile start

createuser --encrypted --pwprompt pjchallengeuser
```
This will ask for a password. Set the password as ```
pjchallengeuser```


```
createdb --owner=pjchallengeuser pjchallenge_db

```
Init node
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
pg_ctl -D pjchallenge_db -l logfile stop
conda deactivate
conda remove --name PJ-Challenge_compsoftware --all -y
rm -rf ~/pjchallenge
```

Packages that have been used to get the project working are shown below.
```
# packages in environment at /home/santeri/miniconda3/envs/PJ-Challenge_kisasofta:
#
# Name                    Version                   Build  Channel
_libgcc_mutex             0.1                 conda_forge    conda-forge
_openmp_mutex             4.5                       2_gnu    conda-forge
ca-certificates           2023.08.22           h06a4308_0    anaconda
icu                       73.2                 h59595ed_0    conda-forge
krb5                      1.20.1               h143b758_1    anaconda
libedit                   3.1.20221030         h5eee18b_0    anaconda
libgcc-ng                 13.2.0               h807b86a_2    conda-forge
libgomp                   13.2.0               h807b86a_2    conda-forge
libpq                     12.15                hdbd6064_1    anaconda
libstdcxx-ng              13.2.0               h7e041cc_2    conda-forge
libuv                     1.46.0               hd590300_0    conda-forge
libzlib                   1.2.13               hd590300_5    conda-forge
ncurses                   6.4                  h6a678d5_0    anaconda
nodejs                    20.8.1               h1990674_0    conda-forge
openssl                   3.1.4                hd590300_0    conda-forge
postgresql                12.15                h29ababe_1    anaconda
readline                  8.2                  h5eee18b_0    anaconda
zlib                      1.2.13               hd590300_5    conda-forge
```
