Copiado a lo bruto, y tuneando ligeramente, este articulo de medium  
https://medium.com/disney-streaming/setup-a-single-sign-on-saml-test-environment-with-docker-and-nodejs-c53fc1a984c9

### Descargamos la imagen Docker
```shell
docker pull kristophjunge/test-saml-idp
```

### Ejecutamos la imagen Docker (en este caso no la he puesto en modo daemon)
```shell
docker run — name=testsamlidp -p 8080:8080 -p 8443:8443 
-e SIMPLESAMLPHP_SP_ENTITY_ID= saml-poc 
-e SIMPLESAMLPHP_SP_ASSERTION_CONSUMER_SERVICE=http://localhost:4300/login/callback 
-d kristophjunge/test-saml-idp
```

### Preparamos la instalación de los paquetes node
```shell
npm install 
npm build
```

### Para terminar, arrancamos...
```shell
node index
```

Se puede consultar la página en http://localhost:4300  
Si accedemos a http://localhost:4300/login, se redireccionará a la página de login del servidor PHP con el IdP (el que se ha arrancado con Docker)

Una vez finalizado, el callback te devolverá al host original.  
Se puede ver el resultado por la consola (node)



### Los usuarios y contraseñas por defecto son estos
| UID | Username | Password  | Group  |       Email       |
|-----|----------|-----------|--------|-------------------|
|  1  |  user1   | user1pass | group1 | user1@example.com |
|  2  |  user2   | user2pass | group2 | user2@example.com |

