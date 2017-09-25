# Segurança no teu Raspberry Pi

A segurança do seu Raspberry Pi é importante. Falhas de segurança deixam o teu Raspberry Pi aberto para crackers que podem usá-lo sem a tua permissão.

Qual o nível de segurança que tu precisas depende de como tu desejas usar o teu Raspberry Pi. Por exemplo, se tu estiveres simplesmente usando o teu Raspberry Pi na tua rede doméstica, por trás de um roteador com um firewall, então já é bastante seguro por padrão.

No entanto, se tu desejares expor o tu Raspberry Pi diretamente à Internet, seja com conexão direta (improvável) ou deixando certos protocolos através do firewall do roteador (por exemplo, SSH), então você precisa fazer algumas mudanças de segurança básicas.

Mesmo que tu estejas escondido atrás de um firewall, é sensato levar a sério a segurança. Esta documentação descreverá algumas maneiras de melhorar a segurança do teu Raspberry Pi. Por favor, nota que não é exaustivo.

## Muda a tua senha padrão

O nome de usuário e a senha padrão são usados para cada Raspberry Pi executando o Raspbian. Então, se tu podes obter acesso a um Raspberry Pi, e essas configurações não foram alteradas, tu tens root nesse Raspberry Pi.

Então, a primeira coisa a fazer é mudar a senha. Isso pode ser feito através da aplicação raspi-config ou da linha de comando.

```
sudo raspi-config
```

Seleciona a opção 2 e segue as instruções para alterar a senha.

Na verdade, tudo o que o raspi-config é iniciar a aplicação de linha de comando passwd, que tu podes fazer a partir da linha de comando. Basta digitar a tua nova senha e confirmá-la.

```
passwd
```

## Mudanr o teu nome de utilizador

Tu podes, é claro, tornar o teu Raspberry Pi ainda mais seguro ao alterar o teu nome de utilizador. Todas os Raspberry Pis vêm com o nome de utilizador padrão, então, mudar isso irá tornar o teu Raspberry Pi mais seguro.

Para adicionar um novo utilizador com as mesmas permissões do usuário `pi`

```
sudo useradd -m fred -G sudo
```

Isso adiciona um novo utilizador com o nome de `fred`, cria uma pasta inicial e adiciona o utilizador ao grupo `sudo`. Agora tu precisas de definir uma senha para o novo utilizador:

```
sudo passwd fred
```

Faz o terminar sessão e faz login com os novos detalhes da conta. Verifica se as tuas permissões estão em vigor (ou seja, tu podes fazer sudo) tentando o seguinte.

```
sudo visudo
```

O comando `visudo` só pode ser executado por uma conta com privilégios sudo. Se o comando for executado com sucesso, então tu podes ter certeza de que a nova conta está no grupo `sudo`.

Depois de confirmar que a nova conta está a funcionar, tu podes excluir o utilizador `pi`. Por favor, nota que, com a atual distribuição Raspbian, existem alguns aspectos que exigem que o usuário do Pi esteja presente. Se tu não tens certeza se vais ser afetado por isso, então deixa o utilizador pi a funcionar. O trabalho está sendo feito para reduzir a dependência do utilizador do `pi`.

Para excluir o utilizador `pi`, digita o seguinte:

```
sudo deluser pi
```

Este comando irá excluir o utilizador `pi`, mas deixará a pasta `home/pi`. Se necessário, tu podes usar o comando abaixo para remover a pasta inicial do utilizador do pi ao mesmo tempo. Observa que os dados nesta pasta serão excluídos permanentemente, portanto, certifica-te de que todos os dados necessários estão armazenados em outro lugar.

```
sudo deluser -remove-home pi
```

## Fazer `sudo` o exigir uma senha

A colocação de `sudo` atrás de um comando faz com que seja executado como um super utilizador e, por padrão, não precisa de senha. Em geral, isso não é um problema. No entanto, se o teu Pi estiver exposto à Internet e de alguma forma, for explorado (talvez através de uma falha da página da Web, por exemplo), o invasor poderá alterar as coisas que exigem credenciais de super utilizador, a menos que tu configures o `sudo` para exigir uma senha.

Para forçar o `sudo` a exigir uma senha, digita

```
sudo nano /etc/sudoers.d/010_pi-nopasswd
```

e altere a linha do `pi` (ou qualquer nome de utilizador que tenha direitos de super utilizador) para

```
pi ALL=(ALL) PASSWD: ALL
```

Depois de alterado, não te esqueças de gravar o ficheiro.

## Certifica-te que tens as ultimas correcções de segurança

Isso pode ser tão simples como garantir que a tua versão do Raspbian está actualizada, uma vez que uma distribuição actualizada contém todas as últimas correcções de segurança. Instruções completas podem ser encontradas [aqui](../raspbian/updating.md).

If you are using SSH to connect to your Raspberry Pi, it can be worthwhile to add a cron job that specifically updates the ssh-server. The following command, perhaps as a daily cron job, will ensure you have the latest SSH security fixes promptly, independent of your normal update process. More information on setting up cron can be found [here](../linux/usage/cron.md)

Se tu estiveres a utilizar o SSH para te conectares ao teu Raspberry Pi, pode valer a pena adicionar um trabalho cron que actualiza especificamente o servidor ssh. O seguinte comando, talvez como um trabalho cron diário, assegurará que tu tens as últimas correcções de segurança SSH prontamente, independentemente do teu processo de actualização normal. Mais informações sobre como configurar o cron podem ser encontradas [aqui][here](../linux/usage/cron.md)

```
apt-get install openssh-server
```

## Melhorar a segurança SSH

SSH é uma maneira comum de acessar um Raspberry Pi remotamente. Por padrão, efectuar login com o SSH requer a combinação do nome de utilizador / senha e existem maneiras de tornar isso mais seguro. Um método ainda mais seguro é usar a autenticação baseada em chave.

### Melhorar a segurança do utilizador/senha

A coisa mais importante a fazer é garantir que tu tens uma senha muito robusta. Se o teu Raspberry Pi estiver exposto à Internet, a senha precisa ser muito segura. Isso ajudará a evitar ataques de dicionário ou similares.

Tu também podes **permitir** ou **negar** utilizadores específicos alterando a configuração do `sshd`.

```
sudo nano /etc/ssh/sshd_config
```

Adiciona, edita ou anexe ao final do ficheiro a seguinte linha, que contém os nomes de utilizador que tu desejas permitir para fazer login:

```
AllowUsers edward andrew charles anne
```

Tu também podes usar o negar utilizadores (DenyUsers) para impedir especificamente alguns nomes de utilizador de fazer login:

```
DenyUsers harry william
```

Após a alteração, você precisará reiniciar o serviço `sshd` usando `sudo systemctl restart ssh` ou reiniciar para que as mudanças entrem em vigor.

### Autenticação por um par de chaves

Os pares de chaves são duas chaves criptográficamente seguras. Uma é privada e uma é pública. Elas podem ser usadas para autenticar um cliente em um servidor SSH (neste caso o Raspberry Pi).

O cliente gera duas chaves, que estão criptograficamente ligadas uma à outra. A chave privada nunca deve ser liberada, mas a chave pública pode ser compartilhada sem problemas. O servidor SSH tira uma cópia da chave pública e, quando um link é solicitado, usa esta chave para enviar uma mensagem de desafio ao cliente, que o cliente irá criptografar usando a chave privada. Se o servidor pode usar a chave pública para descriptografar esta mensagem de volta para a mensagem de desafio original, a identidade do cliente pode ser confirmada.

Gerar um par de chaves no Linux é feito usando o comando `ssh-keygen` no **cliente**. As chaves são armazenadas por padrão na pasta `.ssh` disponíveis na pasta inicial do utilizador. A chave privada será chamada `id_rsa` e a chave pública associada será chamada `id_rsa.pub`. A chave terá 2048 bits de comprimento: quebrar a criptografia em uma chave desse comprimento levaria um tempo extremamente longo, por isso é muito seguro. Você pode fazer chaves mais longas se a situação o exigir. Observe que você só deve fazer o processo de geração uma vez: se repetido, ele substituirá as chaves geradas anteriores. Qualquer coisa confiando nessas chaves antigas precisará ser actualizada para as novas chaves.

Tu serás solicitado a fornecer uma senha secreta durante a geração de chaves: este é um nível de segurança extra. Por enquanto, deixe este em branco.

The public key now needs to be moved on to the server. This can be done by email, or cut and paste, or file copying. Once on the server it needs to be added to the SSH systems authorised keys. It should be emphasised that the `id_rsa` file is the private key and SHOULD NOT LEAVE THE CLIENT, whilst the public key file is `id_rsa.pub`.


A chave pública agora precisa ser movida para o servidor. Isso pode ser feito por e-mail, ou cortar e colar, ou copiar os ficheiros. Uma vez colocada no servidor, a chave precisa ser adicionado às chaves autorizadas dos sistemas SSH. Deve-se relembrar que o ficheiro `id_rsa` é a chave privada e NÃO DEIXA O CLIENTE, enquanto o ficheiro de chave pública é `id_rsa.pub`.

Adicione a nova chave pública ao ficheiro de autorização da seguinte maneira:

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

Alternativamente, tu podes editar o ficheiro `sudo nano ~/.ssh/authorized_keys` e copiar / colar a chave. É perfeitamente aceitável ter múltiplas entradas no ficheiro authorized_keys, portanto o SSH pode suportar vários clientes.

Observe que o ficheiro authorized_keys precisa das permissões corretas para serem lidas correctamente pelo sistema `ssh`.

```
sudo chmod 644 ~/.ssh/authorized_keys
```

Finalmente, precisamos desactivar os logins de senhas, de modo a que toda autenticação seja feita pelos apenas por utilização dos pares de chaves.

```
sudo nano /etc/ssh/sshd_config
```

Existem três linhas que precisam ser alteradas para `no` caso não estejam escritas já dessa forma:

```
ChallengeResponseAuthentification no
PasswordAuthentification no
UsePAM no
```

Grava o ficheiro e reinicie o sistema ssh com o comando `sudo service ssh reload` ou reboot.

## Instalar uma firewall

Existem muitas soluções de firewall disponíveis para Linux. A maioria usa o projecto subjacente [iptables](http://www.netfilter.org/projects/iptables/index.html) para fornecer filtragem de pacotes. Este projecto se enquadra no sistema de filtragem de rede do Linux. O `iptables` está instalado por padrão no Raspbian, mas não está configurado. Configurá-lo pode ser uma tarefa complicada, e um projeto que fornece uma interface mais simples do que o `iptables` é o [ufw](https://www.linux.com/learn/introduction-uncomplicated-firewall-ufw), que significa "Unconplicated Fire Wall". Esta é a ferramenta de firewall padrão no Ubuntu, e pode ser facilmente instalada no teu Raspberry Pi:

```
sudo apt-get install ufw
```

`ufw` é uma ferramenta de linha de comando bastante direta, embora existam algumas GUIs disponíveis. Este documento descreverá algumas das opções básicas da linha de comando. Observa que o `ufw` precisa de ser executado com privilégios de super utilizador (`sudo`), então todos os comandos são precedidos de sudo. Também é possível usar a opção `--dry-run` em qualquer comando do `ufw`, que indica os resultados do comando sem realmente fazer alterações.

Para activar a firewall, de forma a que também garantir que ela será iniciada no boot, usa:

```
sudo ufw enable
```

Para desactivar a firewall e desactivar a inicialização no boot, usa:

```
sudo ufw disable
```

Permita que uma determinada porta tenha acesso (usamos a porta 22 no nosso exemplo):

```
sudo ufw allow 22
```

Negar o acesso em uma porta também é muito simples (novamente, usamos a porta 22 como exemplo):

```
sudo ufw deny 22
```

Tu também pode especificar qual o serviço que estás a permitir ou a negar em uma porta. Neste exemplo, estamos negando tcp na porta 22:

```
sudo ufw deny 22/tcp
```
Tu podes especificar o serviço, mesmo que não saibas qual a porta que usa. Este exemplo permite o acesso do serviço ssh através da firewall:

```
sudo ufw allow ssh
```

O comando de status lista todas as configurações actuais na firewall:

```
sudo ufw status
```

As regras podem ser bastante complicadas, permitindo que endereços IP específicos sejam bloqueados, especificando em que direcção o tráfego é permitido ou limitando o número de tentativas de conexão, por exemplo, para ajudar a derrotar um ataque de Negação de Serviço (DoS). Tu também podes especificar as regras do dispositivo a serem aplicadas (por exemplo, eth0, wlan0). Consulta a página do manual do `ufw` (`man ufw`) para detalhes completos, mas aqui estão alguns exemplos de comandos mais sofisticados.

Limite as tentativas de login na porta ssh usando tcp: isso nega conexão se um endereço IP tentou se conectar seis ou mais vezes nos últimos 30 segundos:

```
sudo ufw limit ssh/tcp
```

Negar o acesso à porta 30 a partir do endereço IP 192.168.2.1

```
sudo ufw deny from 192.168.2.1 port 30
```

## Instalar fail2ban

Se você estiver usando seu Raspberry Pi como algum tipo de servidor, por exemplo, um ```ssh``` ou servidor web, a tua firewall terá "buracos" deliberados para permitir o tráfego do servidor. Nestes casos, [Fail2ban](http://www.fail2ban.org) pode ser útil. Fail2ban, escrito em Python, é um scanner que examina os ficheiros de log produzidos pelo Raspberry Pi e verifica se está a decorrer alguma atividade suspeita. Ele detecta coisas como tentativas de força bruta para iniciar sessão e pode informar qualquer firewall instalado para impedir novas tentativas de login dos endereços IP suspeitos. Ele salva-te de ter que verificar manualmente os arquivos de log para tentativas de intrusão e, em seguida, actualizar o firewall (via `iptables`) para preveni-los.

Instala o Fail2ban usando o seguinte comando:

```
sudo apt-get install fail2ban
```

Observa que a versão do Fail2ban no repositório (v0.8.13) não suporta redes IPv6. Se tu estiveres a usar IPv6, tu vais precisar de instalar a versão v0.10 ou superior da fonte. Consulta o site [Fail2ban](http://www.fail2ban.org) para obter mais informações sobre como fazer isso.

Quando estiveres a instar o Fail2ban cria uma pasta /etc/fail2ban em que há um ficheiro de configuração chamado `jail.conf`. Esse ficheiro precisa de ser copiado para `jail.local` para activar o mesmo. Dentro deste ficheiro de configuração estão um conjunto de opções padrão, juntamente com opções para verificar serviços específicos para anormalidades. Faz o seguinte para examinar/alterar as regras que são usadas para `ssh`:

```
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
```

Procura a sessão `[ssh]`. Vai ser parecido a isto.

```
[ssh]
enabled  = true
port     = ssh
filter   = sshd
logpath  = /var/log/auth.log
maxretry = 6
```

Como podes ver, esta sessão é chamada ssh, está activada, examina a porta ssh, filtros usando os parâmetros `\etc\fail2ban\filters.d\sshd.conf`, analisa o /var/log/auth.log por actividades mal-intencionadas e permite seis tentativas antes que o limite de detecção seja atingido. Ao verificar a sessão padrão, podemos ver que a acção de proibição padrão é:

```
# Default banning action (e.g. iptables, iptables-new,
# iptables-multiport, shorewall, etc) It is used to define
# action_* variables. Can be overridden globally or per
# section within jail.local file
banaction = iptables-multiport
```

`iptables-multiport` significa que o sistema Fail2ban executará o arquivo `/etc/fail2ban/action.d/iptables-multiport.conf` quando o limite de detecção for atingido. Existem vários ficheiros de configuração de acção diferentes que podem ser usados. O Multiport proíbe todo o acesso em todas as portas.


Se tu desejares proibir permanentemente um endereço IP após três tentativas falhadas, tu podes alterar o valor maxretry na secção `[ssh]` e definir o tempo que vai ser banido (bantime) para um número negativo:

```
[ssh]
enabled  = true
port     = ssh
filter   = sshd
logpath  = /var/log/auth.log
maxretry = 3 
bantime = -1
```

Há um bom tutorial sobre alguns dos detalhes do Fail2ban [aqui](https://www.digitalocean.com/community/tutorials/how-fail2ban-works-to-protect-services-on-a-linux-server).
