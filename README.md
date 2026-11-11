Desafio Prático: Simulação de Brute Force e Mitigação
Nesse repositório eu documentei o laboratório prático que fiz utilizando Kali Linux, Metasploitable 2 e DVWA para testar ataques de força bruta e entender como proteger os sistemas.

Ambiente do Lab
Atacante: Kali Linux (no VirtualBox)

Alvo: Metasploitable 2 (com FTP, SMB e HTTP/DVWA rodando)

Rede: Apenas Host-Only para manter tudo isolado e seguro.

O que foi feito
1. Teste de Força Bruta no FTP
Usei o Medusa para testar uma lista de senhas no serviço FTP do Metasploitable 2.

Comando que utilizei:
medusa -h <IP_DO_ALVO> -u msfadmin -P /caminho/para/wordlist.txt -M ftp

O que aprendi / Como defender: Senhas fáceis deixam o sistema totalmente vulnerável. A solução é usar senhas fortes, colocar bloqueio após várias tentativas erradas e, se possível, trocar FTP por SFTP.

2. Enumeração e Password Spraying no SMB
Procurei usuários válidos no serviço SMB e testei uma senha comum em vários deles.

Comando de enumeração (Nmap):
nmap -p 445 --script smb-enum-users <IP_DO_ALVO>

Ataque com Medusa:
medusa -h <IP_DO_ALVO> -U users.txt -p senha123 -M smbnt

O que aprendi / Como defender: Esse tipo de ataque tenta passar despercebido pelos bloqueios de conta. Para mitigar, o ideal é desligar versões antigas do SMB (como o SMBv1), usar autenticação em dois fatores e ficar de olho nos logs.

3. Força Bruta em Aplicação Web (DVWA)
Simulei ataques de login em uma página web vulnerável usando o DVWA no nível baixo de segurança.

Como fiz: Direcionei a ferramenta para a página de login do DVWA (/vulnerabilities/brute/) e testei uma lista de credenciais.

O que aprendi / Como defender: Formulários sem proteção contra muitas requisições caem fácil. A mitigação envolve colocar CAPTCHA, limitar tentativas por IP e cuidar bem das sessões.

Conclusão
vi na prática como senhas fracas e serviços desprotegidos facilitam a vida de um invasor. A segurança exige sempre várias camadas de proteção e monitoramento constante.
