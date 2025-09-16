## ORACLEDB-EX-02
This repository explains how I completed and run the ORACLEDB-EX-02 assignment: running Oracle Database Express Edition inside a Docker container and connecting via SQLPlus to verify the setup.


## Build the Oracle XE Docker Image
git clone https://github.com/oracle/docker-images.git
cd docker-images/OracleDatabase/SingleInstance/dockerfiles
./buildContainerImage.sh -v 21.3.0 -x

This builds the oracle/database:21.3.0-xe image locally.

## Start the Container
Run the container with ports mapped and a default password:(Password and username that in the homework file.)

docker run --name oraclexe -p 1521:1521 -p 5500:5500 \
  -e ORACLE_PWD=ORACLE oracle/database:21.3.0-xe

docker logs -f oraclexe

## Connect via SQLPlus
First, lets open a bash shell inside the container;
docker exec -it oraclexe bash

Then, we should connect with SQLPlus:
sqlplus sys/ORACLE as sysdba

<img width="683" height="279" alt="Screenshot 2025-09-16 at 14 37 06" src="https://github.com/user-attachments/assets/57cf933e-59cb-4199-979a-79960ea38385" />

## Run Verification Queries
select name from v$database;

Seen Output:
NAME 
---------
FREE

We can also check the versiın of the database version:
select * from v$version;

<img width="789" height="369" alt="Screenshot 2025-09-16 at 14 46 58" src="https://github.com/user-attachments/assets/51a49672-2636-48b1-a831-4f44ecba4253" />

Seen Output;
BANNER
--------------------------------------------------------------------------------
BANNER_FULL
--------------------------------------------------------------------------------
BANNER_LEGACY
--------------------------------------------------------------------------------
    CON_ID
----------
Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free
Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free
Version 23.9.0.25.07
Oracle Database 23ai Free Release 23.0.0.0.0 - Develop, Learn, and Run for Free
	 0

BANNER
--------------------------------------------------------------------------------
BANNER_FULL
--------------------------------------------------------------------------------
BANNER_LEGACY
--------------------------------------------------------------------------------
    CON_ID
----------

## Exit and Finish
Just type "exit;" to close and leave the database.
<img width="783" height="106" alt="Screenshot 2025-09-16 at 14 47 42" src="https://github.com/user-attachments/assets/861dd103-8fd4-4850-b2fd-690fe7862ea4" />

After that to remove the container:

docker stop oraclexe
docker rm oraclexe
