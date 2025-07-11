# 🖥️ VMware Workstation 17 Pro by HTTP

Este template permite o monitoramento completo do **VMware Workstation 17 Pro** utilizando a **API REST via HTTP**, sem necessidade de agentes ou SNMP. Ideal para ambientes locais, laboratórios e estações de trabalho com múltiplas VMs.

> 📅 **Data de criação:** 11/07/2025  
> 👨‍💻 **Autor:** Magno M. Cerqueira  
> 🧩 **Versão do template:** 0.0.1  
> 📚 **Curso relacionado:** [Zabbix 7.0 Academy – Monitoring Veeam backup from basic to advanced](https://go.hotmart.com/C92709578Y?dp=1)

---

## 📌 Funcionalidades

✅ Monitoramento via API REST  
✅ Descoberta automática de VMs  
✅ Coleta de CPU, RAM, estado e contagem de VMs  
✅ Detecção de erros de comunicação com a API  
✅ Triggers automáticas por VM

---

## 🛠️ Requisitos

- **Zabbix Server:** 7.0 LTS ou superior  
- **VMware Workstation Pro:** versão 17 com API REST ativada  
- Integração customizada que expõe o endpoint `/api/vms/`

📚 **Documentação oficial da API:**  
[Use the VMware Workstation Pro REST API Service (Broadcom TechDocs)](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/17-0/using-vmware-workstation-pro/using-vmware-workstation-pro-rest-api/use-the-vmware-workstation-pro-rest-api-service.html)

---

## ⚙️ Macros Necessárias

| Macro | Descrição | Exemplo |
|-------|-----------|---------|
| `{$VWP.API.URL}` | Endereço IP ou hostname do serviço | `192.168.1.100` |
| `{$VWP.API.PORT}` | Porta da API REST | `8080` |
| `{$VWP.STATUS.SCHEME}` | Protocolo de acesso | `http` |
| `{$VWP.DATA.TIMEOUT}` | Tempo limite de requisição | `60s` |

---

## 🔍 Itens Coletados

| Nome | Tipo | Chave |
|------|------|-------|
| Get Metrics | HTTP Agent | `veeam.get.metrics` |
| Get Errors | Script JS | `veeam.get.erros` |
| Get Count VMs | Dependent | `vwp.get.count.vms` |

---

## 🔄 Descobertas Automáticas (LLD)

### 1. **VMware VMs Discovery**
- Descobre todas as VMs do host
- Itens criados por VM:
  - ID
  - Nome
  - CPUs
  - Memória RAM
  - Status (poweredOn/poweredOff)

### 2. **VMs Count Discovery**
- Descobre e conta:
  - Total de VMs
  - VMs Online
  - VMs Offline

---

## 🚨 Triggers

| Nome | Gravidade | Expressão |
|------|-----------|-----------|
| VMware API com erros | Média | `veeam.get.erros ≠ 200` |
| VM desligada (`{#VWP_VM_NAME}`) | Alta | `vmware.vm.power ≠ 0` |

---

## 🎨 Value Maps

- `Get rest api error status`:  
  - `200` → `Online`

- `VMware VMs Power Status`:  
  - `0` → `poweredOn`  
  - `1` → `poweredOff`

---

## 🚀 Instalação

1. Importe o arquivo XML no Zabbix.
2. Vincule o template ao host desejado.
3. Configure as macros com os dados corretos.
4. Acompanhe os dados na interface do Zabbix.

---

## 🧪 Testado em

- VMware Workstation Pro 17 (Windows)
- Zabbix Server 7.0 LTS
- Coleta via HTTP sem agente

---

## 📫 Contato

📧 **E-mail:** magnopeem@gmail.com  
📣 **Telegram:** [Zabbix Brasil](https://t.me/ZabbixBrasil)

---

## 📁 Arquivos

- `template_vmware_workstation_17_pro_by_http.xml`: Template Zabbix para importação
- `README.md`: Este arquivo com todas as instruções

---

## 🧠 Créditos

Desenvolvido com base em boas práticas de monitoramento, visando controle total de VMs locais com integração leve e eficiente.

---

🔗 **Curso oficial para aprofundar:**  
[🎓 Zabbix 7.0 Academy – Monitoring Veeam backup from basic to advanced](https://go.hotmart.com/C92709578Y?dp=1)
