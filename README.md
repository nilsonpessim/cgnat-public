## :rocket: ISP Manager
:star_struck: Repositório de Instalação e Configuração do ISP Manager
 
## :computer: Requisitos do Sistema
Requisitos para execução do ISP Manager.
 
* :cd: Ubuntu 22.04 Server (ISO ou CT).
* :heavy_check_mark: Processador: 2 vCPU.
* :heavy_check_mark: Memória RAM: 2GB.
* :heavy_check_mark: Armazenamento: 30GB.
* :heavy_check_mark: PHP 8.2+ e MySQL.
* :heavy_check_mark: IP Público + Subdomínio [Para gerar o certificado SSL].

## :cd: Preparação do Ubuntu 22.04
Pacotes necessários para o Ubuntu.

* Atualize os Repositórios e Pacotes:
``` 
apt update && apt -y upgrade
```

* Ajuste de Data/Hora (America/Sao_Paulo):
``` 
dpkg-reconfigure tzdata 
```

## :package: Instalação dos Pacotes
Pacotes necessários para o Software.

* Servidor Web e Banco de Dados:
``` 
apt -y install apache2 unzip libapache2-mod-php php mariadb-client mariadb-server
apt -y install php-gmp php-mysql php-mbstring php-gd php-curl php-xml php-pear
```

* Regras de Reescrita:
``` 
a2enmod rewrite
systemctl restart apache2
```

```nano /etc/apache2/apache2.conf```
Dentro de <Directory /var/www/>, altere ```AllowOverride None``` para ```AllowOverride All```


## :hammer_and_wrench: Configuração do Software
Configuração do Software.

* [Aplicação] - Importar Arquivos de Instalação:
```
cd /var/www/html/
rm -rf *
wget https://cgnat.techlabs.net.br/install.zip
unzip install.zip
```

* [Banco de Dados] - Importar Schema:
```
cd /var/www/html/
mysql -uroot -p < cgnat.sql
```

* [Segurança] - Remover Arquivos de Instalação:
```
cd /var/www/html
rm install.zip && rm cgnat.sql
```

* [Segurança] - Ajustar Permissão da ExportCGNAT:
```
cd /var/www/html/
chmod 777 files/
```

* [Segurança] - Proteção do Apache:
```
sed -i 's/ServerTokens OS/ServerTokens Prod/' /etc/apache2/conf-available/security.conf
sed -i 's/ServerSignature On/ServerSignature Off/' /etc/apache2/conf-available/security.conf
```

## :dizzy: Configuração SSL
Configuração do SSL para Apache

* Instalar LetsEncrypt:
```
apt install letsencrypt python-certbot-apache
apache2ctl stop
letsencrypt --authenticator standalone --installer apache -n --agree-tos --email mail@example.com -d example.com
```

Para forçar o SSL na URL é necessário descomentar as seguintes linhas nos arquivo .htaccess
```
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```


## :key: Acessando o Sistema
Acesso Padrão do Sistema

:pouting_man: Usuário: admin

:lock: Senha: admin

## :1234: Versão do Sistema

```Versão 0.0.1```

## :sparkling_heart: Nos Ajude a Crescer
>Se este Material foi útil para você, ajude se inscrevendo no meu canal do YouTube.
>
>(https://youtube.com/techlabs94?sub_confirmation=1)
> 
>Isso me incentiva a trazer mais materiais como este e muitos outros de redes e tecnologia.
> 
>## ![YouTube Channel Subscribers](https://img.shields.io/youtube/channel/subscribers/UCWN6suTq5sZGqnSLos992Yw?style=social)
