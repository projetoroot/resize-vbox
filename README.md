# 💽 Resize VBox Disk

**Autor:** Diego Costa (@diegocostaroot)  
**Canal no youtube:** Projeto Root ([youtube.com/projetoroot](https://www.youtube.com/projetoroot))  
**Wiki:** ([wiki.projetoroot.com.br](https://wiki.projetoroot.com.br))  
**Versão:** 1.0 | **Ano:** 2026  

Interface gráfica para redimensionamento de discos no VirtualBox com validações de segurança e uso simplificado.

---

## 📌 Objetivo

Este software foi criado para simplificar o processo de resize de discos virtuais, reduzindo erros operacionais comuns.

Os ajustes ajudam a:

- Evitar uso manual direto do `VBoxManage`  
- Garantir que a VM esteja em estado seguro  
- Validar acesso ao storage antes da operação  
- Fornecer interface gráfica simples e direta  

> ⚠️ Após o resize, é necessário expandir a partição dentro da VM.

---

## 🧠 Modelo de funcionamento

O princípio adotado é execução segura com validações antes da operação.

| Etapa | Ação |
|---|---|
| 1 | Listar VMs registradas |
| 2 | Selecionar VM |
| 3 | Identificar discos vinculados |
| 4 | Exibir tamanho provisionado e uso real |
| 5 | Solicitar novo tamanho |
| 6 | Executar resize |

---

## 🔧 Compatibilidade

| Sistema | Versões Testadas | Observações |
|---|---|---|
| 🐧 Debian | 11, 12, 13 | Total compatibilidade |
| 🐧 Ubuntu | 20.04 ou superior | Funciona normalmente |
| 🐧 Linux Mint | 21, 22 | Compatível |
| 🖥️ VirtualBox | 6.x, 7.x | Requer VBoxManage |

> ⚠️ Requer VirtualBox instalado e VMs registradas no sistema.

---

## 🛡️ Validações Implementadas

| Validação | Comportamento |
|---|---|
| Estado da VM | Bloqueia se não estiver desligada |
| Existência do disco | Valida caminho físico |
| Permissão | Verifica leitura e escrita |
| Storage | Detecta storage offline |
| Entrada | Aceita apenas números |
| Resize | Permite apenas expansão |

---

## 🎛️ Informações exibidas

| Campo | Descrição |
|---|---|
| Caminho do disco | Localização completa do VDI ou VMDK |
| Tamanho provisionado | Tamanho configurado no VirtualBox |
| Uso real | Espaço ocupado em disco |

---

## 📂 Estrutura do pacote

| Caminho | Descrição |
|---|---|
| /usr/bin/resize-vbox | Executável principal |
| /usr/share/applications/resize-vbox.desktop | Atalho no menu |
| /usr/share/icons/hicolor/... | Ícone do sistema |

---

## 💻 Uso

### Execução

```bash
resize-vbox
```

### Fluxo

- Selecionar VM  
- Escolher disco  
- Informar novo tamanho  
- Confirmar operação  

---

## ⚠️ Limitações

| Item | Status |
|---|---|
| Redução de disco | ❌ Não suportado |
| Resize com VM ligada | ❌ Bloqueado |
| Snapshots ativos | ⚠️ Pode falhar |
| Partição interna | ❌ Não gerenciado |

---

## 📌 Pós operação

Após o resize:

| Ação necessária | Ferramentas |
|---|---|
| Expandir partição | fdisk, parted |
| Expandir filesystem | resize2fs, xfs_growfs |
| Interface gráfica | gparted |

---

## 🧪 Checklist

| Item | Status Esperado |
|---|---|
| VM desligada | ✅ |
| Disco acessível | ✅ |
| Permissão válida | ✅ |
| Resize executado | ✅ |
| Partição expandida | ⚠️ Manual |

---

## 📁 Estrutura recomendada do repositório

```
resize-vbox/
├── resize-vbox.sh
├── resize-vbox.desktop
├── icon.png
├── DEBIAN/
│   └── control
```

---

## 📚 Boas práticas

✔ Sempre desligar a VM antes  
✔ Evitar resize em discos com snapshot  
✔ Garantir backup antes da operação  
✔ Validar storage antes de executar  

---

## 🚀 Instalação

### Dependências
Instalação do Virtualbox deve ser realizada antes, então faça como achar melhor para o seu sistema!

```bash
sudo apt update
sudo apt install zenity
```

### Instalar pacote

```bash
cd /tmp
wget https://github.com/projetoroot/resize-vbox/blob/main/resize-vbox_1.0.deb
sudo dpkg -i resize-vbox_1.0.deb
sudo apt -f install
```
---
#### Abrir o software
No seu ambiente gráfico no linux clique no menu e pesquise por Resize, será exibido "Resize Disco VirtualBox"

OU 

No shell do linux com seu usuário digite: 

```bash
resize-vbox
```



