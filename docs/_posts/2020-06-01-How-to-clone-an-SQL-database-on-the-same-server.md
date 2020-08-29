---
title: How to clone an sql database on the same server
tags: sql mssql database
style: fill
color: info
description: fsdfsd
---

Although this should be straight forward, it took me some time to find an easy way to do it. Finally found it on [Stack Overflow](https://stackoverflow.com/a/22409447/2111052), therefore, I am documenting it here for (my) future reference.


    use [master]
    
    DECLARE @backupPath nvarchar(400);
    DECLARE @sourceDb nvarchar(50);
    DECLARE @sourceDb_log nvarchar(50);
    DECLARE @destDb nvarchar(50);
    DECLARE @destMdf nvarchar(100);
    DECLARE @destLdf nvarchar(100);
    DECLARE @sqlServerDbFolder nvarchar(100);
    
    SET @sourceDb = 'OriginalDb';
    SET @sourceDb_log = @sourceDb + '_log'
    SET @backupPath = 'c:\tmp\' + @sourceDb + '.bak' --ATTENTION: file must already exist and SQL Server must have access to it
    SET @sqlServerDbFolder = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\' -- The path to your Sql Server Folder 
    SET @destDb = 'NewDb'
    SET @destMdf = @sqlServerDbFolder + @destDb + '.mdf'
    SET @destLdf = @sqlServerDbFolder + @destDb + '_log' + '.ldf'
    
    BACKUP DATABASE @sourceDb TO DISK = @backupPath
    
    RESTORE DATABASE @destDb FROM DISK = @backupPath
    WITH REPLACE,
       MOVE @sourceDb     TO @destMdf,
       MOVE @sourceDb_log TO @destLdf
