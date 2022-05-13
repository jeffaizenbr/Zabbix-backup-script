# Zabbix-backup-script

```bash
vim /backup/script.sh
```
```bash
chmod +x script.sh
```

```bash
#!/bin/bash

#################### SCRIPT PARA BACKUP MYSQL ZABBIX ####################
# Jefferson de S. Silva                            #
# Created Maio 2022                                                #
                                                    #
# Excluindo ultimo arquivo
find /backup -type f -mtime +1 -exec rm -rf {} \;


# Gerando arquivo sql
mysqldump --add-drop-table -u root -pPASSWORD -x -e -B zabbix_db > /backup/zabbix.sql

# Compactando o arquivo
gzip /backup/zabbix.sql


# Testando arquivo
if gzip -t /backup/zabbix.sql.gz
then
echo "0"

else

echo "1"
fi
# Renomeando

mv /backup/zabbix.sql.gz /backup/$(date +%F)zabbix.sql.gz
```
