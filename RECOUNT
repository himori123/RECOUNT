# ------------------------------------------------------------------------ #

echo "    ██████╗ ███████╗ ██████╗ ██████╗ ██╗   ██╗███╗   ██████████╗"
echo "    ██╔══██╗██╔════╝██╔════╝██╔═══██╗██║   ██║████╗  ██ ═██╔══╝"
echo "    ██████╔╝█████╗  ██║     ██║   ██║██║   ██║██╔██╗ ██║ ██║"    
echo "    ██╔══██╗██╔══╝  ██║     ██║   ██║██║   ██║██║╚██╗██║ ██║"    
echo "    ██║  ██║███████╗╚██████╗╚██████╔╝╚██████╔╝██║ ╚████║ ██║"  
echo "    ╚═╝  ╚═╝╚══════╝ ╚═════╝ ╚═════╝  ╚═════╝ ╚═╝  ╚═══╝ ╚═╝"   

      echo "ESTÁ FERRAMENTA TEM COMO OBJETIVO DE MINIMIZAR O TRABALHO DE PROFISSIONAIS BLUE TEAM"                                 

echo -e "\e[33m"
#----------------------------MENU INFORMAÇÃO ----------------------------------------- #
MENSAGEM_USO="
  $(basename $0) - [OPÇÕES]

      -h - Menu de ajuda
      -v - Versão do programa
      -s - Ordernar a saída
"
# ------------------------------------------------------------------------ #

VERSAO="v1.1"


 # ------------------------------- EXECUÇÃO ----------------------------------------- #
case "$1" in
  -h) echo "$MENSAGEM_USO" && exit 0    ;;
  -v) echo "$VERSAO" && exit 0          ;;
  -s) echo "$USUARIOS" | sort && exit 0 ;;
   *) echo "$USUARIOS"                  ;;
esac

if [ ! -f "/etc/snort/snort.conf" ]; then
  # Pergunta ao usuário se deseja instalar o Snort
  read -p "O Snort não está instalado no sistema. Deseja instalá-lo agora? (y/n) " choice

# Verifica a escolha do usuário
if [[ "$choice" =~ [yY](es)* ]]; then
  # Instala o Snort
  sudo apt-get update
  sudo apt-get install -y snort
fi
elif [[ "$choice" == [Nn] ]]; then
  echo "Instalação do Snort cancelada."
else
  echo "Escolha inválida. Apenas 'y', 'yes' ou 'n', 'no' são permitidos."
  exit 1
fi

# Faz o download das regras atualizadas
wget https://www.snort.org/downloads/community/community-rules.tar.gz

# Extrai o arquivo das regras
tar -xvzf community-rules.tar.gz -C /etc/snort/rules/

# Remove o arquivo das regras compactado
rm community-rules.tar.gz

# Adiciona as regras ao arquivo de configuração do Snort
echo "include \$RULE_PATH/community.rules" >> /etc/snort/snort.conf

# Reinicia o serviço do Snort para carregar as novas regras
systemctl restart snort

echo "Regras do Snort foram atualizadas com sucesso."
