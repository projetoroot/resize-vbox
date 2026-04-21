# 📦 Build do pacote Resize VBox Disk (.deb)

**Autor:** Diego Costa (@diegocostaroot)  
**Projeto:** Resize VBox Disk  
**Versão:** 1.0 | **Ano:** 2026  

Guia completo para compilar o pacote `.deb` a partir do código-fonte, permitindo personalizações antes da distribuição.

---

## 📌 Objetivo

Este documento explica como gerar manualmente o pacote `.deb` do projeto.

Indicado para quem deseja:

- Modificar o script principal  
- Alterar dependências  
- Customizar nome, versão ou descrição  
- Gerar seu próprio pacote instalável  

---

## 🧠 Estrutura do pacote Debian

O pacote segue o padrão de empacotamento do Debian:

```
resize-vbox_1.0/
├── DEBIAN/
│   └── control
├── usr/
│   ├── bin/
│   │   └── resize-vbox
│   ├── share/
│   │   ├── applications/
│   │   │   └── resize-vbox.desktop
│   │   └── icons/
│   │       └── hicolor/128x128/apps/
│   │           └── resize-vbox.png
```

---

## 🔧 Arquivo de controle

O arquivo `DEBIAN/control` define os metadados do pacote:

```
Package: resize-vbox
Version: 1.0
Section: utils
Priority: optional
Architecture: all
Depends: virtualbox, zenity
Maintainer: Diego Costa - Projeto Root
Description: Interface grafica para redimensionar discos do VirtualBox
 Ferramenta simples para aumentar discos VDI/VMDK com interface Zenity.
```

### 📌 Explicação dos campos

| Campo | Descrição |
|---|---|
| Package | Nome do pacote |
| Version | Versão do software |
| Section | Categoria do pacote |
| Priority | Prioridade no sistema |
| Architecture | Tipo de arquitetura (all = independente) |
| Depends | Dependências obrigatórias |
| Maintainer | Responsável pelo pacote |
| Description | Descrição curta e longa |

---

## ⚙️ Processo de build

### 1. Criar estrutura

```bash
mkdir -p resize-vbox_1.0/{DEBIAN,usr/bin,usr/share/applications,usr/share/icons/hicolor/128x128/apps}
cd resize-vbox_1.0/
```

---

### 2. Criar script principal

```bash
nano usr/bin/resize-vbox
```

Após inserir o conteúdo do script:

```bash
chmod 755 usr/bin/resize-vbox
```

---

### 3. Criar atalho do sistema

```bash
nano usr/share/applications/resize-vbox.desktop
```

Exemplo:

```
[Desktop Entry]
Name=Resize Disco VirtualBox
Exec=resize-vbox
Icon=resize-vbox
Type=Application
Terminal=false
Categories=System;
```

---

### 4. Criar arquivo de controle

```bash
nano DEBIAN/control
```

Copie o conteúdo apresentado anteriormente.

Definir permissões:

```bash
chmod 755 DEBIAN
chmod 644 DEBIAN/control
```

---

### 5. Gerar pacote

```bash
cd ..
dpkg-deb --build resize-vbox_1.0
```

Saída esperada:

```
resize-vbox_1.0.deb
```

---

## 🧪 Validação

Após o build, valide o pacote:

```bash
dpkg -I resize-vbox_1.0.deb
```

E instale para teste:

```bash
sudo dpkg -i resize-vbox_1.0.deb
```

---

## 🔄 Customização

Você pode alterar facilmente:

| Item | Onde modificar |
|---|---|
| Script principal | usr/bin/resize-vbox |
| Nome do app | .desktop |
| Ícone | pasta icons |
| Dependências | DEBIAN/control |
| Versão | DEBIAN/control |

---

## ⚠️ Boas práticas

✔ Manter permissões corretas (755 para executáveis)  
✔ Garantir dependências válidas  
✔ Testar instalação antes de distribuir  
✔ Evitar caminhos absolutos de usuário  

---

## 🎯 Resultado

Após seguir o processo:

- Pacote `.deb` funcional  
- Instalável via `dpkg`  
- Integrado ao menu do sistema  
- Pronto para distribuição  



