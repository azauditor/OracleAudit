# OracleAudit

These are queries to help assist with retrieving users inside of a SQL instance and the permissions that those users are assigned.  These queries are designed to only read data and will not modify or create data inside of the database.

## **Oracle - Version Check**
The following queries may assist you in determining your version of Oracle database if you are unsure. The version of the database will impact the queries you will need to run for "Users and Account Status", listed further below.

``` SQL
SELECT 'Oracle/Version' as ScriptName, * 
FROM v$version
```

``` SQL
SELECT 'Oracle/PCV' as ScriptName, * 
FROM product_component_version
```

``` SQL
SELECT 'Oracle/Instance' as ScriptName, INSTANCE_NAME, HOST_NAME, VERSION, STATUS, LOGINS,
    DATABASE_STATUS, INSTANCE_ROLE, CON_ID
FROM V$INSTANCE
```

## ***Password Settings***

The following query will show the password settings for all profiles in the database.

``` SQL
SELECT 'Oracle/Password Settings' as ScriptName, PROFILE, RESOURCE_NAME, LIMIT
FROM DBA_PROFILES
WHERE RESOURCE_TYPE = 'PASSWORD'
ORDER BY PROFILE
```

## **Oracle - Users and Account Status**

The following query has been designed to **NOT** pull password hashes out of the DBA_USERS table.

``` SQL
SELECT 'Oracle/User Account Status' as ScriptName, USERNAME, USER_ID, PROFILE, ACCOUNT_STATUS, LOCK_DATE,
    EXPIRY_DATE, LAST_LOGIN, ORACLE_MAINTAINED
FROM DBA_USERS
```

## **Oracle - System Privilege Grants**

The following query determines what System Privileges allow the user to perform system level activities.

``` SQL
SELECT 'Oracle/System Privilege Grants' as ScriptName, GRANTEE, PRIVILEGE, ADMIN_OPTION
FROM DBA_SYS_PRIVS
```

## **Oracle - Role Grants**

The following query lists the roles granted to all users and roles in the database.

``` SQL
SELECT 'Oracle/Role Grants' as ScriptName, GRANTEE, GRANTED_ROLE, ADMIN_OPTION
FROM DBA_ROLE_PRIVS
```

## **Oracle - Roles**

The following query lists all roles that exist in the database.

``` SQL
SELECT 'Oracle/Roles' as ScriptName, ROLE, ROLE_ID, PASSWORD_REQUIRED, AUTHENTICATION_TYPE, ORACLE_MAINTAINED
FROM DBA_ROLES
```

## **Oracle - PW_File Users**

The following query determines what users are granted SYSDBA, SYSOPER, SYSASM, SYSBACKUP, SYSDG, and SYSKM privileges.

``` SQL
SELECT 'Oracle/PWFile' as ScriptName, USERNAME, SYSDBA, SYSOPER, SYSBACKUP, SYSKM, SYSDG, SYSASM
FROM V$PWFILE_USERS
```
