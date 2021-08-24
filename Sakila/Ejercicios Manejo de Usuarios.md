# Ejercicios Manejo de Usuarios

## Lucas Pasolli

## Exercises

1. Create a user **data_analyst**

```sql
CREATE USER data_analyst;
```

2. Grant permissions only to SELECT, UPDATE and DELETE to all sakila tables to it.

```sql
GRANT SELECT, UPDATE, DELETE ON *.* TO data_analyst;
SHOW GRANTS FOR data_analyst;
```

3. Login with this user and try to create a table. Show the result of that operation.
4. Try to update a title of a film. Write the update script.
5. With **root** or any admin user revoke the UPDATE permission. Write the command
6. Login again with **data_analyst** and try again the update done in step 4. Show the result.
