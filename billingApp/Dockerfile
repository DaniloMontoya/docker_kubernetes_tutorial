FROM nginx:stable-alpine

 # use a volume is mor efficient and speed that filesystem
VOLUME /tmp

# RUN es para ejecutar un comando.
#Install web app on nginx server
RUN rm -rf /usr/share/nginx/html/*

COPY nginx.conf /etc/nginx/nginx.conf
COPY dist/billingApp /usr/share/nginx/html
COPY mime.types /etc/nginx/mime.types

# Comando de alpine para hacer la instalacion de JAVA 17
# Instalamos OpenJDK 17
RUN apk --no-cache add openjdk17-jre

# Definimos la variable de entorno JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-17-openjdk
ENV PATH $JAVA_HOME/bin:$PATH

# Verificamos la instalación
RUN java -version


#Install java microservice
ENV JAVA_OPTS=""
# Los ARG (argumento) funciona para cuando yo valla a construir la image de docker poder pasarselo a la hora de construir la imagen.
ARG JAR_FILE
ADD ${JAR_FILE} app.jar

#Copy the init script
COPY appshell.sh appshell.sh

#The ports 7080 for backend-app and 80 for web app
EXPOSE 80 7080

ENTRYPOINT ["sh", "/appshell.sh"]