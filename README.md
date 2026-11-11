<div align="center">

# ⚡ WhySystem — By Maad

**Conjunto de scripts PowerShell + VBS para otimização de Windows voltada a gaming/performance, com personalização de identidade do sistema, limpeza de rastros e sistema de autenticação/blacklist.**

![versão](https://img.shields.io/badge/vers%C3%A3o-2.5-blue)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-5391FE?logo=powershell&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?logo=windows&logoColor=white)
![licença](https://img.shields.io/badge/licen%C3%A7a-MIT-yellow)
![status](https://img.shields.io/badge/status-experimental-red)

</div>

---

## ⚠️ AVISO IMPORTANTE — LEIA ANTES DE USAR

> 🚨 **Este projeto executa alterações profundas no Windows, incluindo:**
> - Alteração de registros do sistema, WMI, BIOS (string), nome do PC e OEM info
> - Desativação de serviços (Windows Update, Defender auxiliares, Spooler, etc.)
> - Criação de políticas de QoS e prioridade de CPU para dezenas de jogos
> - **Envio de dados do PC (IP, MAC, serial, geolocalização) para um webhook externo do Discord**
> - Um script de "punição" (`withoutperm.ps1`) que **apaga o Desktop, renomeia binários do sistema (explorer, cmd, regedit, etc.) e trava a máquina** caso o usuário esteja na blacklist
>
> ❌ **NÃO execute isso em máquina de trabalho, de terceiros ou sem backup.**
> ✅ Use apenas em VM ou em um PC pessoal ciente dos riscos.
> 🔐 O autor não se responsabiliza por perda de dados, banimentos ou sistema inutilizado.

---

## 📖 Sobre

**WhySystem** é uma suíte de scripts para Windows focada em:

- 🎮 **Performance em jogos** — QoS por app, prioridade de CPU, tweaks de rede e energia
- 🧹 **Limpeza de rastros** — registros de histórico do Explorer, WinRAR, USB, MRU, etc.
- 🎭 **Personalização de identidade** — nome do PC, fabricante, modelo, CPU, BIOS, OEM
- 🔐 **Autenticação + blacklist** — verifica `blacklist.txt` e dispara `withoutperm.ps1` se detectar bypass

O script principal (`why.ps1`) coleta informações do sistema e **envia um embed para um Discord webhook** (URL carregada de um Pastebin) como forma de "log/telemetria do autor".

---

## ✨ Funcionalidades

| Arquivo | Função |
|---|---|
| 🚀 **`why.ps1`** | Script principal: cria ponto de restauração, aplica QoS, prioridades, desativa telemetria/serviços, remove bloatware, verifica auth + blacklist, envia log para webhook |
| 🎨 **`personalization.ps1`** | Renomeia PC, altera WMI (fabricante/modelo/CPU/BIOS), aplica wallpaper, cria logo OEM e chave de desinstalação falsa ("NVIDIA Shader Cache Optimizer") |
| 🧹 **`microsoft.vbs`** | Limpa ~50 chaves de registro (ShellBags, MRU, UserAssist, USBSTOR, AppCompat, journal USN) e apaga `.ps1` em `C:\Program Files\Windows NT` |
| 💀 **`withoutperm.ps1`** | Script de punição: apaga Desktop, cria pastas infinitas, abre 15 notepads, renomeia binários do sistema, mata explorer, beeps — **destrutivo** |
| 📋 **`blacklist.txt`** | Lista de identificadores `Usuário MAC Serial` bloqueados |

---

## 🚀 Instalação e uso

### Pré-requisitos

- **Windows 10 ou 11**
- **PowerShell 5.1+** (já incluso no Windows)
- **Execução como Administrador** (obrigatório — o script reabre elevado se necessário)
- **ExecutionPolicy** permitindo scripts (`Bypass` ou `Unrestricted`)
- Ponto de restauração habilitado no sistema (recomendado)

### Passo a passo

1. **Faça backup** do seu sistema (ponto de restauração ou imagem).
2. Clone o repositório ou baixe os arquivos:
   ```powershell
   git clone https://github.com/castielwallker/whysistem.git
   cd whysistem
