# Usar la imagen base de JRE 17 en Alpine
FROM eclipse-temurin:17-alpine

# Establecer el directorio de trabajo dentro del contenedor
# WORKDIR /app

# Crear un grupo llamado 'devopsc' y un usuario 'admin' que pertenezca a este grupo
RUN addgroup -g 1028 devopsc\
    && adduser -D -G devopsc admin 

VOLUME /tmp

# Argumento que acepta el nombre del JAR como parámetro en el momento de construir la imagen
ARG JAR_FILE

#Argumento para la contraseña de la base de datos.
ARG DB_PASSWORD
#Establece el valor del argumento en la variable de entorno.
ENV DB_PASSWORD=$DB_PASSWORD

# Copiar el JAR de Spring Boot al directorio de trabajo en el contenedor
COPY ${JAR_FILE} /tmp/app.jar

# Cambiar el propietario del directorio de trabajo al usuario 'admin'
RUN chown -R admin:devopsc /tmp

# Cambiar al usuario 'admin' (se ejecutará el proceso como este usuario)
USER admin

# Comando que se ejecutará al iniciar el contenedor
ENTRYPOINT ["java", "-jar", "/tmp/app.jar"]
