# Dockerización de una aplicación NodeJs a través de un DockerFile

1. Esta aplicación utiliza MongoDB por lo que deberá darse de alta en [mongoDB Atlas](https://www.mongodb.com/cloud/atlas) para tener la base de datos de forma remota. 

2. Deberá crear un clúster y conectar la base de datos con la app. Si no sabe como hacerlo puedes seguir este [tutorial](https://codeforgeek.com/mongodb-atlas-node-js)

3. En la raíz del proyecto tendrá que crear un fichero Dockerfile.

    3.1 Indicar la imagen que se va a descargar para realizar la dockerización.
    ```
    FROM node:latest
    ```
      
    3.2 Mostrar el directorio donde se alojará la app dentro de la imagen.
    ```
    WORKDIR /usr/src/app
    ```

    3.3 Se escriben las dependencias que se van a instalar:
    ```
    COPY package*.json ./
        
    RUN npm install
    ```
        
    3.4 El siguiente comando se usa par la agrupación del código fuente dentro de la imagen de docker:
    ```   
    COPY . .
    ```
        
    3.5 Se muestra el puerto en el que se expone la aplicación:
    ```   
    EXPOSE 3000
    ```

    3.6 Se arranza la aplicación:
    ```
    CMD [ "node", "./bin/www" ]
    ```

4. Crear un fichero .dockerignore para obviar la carpeta node_modules y npm-debug.log
    ```
    node_modules
    npm-debug.log
    ```
  
5. Crear una imagen contenida en el Dockerfile con el comando:
    ```
    docker build -t <your username>/node-weather-app .
    ```
 
6. Crear un contenedor:
    ```
    docker run --name dockerizar-weatherApp -p 49160:3000 -d <your username>/node-weather-app
    ```

7. Ejecute el siguiente comando para comprobar que todo ha ído correctamente
   ```
   docker logs dockerizar-weatherApp
   ```
