# qual imagem selecionada
FROM debian

# informacao metadata
LABEL app="Apolo"
# variavel de ambiente
ENV APOLO="LINDO"

# execucao dentro da img
RUN apt-get update && apt-get install -y stress && apt-get clean

# comandos
CMD stress --cpu 1 --vm-bytes 64M --vm 1