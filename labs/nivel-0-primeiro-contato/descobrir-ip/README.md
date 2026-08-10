# 🌐 Nível 0 – Guia de Introdução ao Terminal e Endereços IP

**Objetivo:** Entender o básico sobre a linha de comandos, compreender o que é um endereço IP (Público vs. Privado) e aprender a identificar ambos utilizando o terminal.

---

## 🖥️ 1. Pré-requisito: A Interface de Linha de Comandos (CLI)

Antes de falarmos sobre redes e endereços IP, precisamos de entender onde os comandos são executados: a **Linha de Comandos** (ou **Terminal**).

Em cibersegurança, grande parte do trabalho é feito interagindo diretamente com o sistema através de texto, usando diretamente o Terminal, vou citar os principais para melhor entendimento de onde os comandos devem ser inseridos, e particularidades de cada sistema operacional (OS).

### O que é o Terminal e o Shell (Bash)?
* **Terminal:** É a janela/aplicação gráfica onde digitas os comandos.
* **Shell (ex.: Bash, PowerShell):** É o programa que roda dentro do terminal. Ele lê o comando que digitaste, executa-o no sistema operativo e devolve a resposta no ecrã.

### Principais Terminais por Sistema Operativo:
* **Windows:**
  * **CMD (Prompt de Comando):** O terminal clássico do Windows.
  * **PowerShell:** O terminal moderno do Windows, mais poderoso e compatível com vários comandos avançados.
* **Linux / macOS:**
  * **Bash / Zsh:** O shell/terminal padrão nesses sistemas. É a base para a maioria dos servidores e ferramentas de segurança.

> 💡 **Como abrir no teu computador:**
> * **Windows:** Pressiona `Win + R`, digita `powershell` ou `cmd` e pressiona `Enter`.
> * **Linux:** Pressiona `Ctrl + Alt + T`.
> * **macOS:** Pressiona `Cmd + Espaço`, digita `Terminal` e pressiona `Enter`.

![Exemplo de imagem prompt de comando no Windows](https://i.ibb.co/CKWW5TvY/image.png)
---

## 💡 2. O que é um Endereço IP?

Um **endereço IP (Internet Protocol)** é a identificação única de um dispositivo numa rede, funcionando de forma semelhante ao endereço de uma casa. É através dele que os dados sabem exatamente de onde saíram e para onde devem ir.

Existem dois tipos fundamentais de endereços IP:

* **IP Privado (Rede Local / LAN):** Atribuído pelo teu router para identificar a tua máquina **dentro da tua casa ou escritório**. Ninguém fora da tua rede local consegue aceder diretamente a este IP.
* **IP Público (Internet / WAN):** Fornecido pelo teu operador de internet (provedor). É a tua identidade para o resto do mundo na Internet.

> 🏠 **Analogia rápida:**
> * O **IP Privado** é o número do teu quarto/apartamento (só quem está dentro do prédio usa).
> * O **IP Público** é o endereço do prédio com o código postal (é o que os correios usam para entregar encomendas).

---

## 💻 3. Método 1: Descobrir o teu IP Privado (`ipconfig`)

O comando `ipconfig` consulta as placas de rede do teu próprio computador localmente, sem precisar de acesso à Internet.

### Como Executar:
1. Abre o **Terminal** (CMD ou PowerShell no Windows).
2. Digita o comando e pressiona `Enter`:
   ```cmd
   ipconfig
   ```
*(Em sistemas Linux ou macOS, o comando equivalente é `ip a` ou `hostname -I`).*

### Exemplo de Resultado (*Output*):
```text
Adaptador de Rede Sem Fio Wi-Fi:

   Sufixo DNS específico da conexão. . . . . . : localdomain
   Endereço IPv4. . . . . . . . . . . . . . . : 192.168.1.15
   Máscara de Sub-rede . . . . . . . . . . . . : 255.255.255.0
   Gateway Padrão. . . . . . . . . . . . . . . : 192.168.1.1
```

### Explicação dos Campos:
* **Endereço IPv4 (`192.168.1.15`):** É o teu **IP Privado**. É assim que o teu router reconhece a tua máquina na rede local.
* **Gateway Padrão (`192.168.1.1`):** É o IP do teu próprio router dentro da rede local.

---

## 🌍 4. Método 2: Descobrir o teu IP Público (`curl ifconfig.me`)

Para saber qual é o teu IP na Internet, fazemos uma requisição a um servidor externo para que ele nos diga com que endereço chegámos até ele.

### Pré-requisito: O que é o `curl`?
O `curl` é uma ferramenta de linha de comandos usada para transferir dados e interagir com sites e APIs diretamente pelo terminal.

* **Windows 10/11, macOS e Linux:** O `curl` já vem instalado por padrão!
* **Verificação / Instalação (se necessário):**
  * Para confirmar se está instalado: `curl --version`
  * No Linux (Ubuntu/Debian), se não estiver instalado: `sudo apt install curl`

### Como Executar:
Abre o terminal e executa:
```bash
curl ifconfig.me
```

### Exemplo de Resultado (*Output*):
```text
203.0.113.195
```

### Explicação:
Ao executar este comando, o `curl` faz uma requisição silenciosa ao site `ifconfig.me`. O site lê o teu endereço de origem na Internet e devolve apenas os números do teu **IP Público**.

---

## 💡 5. O que fazer se o resultado for um código longo (IPv6)?

Se ao executar `curl ifconfig.me` receberes um código longo com letras e dois pontos (ex.: `2001:db8:85a3::8a2e:0370:7334`), significa que o teu operador de internet te atribuiu um **IPv6**.

* **IPv4:** É o formato tradicional com 4 blocos de números (ex.: `203.0.113.195`).
* **IPv6:** É o formato moderno e mais longo, criado para substituir o IPv4 devido ao esgotamento de endereços no mundo.

👉 **Dica Prática:** Para forçar o `curl` a exibir especificamente o teu **IPv4 público**, adiciona o parâmetro `-4`:
```bash
curl -4 ifconfig.me
```

---

## 🔄 6. Resumo das Diferenças

| Conceito | `ipconfig` (ou `ip a`) | `curl ifconfig.me` |
| :--- | :--- | :--- |
| **Tipo de IP** | Privado (Local) | Público (Internet) |
| **Escopo** | Apenas dentro da tua rede doméstica | Toda a Internet |
| **Precisa de Internet?** | Não | Sim |
| **Formato Comum** | `192.168.X.X` ou `10.X.X.X` | Varia de acordo com o teu operador |

---

## ⚠️ 7. Nota de Segurança

O teu **IP Privado** só funciona dentro da tua casa e não expõe o teu computador diretamente à Internet. No entanto, o teu **IP Público** pode revelar a tua localização aproximada (cidade e fornecedor de internet). Em contextos reais de testes de segurança, evita expor o teu IP público em fóruns ou capturas de ecrã públicas.

---

## ❓ 8. Perguntas de Fixação

1. Qual é a diferença entre o IP que aparece no `ipconfig` e o que aparece no `curl ifconfig.me`?
2. Se desligar o teu roteador da tomada e o voltar a ligar, qual dos dois IPs tem maior probabilidade de mudar?
3. O que acontece se executar o comando `ipconfig` com o computador totalmente desligado da Internet?