# Lab Nível 0: Linux na Cibersegurança

Neste laboratório, você vai entender por que o Linux é o sistema operacional padrão da área de cibersegurança, como preparar o seu ambiente de testes com Máquina Virtual e os comandos práticos essenciais no terminal.

---

## 1. Por que usamos Linux em Cibersegurança?

Embora o Windows e o macOS sejam excelentes para o uso diário, o Linux reina absoluto na cibersegurança e no ecossistema de servidores.

### 🛡️ Máquina Virtual (VM) vs. Ambiente Virtual (Virtualenv / VS Code)
* **Isolamento de Segurança (Sandbox Real):** Quando você executa testes de segurança ou analisa um artefato suspeito, uma *virtualenv* do Python ou um terminal interno do VS Code **não isola** o seu sistema operacional host (Windows). Se um script malicioso alterar registros ou infectar o sistema, seu computador principal estará vulnerável.
* **Rede e Kernel Dedicados:** A Máquina Virtual (VM) roda um sistema completo e isolado. Caso algo dê errado ou um serviço quebre, você pode simplesmente restaurar um *snapshot* (ponto de restauração) sem afetar sua máquina física.

---

## 2. Distribuições Linux para Cibersegurança

Existem centenas de distribuições (distros) Linux, mas duas se destacam no cenário de segurança defensiva e ofensiva:

<p align="center">
  <a href="https://ibb.co/KzrFgc0C"><img src="https://i.ibb.co/fGx4WV1m/img1.png" alt="Menu de Inicialização do Kali Linux" border="0"></a>
  <br>
  <em>Figura 1: Tela do GRUB / Menu de inicialização do Kali Linux.</em>
</p>

1. **Kali Linux:** A distribuição mais popular e mantida pela *OffSec*. Já vem pronta para uso com uma enorme coleção de ferramentas pré-instaladas e um kernel modificado para suporte a injeção de pacotes e auditoria sem fio.
2. **Parrot OS:** Uma alternativa leve, elegante e muito bem otimizada, excelente para máquinas com recursos de hardware mais limitados e focada em privacidade.

### 📦 Principais categorias de ferramentas pré-instaladas
Essas distros trazem suítes prontas para:
* **Reconhecimento e Escaneamento de Redes** (ex: *Nmap*, *Netcat*)
* **Análise de Aplicações Web** (ex: *Burp Suite*, *Gobuster*)
* **Quebra de Senhas e Criptografia** (ex: *John the Ripper*, *Hashcat*)
* **Exploração e Pós-Exploração** (ex: *Metasploit Framework*, *Mimikatz*)

---

## 3. A Importância da Linha de Comando (CLI)

<p align="center">
  <a href="https://ibb.co/Y7T2TfX3"><img src="https://i.ibb.co/7JNvNrQX/img2.png" alt="Kali Linux rodando com o terminal aberto" border="0"></a>
  <br>
  <em>Figura 2: Área de trabalho do Kali Linux com o terminal (CLI) em execução.</em>
</p>

Trabalhar via **CLI** (*Command Line Interface*) não é preciosismo: é uma necessidade prática e a habilidade mais fundamental de um profissional de segurança.

* **Servidores sem Interface Gráfica (Headless Systems):** A vasta maioria dos servidores e hardwares de rede na nuvem, data centers ou infraestruturas críticas não possui interface visual (GUI) para economizar recursos de hardware e reduzir a superfície de ataque. Você precisará gerenciar 100% desses sistemas via linha de comando.
* **Exploração de Vulnerabilidades & Controle Remoto:** Ao obter acesso inicial (*foothold*) a uma aplicação ou servidor vulnerável, você quase nunca terá uma interface gráfica. O que você obtém é um *shell* (terminal remoto). Saber navegar, escalar privilégios e transferir arquivos sem interface visual é o divisor de águas entre o amador e o profissional.
* **Velocidade e Eficiência:** Interagir com o sistema operacional diretamente via chamadas de sistema e utilitários nativos é infinitamente mais rápido do que depender de cliques em menus e janelas.

---

## 4. Comandos Essenciais do Linux

Abaixo está um guia expandido com os comandos indispensáveis para navegação, manipulação de arquivos, redes e gerenciamento de processos no terminal Linux:

### 📂 Navegação e Manipulação de Arquivos

| Comando | O que faz | Exemplo de Uso |
| :--- | :--- | :--- |
| `pwd` | Exibe o diretório atual (*Print Working Directory*) | `pwd` |
| `cd` | Navega entre diretórios (*Change Directory*) | `cd /var/www/html` |
| `ls` | Lista os arquivos e pastas do diretório | `ls -la` (detalhes e arquivos ocultos) |
| `mkdir` | Cria um novo diretório | `mkdir -p labs/nivel0` |
| `cp` | Copia arquivos ou diretórios | `cp config.txt config.bak` |
| `mv` | Move ou renomeia arquivos/diretórios | `mv script.py /tmp/` |
| `rm` / `rmdir` | Remove arquivos ou diretórios | `rm arquivo.txt` ou `rm -rf pasta/` |
| `cat` | Exibe o conteúdo de um arquivo na tela | `cat /etc/passwd` |
| `head` / `tail` | Exibe as primeiras ou últimas linhas de um arquivo | `tail -n 20 /var/log/auth.log` |

### 🔍 Busca e Processamento de Texto

| Comando | O que faz | Exemplo de Uso |
| :--- | :--- | :--- |
| `grep` | Filtra textos ou saídas de comandos por padrão | `cat log.txt \| grep "ERROR"` |
| `find` | Busca arquivos no sistema por nome, tamanho ou permissão | `find / -name "*.conf" 2>/dev/null` |
| `wc` | Conta linhas, palavras e caracteres | `wc -l lista_ips.txt` |

### 🔐 Permissões e Privilégios

| Comando | O que faz | Exemplo de Uso |
| :--- | :--- | :--- |
| `sudo` | Executa um comando com privilégios de superusuário (*root*) | `sudo apt update` |
| `chmod` | Altera permissões de leitura, escrita e execução | `chmod +x script.sh` ou `chmod 600 id_rsa` |
| `chown` | Altera o proprietário/grupo de um arquivo | `chown kali:kali script.sh` |

### 🌐 Rede, Download e Diagnóstico

| Comando | O que faz | Exemplo de Uso |
| :--- | :--- | :--- |
| `ping` | Testa a conectividade com um host remoto | `ping -c 4 8.8.8.8` |
| `netstat` / `ss` | Exibe conexões de rede e portas abertas | `ss -tuln` (mostra portas ouvindo conexões) |
| `curl` / `wget` | Baixa arquivos ou faz requisições HTTP via terminal | `curl -I https://exemplo.com` |
| `ifconfig` / `ip` | Exibe informações das interfaces de rede da máquina | `ip a` ou `ifconfig` |

### ⚙️ Processos e Sistema

| Comando | O que faz | Exemplo de Uso |
| :--- | :--- | :--- |
| `ps` | Exibe os processos em execução no momento | `ps aux \| grep python` |
| `top` / `htop` | Monitora o uso de CPU, memória e processos em tempo real | `htop` |
| `kill` | Finaliza um processo pelo seu ID (PID) | `kill -9 1234` |

---

## 5. Configurando o Ambiente: VirtualBox + Kali Linux

Para não ter o trabalho de realizar a instalação manual do sistema operacional (particionamento de disco, fuso horário, usuários), utilizamos uma **imagem pré-configurada (Virtual Appliance / `.ova` ou `.vbox`)**.

### Passo 1: Instalar o VirtualBox
1. Baixe e instale o [Oracle VirtualBox](https://www.virtualbox.org/).

### Passo 2: Baixar e Importar a imagem do Kali Linux

<p align="center">
  <a href="https://ibb.co/twHVYqVr"><img src="https://i.ibb.co/6cyjDHjC/img3.png" alt="Gerenciador do Oracle VirtualBox" border="0"></a>
  <br>
  <em>Figura 3: Painel principal do Oracle VirtualBox Gerenciador com a VM pré-configurada.</em>
</p>

1. Acesse a área de downloads oficiais do Kali em [kali.org/get-kali/#kali-virtual-machines](https://www.kali.org/get-kali/#kali-virtual-machines).
2. Baixe o arquivo da **Virtual Machine** pré-configurada para VirtualBox (arquivo no formato `.ova` ou `.vbox`).
3. Abra o **Oracle VirtualBox Gerenciador**:
   * Clique no botão **Open** (ou vá no menu superior em *Arquivo > Importar Appliance...*).
   * Selecione o arquivo `.ova` ou `.vbox` baixado no seu computador e confirme a importação.
   * Alternativamente, basta dar um duplo clique diretamente no arquivo baixado para que o VirtualBox o abra automaticamente.
4. Após a importação, a máquina virtual aparecerá no painel esquerdo do Gerenciador (como mostrado na **Figura 3**).
5. Selecione a máquina virtual e clique no botão **Iniciar / Exibir** para ligar o sistema.

> **Vantagem:** Diferente de uma imagem de instalação comum (ISO), a imagem em formato **Appliance (`.ova`/`.vbox`)** já vem com o sistema operacional instalado, ferramentas configuradas, drivers de vídeo e o *Guest Additions* prontos para uso!

### 🔑 Credenciais Padrão do Kali:
* **Usuário:** `kali`
* **Senha:** `kali`

---

## 6. Conectando a Laboratórios Práticos (OpenVPN)

### 🌐 O que são o Hack The Box (HTB) e o TryHackMe (THM)?
O **Hack The Box (HTB)** e o **TryHackMe (THM)** são plataformas online voltadas para o aprendizado e prática de cibersegurança e hacking ético onde você pode entrar e explorar também, veja como se conectar abaixo:
* **Para que servem:** Elas disponibilizam máquinas vulneráveis e cenários reais simulados em um ambiente legal e controlado. Em vez de tentar invadir sistemas sem permissão (o que é ilegal), você pratica em redes de laboratório projetadas especificamente para testes de invasão (*pentest*), desafios do tipo *Capture The Flag* (CTF) e treinamento defensivo.
* **Como funcionam os alvos:** Os servidores e sistemas vulneráveis dessas plataformas não ficam expostos abertamente na internet pública. Eles ficam isolados em uma rede privada.

---

### 🖥️ Por que e como conectar diretamente da sua Máquina Virtual (VM)?
Para ter acesso direto aos IPs das máquinas do laboratório, você deve estabelecer um **túnel VPN** entre a sua máquina e a rede privada do HTB/THM.

Conectar **diretamente de dentro da sua Máquina Virtual (Kali Linux)** é a prática recomendada por dois motivos essenciais:
1. **Isolamento e Segurança:** Todas as ferramentas de ataque e exploração serão executadas dentro da VM, sem risco de interferir ou expor o seu computador hospedeiro (Windows/macOS).
2. **Roteamento de Rede:** O tráfego de rede gerado por ferramentas como *Nmap*, *Metasploit* ou *Burp Suite* sairá direto da interface da VM para o túnel da VPN.

---

### 🛠️ Passo a Passo para Conexão Manual via OpenVPN:

1. **Baixe o arquivo de configuração (`.ovpn`):**
   Acesse o painel do HTB ou THM usando o navegador web **de dentro do próprio Kali Linux** e faça o download do seu arquivo individual de conexão `.ovpn` (geralmente disponível no menu *Lab Access* ou *Access*).

2. **Abra o terminal e navegue até a pasta do arquivo:**
   ```bash
   cd ~/Downloads
   ```

3. **Inicie a conexão VPN:**
   Execute o comando `openvpn` com privilégios de administrador:
   ```bash
   sudo openvpn seu_arquivo.ovpn
   ```

4. **Confirme a conexão:**
   Mantenha esse terminal aberto. Quando a saída exibir a mensagem:
   ```text
   Initialization Sequence Completed
   ```
   Significa que o túnel foi criado com sucesso e sua VM agora faz parte da rede interna do laboratório.

---

### 🧪 Testando a Conexão
Para verificar se sua Máquina Virtual já enxerga o ambiente do lab:
1. Abra uma **nova aba ou janela do terminal** no Kali (deixe a janela da VPN rodando em segundo plano).
2. Tente disparar um comando `ping` para o IP da máquina do desafio fornecida pela plataforma:
   ```bash
   ping -c 4 <IP_DA_MAQUINA_DO_LAB>
   ```
3. Se houver resposta de pacotes, seu ambiente está 100% configurado e pronto para o treinamento!

---

## 🎯 Desafio Prático

1. Baixe o VirtualBox e importe a imagem do Kali Linux.
2. Inicie a VM e faça login com as credenciais padrão (`kali` / `kali`).
3. Abra o terminal e crie uma pasta chamada `desafio_nivel0` usando `mkdir -p`.
4. Entre na pasta criada com `cd` e crie um arquivo de teste usando `echo "Lab OK" > teste.txt`.
5. Verifique o conteúdo do arquivo com `cat` e liste suas permissões com `ls -la`.