# Ethical-Hacking-

# 🛡️ Desafio: Pentest com Kali Linux e Medusa

Este repositório contém a documentação e os artefatos do desafio prático de simulação de ataques de força bruta, utilizando o ecossistema Kali Linux contra o ambiente vulnerável Metasploitable 2.

## 📋 Objetivo
Implementar, documentar e validar ataques de força bruta em serviços de rede (FTP, SMB e Web) para entender vulnerabilidades de autenticação e propor medidas de mitigação.

## 💻 Ambiente de Laboratório
- **Atacante:** jeferson@Kali (IP: [192.168.56.101])
- **Alvo:** Metasploitable 2 (IP: [192.168.56.102])
- **Ferramentas:** Medusa, Nmap, VirtualBox, DVWA, Kali Linux
- **Rede:** Host-Only (Isolada).

---

## 🛠️ Execução do Projeto

### 1. Escaneamento de Rede (Reconhecimento)
Identificação de serviços ativos no alvo para definir os vetores de ataque.
- **Comando:** `nmap -sV 192.168.56.101`
- **Resultado:** Portas 21 (FTP), 22 (ssh), 139/445 (SMB) e 80 (HTTP) identificadas como abertas.

> ![Print do Nmap](Ethical-Hacking/NMAP.png)

### 2. Ataque Web (DVWA) - Brute Force HTTP
Simulação de ataque de força bruta contra o formulário de login da aplicação web DVWA.
- **Configuração:** Security Level definido como `Low`.
- **Cenário:** O alvo foi o formulário de autenticação HTTP GET/POST.
- **Comando :*medusa -h 192.168.56.102 -U users.txt -P pass.txt -M http \
             -m PAGE: '/dvwa/login.php' \
             -m FORM: 'username=^USER^§Login' \ 
             -m 'FAIL=Login failed' -t 6
Pagina web:
  http://192.168.56.102/dvwa/login.php

> !(prints2/DVWA.png)

### 3. Ataque de Força Bruta: FTP
Simulação de tentativa de login no serviço de transferência de arquivos.
- **Comando:** `medusa -h [IP_ALVO] -u msfadmin -P wordlist.txt -M ftp`
- **Sucesso:** Credenciais encontradas: `msfadmin:msfadmin`.

> ![Print do Medusa FTP](images/Loginftp.png)

### 4. Ataque SMB (Password Spraying)
Teste de credenciais no serviço de compartilhamento de arquivos.
- **Comando:** `medusa -h [IP_ALVO] -U users.txt -p password123 -M smbnt`

---

## 🛡️ Mitigações Recomendadas
Para prevenir os ataques demonstrados, as seguintes medidas são sugeridas:
1. **Políticas de Senhas:** Implementar complexidade mínima e rotação periódica.
2. **Bloqueio de Intrusão:** Utilizar ferramentas como `Fail2Ban` para bloquear IPs após sucessivas falhas.
3. **Desativação de Serviços:** Desabilitar FTP e SMB se não forem estritamente necessários.
4. **2FA:** Implementar autenticação de dois fatores em serviços críticos.

## 📂 Estrutura de Arquivos
- `/prints 2`: Capturas de tela dos testes.
- `/wordlists`: Listas de usuários e senhas utilizadas.
- `README.md`: Documentação principal.
