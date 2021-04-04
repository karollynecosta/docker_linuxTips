FROM debian

RUN apt update && apt install -y apache
#OPCIONAL: dar permissao para  o usuario
#RUN chown deploy:deploy /var/lock && chown deploy:deploy /var/run && chown deploy:deploy /var/log
# variaveis de ambiente obrigatorias para o servico apache - descrito no dockerhub
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

# COPIAR O INDEX e colocar no html
COPY index.html /var/www/html/

LABEL description="Webserver"
LABEL version="1.0"

#OPCIONAL: usuario escolhido, padrão=root
#USER deploy

# repositorio inicial quando for montado
WORKDIR /var/www/html/

# montar esse caminho
VOLUME /var/www/html/

# porta para expor
EXPOSE 80

# principal processo do container, modo exec
ENTRYPOINT ["/usr/sbin/apache"]
CMD ["-D", "FOREGROUND"]