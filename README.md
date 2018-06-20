# OracleAudit

These are queries to help assist with retrieving users inside of a SQL instance and the permissions that those users are assigned.  These queries are designed to only read data and will not modify or create data inside of the database.

## **Oracle - Users and Account Status**

The following queries have been designed to **NOT** pull password hashes out of the DBA_USERS table.  Due to differences in table structure between Oracle versions please run the query that is appropriate to your environment.

### ORACLE ***18***

``` SQL
    SELECT USERNAME, USER_ID, ACCOUNT_STATUS, LOCK_DATE,
        EXPIRY_DATE, CREATED, EXTERNAL_NAME, PASSWORD_VERSIONS,
        EDITIONS_ENABLED, AUTHENTICATION_TYPE, PROXY_ONLY_CONNECT,
        COMMON, LAST_LOGIN, ORACLE_MAINTAINED, INHERITED, IMPLICIT
    FROM DBA_USERS
```

### ORACLE ***12***

``` SQL
    SELECT USERNAME, USER_ID, ACCOUNT_STATUS, LOCK_DATE,
        EXPIRY_DATE, CREATED, EXTERNAL_NAME, PASSWORD_VERSIONS,
        EDITIONS_ENABLED, AUTHENTICATION_TYPE, PROXY_ONLY_CONNECT,
        COMMON, LAST_LOGIN, ORACLE_MAINTAINED, INHERITED, IMPLICIT
    FROM DBA_USERS
```

### ORACLE ***11***

``` SQL
SELECT USERNAME, USER_ID, ACCOUNT_STATUS, LOCK_DATE,
    EXPIRY_DATE, CREATED, EXTERNAL_NAME, PASSWORD_VERSIONS,
    EDITIONS_ENABLED, AUTHENTICATION_TYPE
    FROM DBA_USERS
```

### ORACLE ***10***

``` SQL
SELECT USERNAME, USER_ID, ACCOUNT_STATUS, LOCK_DATE,
    EXPIRY_DATE, CREATED, EXTERNAL_NAME
    FROM DBA_USERS
```

### ORACLE ***9***

``` SQL
SELECT USERNAME, USER_ID, ACCOUNT_STATUS, LOCK_DATE,
    EXPIRY_DATE, CREATED, EXTERNAL_NAME
    FROM DBA_USERS
```

## **Oracle - System Privilege Grants**

The following query determines what System Privileges allow the user to perform system level activities.

``` SQL
SELECT *
    FROM DBA_SYS_PRIVS
```

## **Oracle - Role Grants**

The following query lists the roles granted to all users and roles in the database.

``` SQL
SELECT *
    FROM DBA_ROLE_PRIVS
```

## **Oracle - Roles**

The following query lists all roles that exist in the database.

``` SQL
SELECT *
    FROM DBA_ROLES
```

## **Oracle - Users Granted SYSDBA or SYSOPER**

The following query determines what users are granted SYSDBA, SYSOPER, SYSASM, SYSBACKUP, SYSDG, and SYSKM privileges.

``` SQL
SELECT *
    FROM V$PWFILE_USERS
```