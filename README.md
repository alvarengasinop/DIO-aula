# DIO-aula
aula brutal force
# Projeto Prático de Cibersegurança: Simulação de Brute Force e Defesa

Este repositório contém a documentação prática, comandos e análise de segurança de um laboratório controlado de força bruta e avaliação de vulnerabilidades utilizando **Kali Linux**, **Metasploitable 2** e **DVWA**.

## 🛠️ Arquitetura do Ambiente de Laboratório
* **Máquina Atacante:** Kali Linux (VirtualBox)
* **Máquina Alvo:** Metasploitable 2 (VM vulnerável executando serviços como FTP, SMB e HTTP/DVWA)
* **Modo de Rede:** Rede Interna (Host-Only) para garantir uma execução isolada e segura.

## 🚀 Cenários Práticos e Execução

### 1. Ataque de Força Bruta em FTP
Utilização do **Medusa** contra o serviço FTP do Metasploitable 2 (`vsftpd`) para testar a força de credenciais contra uma wordlist personalizada.

* **Comando Utilizado:**
  ```bash
  medusa -h <IP_DO_ALVO> -u msfadmin -P /caminho/para/wordlist.txt -M ftp
Análise e Mitigação:

Credenciais fracas ou padrões permitem acesso não autorizado imediato.

Mitigação: Aplicar políticas rígidas de complexidade de senha, implementar mecanismos de bloqueio de conta após várias tentativas falhas e restringir o acesso FTP via firewall ou migrar para alternativas seguras como SFTP.

2. Password Spraying e Enumeração em SMB
Enumeração de contas de usuário válidas e execução de um ataque de password spraying contra o serviço SMB do alvo.

Comando de Enumeração (utilizando Nmap):

Bash
nmap -p 445 --script smb-enum-users <IP_DO_ALVO>
Execução do Ataque (Módulo SMB do Medusa):

Bash
medusa -h <IP_DO_ALVO> -U users.txt -p senha123 -M smbnt
Análise e Mitigação:

O password spraying explora senhas padrão comuns em várias contas enquanto tenta evadir os limites de bloqueio de conta.

Mitigação: Desativar o SMBv1, exigir autenticação multifator (MFA) e monitorar os logs de eventos em busca de picos anômalos de login.

3. Força Bruta em Aplicação Web (DVWA)
Simulação de ataques de força bruta de autenticação contra um formulário de login vulnerável no DVWA (Damn Vulnerable Web Application).

Procedimento:

Configuração do Burp Suite / Medusa para direcionar o endpoint de login do DVWA (/vulnerabilities/brute/).

Teste de listas de credenciais geradas pelo usuário contra os parâmetros do formulário com nível de segurança baixo.

Análise e Mitigação:

Formulários web que carecem de limitação de taxa (rate-limiting) e validação de sessão são altamente suscetíveis a ataques automatizados de preenchimento de credenciais (credential stuffing).

Mitigação: Implementar mecanismos de CAPTCHA, controle rígido de taxa por IP/sessão e gerenciamento seguro de cookies de sessão.

🛡️ Principais Conclusões e Resumo de Defesa
Ferramentas automatizadas como o Medusa demonstram com que rapidez credenciais padrão comprometem o perímetro de uma rede.

A defesa em profundidade exige varreduras regulares de vulnerabilidade, monitoramento agressivo de logs e aplicação estrita do princípio do menor privilégio.
