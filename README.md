# Debezuim_SQLServer_Connect
Using kafka,  Debezium and sql server cdc  to setup change tracking and create kafka payload

Step 1
docker-compose -f docker-compose-sqlserver.yaml up


step 2
Get-Content inventory.sql | docker-compose -f docker-compose-sqlserver.yaml exec -T sqlserver bash -c "/opt/mssql-tools/bin/sqlcmd -U sa -P Password!"


step 3
docker-compose -f docker-compose-sqlserver.yaml exec sqlserver bash -c '/opt/mssql-tools/bin/sqlcmd -U sa -P $SA_PASSWORD -d testDB'

step 4
update products_on_hand set quantity = quantity +1 where product_id = '101';
go

step 5
verify payload in kafka