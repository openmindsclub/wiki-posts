# Oracle 18c XE Installation Guide On Archlinux Host

**Important Disclaimer:** Read the entirety of the guide first before engaging in the installation process. Don’t skip any parts unless you know what you’re doing! If you have any questions, you are free to contact me. This is a beginner's guide so the purpose is to break down and explain each step in details so if you think this guide lacks information, feel free to write an issue to let me know.

## Clone git repository

```
git clone https://aur.archlinux.org/oracle-xe.git
cd oracle-xe
```

## Download oracle-database-xe-18c-1.0-1.x86_64-rpm.zip

```
wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-18c-1.0-1.x86_64.rpm
```

## Installation

```
makepkg -si
```

## Run configuration

As the your terminal prompt suggests, you need to run the following command to configure your oracle 18c XE database:

```
su -s /bin/bash oracle -c '/opt/oracle/product/18c/dbhomeXE/bin/dbca -silent \
-createDatabase -gdbName XE -templateName XE_Database.dbc -characterSet AL32UTF8 \
-createAsContainerDatabase true -numberOfPDBs 1 -sid XE -pdbName XEPDB1 \
-J-Doracle.assistants.dbca.validate.ConfigurationParams=false -emConfiguration DBEXPRESS \
-emExpressPort 5500 -J-Doracle.assistants.dbca.validate.DBCredentials=false -sampleSchema true \
-customScripts /opt/oracle/product/18c/dbhomeXE/assistants/dbca/postdb_creation.sql'
```

Type in and confirm the password for the administrative accounts, `SYS`, `SYSTEM` and `PDBADMIN`, and hit Enter.

After the command has finished, the Oracle Database 18c XE is fully configured and ready to use.

## Connecting to Oracle Database 18c XE

To fire up the SQL prompt for your user, you will have to make sure that `$ORACLE_HOME` is set and `$ORACLE_HOME/bin` is in your `$PATH`. There is a utility script called `oraenv`, that will configure that for you. All you have to do is to call it on your local shell and pass on the `$ORACLE_SID`, which is `XE` in this example:

```
[lilly@localhost ~]$ . oraenv
ORACLE_SID = [lilly] ? XE
ORACLE_BASE environment variable is not being set since this
information is not available for the current user ID lilly.
You can set ORACLE_BASE manually if it is required.
Resetting ORACLE_BASE to its previous value or ORACLE_HOME
The Oracle base has been set to /opt/oracle/product/18c/dbhomeXE
```

Once you have done that you can connect via the SQL prompt. The format for the connect string is:
`[user]/[password]@//[hostname]:[port]/[DB name] [AS [role]]`

Preview:

```
[lilly@localhost ~]$ sqlplus SYS/password1234@//localhost:1521/myDB as SYSDBA
```

If you run into an error at the time of running `oraenv`, make sure to check again if you are on the right directory.

## Create a new user and granting permissions

While trying to create a user in Oracle 18c XE, I kept getting an `ORA-65096: invalid common user or role name` error, which didn’t make sense to me so after validating my command seeing as that my SQL command was formatted correctly. I did some research and determined that the hidden parameter “\_ORACLE_SCRIPT” needed to be set to “True” starting with the Oracle Version 12c and higher, as such:

```
SQL> alter session set "_ORACLE_SCRIPT"=true;
```

Once the `_ORACLE_SCRIPT` hidden variable to `True`, you will be able to create the desired user and run your grants commands as usual with:

```
SQL> create user USERNAME identified by PASSWORD;
SQL> grant CREATE SESSION, ALTER SESSION, CREATE DATABASE LINK, CREATE MATERIALIZED VIEW, CREATE PROCEDURE, CREATE PUBLIC SYNONYM, CREATE ROLE, CREATE SEQUENCE, CREATE SYNONYM, CREATE TABLE, CREATE TRIGGER, CREATE TYPE, CREATE VIEW, UNLIMITED TABLESPACE to USERNAME;
```

**Important Disclaimer:** `_ORACLE_SCRIPT` is an undocumented parameter. Use with caution, you never know when it might behave differently, not at all or just get dropped in a future release. So use it at your own risk, convenience and wisely. Avoid this step if you don't need to create a user in your container.

## Check tables

```
select table_name from user_tables;
```

## Logout

```
exit
```

## Login

The format for the connect string is:
`[user]/[password]@//[hostname]:[port]/[DB name] [AS [role]]`

## Ressources

https://aur.archlinux.org/packages/oracle-xe/
