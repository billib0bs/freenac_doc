# freenac_doc
## Документация по FreeNAC
### Настройка GUI доступа с помощью vmps.exe.

Если сделано все по инструкции в MySQL должен быть пользователь invenwrite, этот пользователь имеет полный доступ к БД opennac.
Работа с помощью vmps.exe с БД осуществляется с помощью этого пользователя. Для того чтобы иметь подключение к БД необходимо сгенерировать хеш пароля данного пользователя. Для этого запускаем vmps.exe

Admin -> Encrypt user

Enter username: **admin**

Enter password: **admin**

Generate Key

Generate Key: **/jpwJvRwN5TwmS8=**

```xml
<vmps>
  <comment c="Sample vmps.xml configuration file for the NAC gui vmps.exe with Demo company. Change the server IP as appropriate"/>
  
  <settings company="Kolobok"  StaticInvEnabled="0" NmapEnabled="1" AntiVirusEnabled="0"
  PatchCableEnabled="1"/>
	<mysql server="192.168.1.1" port="3306" 
        auth="/jpwJvRwN5TwmS8=" database="opennac" />
	<mssql-inv server="UnusedServer\UnusedInstance"  
        auth="XX" database="YYY" />        	
</vmps>
```

Добавляем пользователя админа, username должен соответствовать тому пользователя из под имени которого будет запускаться vmps:
```mysql
insert into opennac.users (username, Surname, GivenName, nac_rights) values
('jsmith', 'John', 'Smith', 99);
```

После этого запускаем vmps.exe
