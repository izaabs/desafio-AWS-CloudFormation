# 🚀 Implementando a Primeira Stack com AWS CloudFormation

Este repositório documenta a prática de criação da primeira Stack utilizando o **AWS CloudFormation**, conforme proposto no desafio de "Implementação de Primeira Stack com AWS CloudFormation" da DIO.

O objetivo principal foi transformar um template de código declarativo em infraestrutura real na AWS, aplicando conceitos de **Infraestrutura como Código (IaC)**.

---

## 🎯 Objetivo da Stack Implementada

O template YAML/JSON utilizado neste projeto (disponível em `./template.yaml` ou similar) visa provisionar a seguinte infraestrutura:

* **Recurso 1 (Ex: Bucket S3):** Cria um bucket S3 para armazenamento de logs/arquivos, configurado com X política (Ex: bloqueio de acesso público).
* **Recurso 2 (Ex: Instância EC2 / Security Group):** Cria um Grupo de Segurança (Security Group) permitindo tráfego na porta 80 (HTTP) e 22 (SSH).

---

## 🛠️ Tecnologias e Conceitos Envolvidos

| Tecnologia/Conceito | Função no Projeto |
| :--- | :--- |
| **AWS CloudFormation** | O serviço IaC principal, responsável pela orquestração e gerenciamento do ciclo de vida da Stack. |
| **YAML/JSON** | Linguagem declarativa utilizada para escrever o template da Stack. |
| **Amazon S3 / EC2 / Outro** | Os serviços de infraestrutura que foram efetivamente provisionados. |
| **IAM** | Utilizado para definir as permissões necessárias para o CloudFormation criar os recursos. |
| **GitHub** | Ferramenta de versionamento e documentação técnica. |

---

## 📝 Análise do Template CloudFormation

O template utilizado é um arquivo **declarativo**, ou seja, ele descreve o *estado final desejado* da infraestrutura, e o CloudFormation se encarrega de realizar os passos para atingir esse estado.

As seções chave do template são:

### 1. `Parameters` (Parâmetros)
* **Função:** Permitem que o usuário personalize a Stack no momento da criação.
    > **Insight:** Usar Parâmetros torna o template reutilizável e flexível, evitando "hard-coding" de valores.

### 2. `Resources` (Recursos)
* **Função:** Lista todos os recursos da AWS que serão criados. Esta é a seção mais importante do template.
* **Sintaxe:** Cada recurso é definido pelo seu **Logical ID** e o **Tipo de Recurso** da AWS (ex: `AWS::S3::Bucket`).
    > **Insight:** É necessário conhecer a sintaxe exata dos tipos de recursos e suas propriedades, que está na documentação oficial da AWS.

### 3. `Outputs` (Saídas)
* **Função:** Exporta valores importantes da Stack (como o Nome do Bucket, URL de um Load Balancer, IDs gerados) para que possam ser usados facilmente por outras Stacks ou visualizados no console.

---

## 🧠 Insights Adquiridos e Aprendizados

Durante a implementação desta Stack, pude consolidar os seguintes conceitos e boas práticas de IaC:

### 1. O Conceito de Rollback
* **Aprendizado:** Se qualquer recurso dentro da Stack falhar na criação (ex: erro de sintaxe ou permissão), o **CloudFormation automaticamente inicia um `ROLLBACK`**.
* **Importância:** Isso garante a **integridade** da infraestrutura, removendo todos os recursos que foram criados com sucesso até o ponto da falha, evitando custos desnecessários e estados incompletos (`half-baked states`).

### 2. Gerenciamento do Ciclo de Vida
* **Aprendizado:** O CloudFormation não apenas cria os recursos, ele os **gerencia**. Se eu modificar o template e usar a função `Update Stack`, ele calcula as diferenças e altera/recria **apenas** o que for necessário.
* **Dica:** É fundamental sempre **DELETAR** a Stack ao final dos testes (via `Delete Stack`) para remover todos os recursos gerenciados e evitar cobranças na AWS.

### 3. Facilidade de Auditoria
* **Aprendizado:** O painel **"Events"** (Eventos) é crucial. Ele fornece um registro detalhado e sequencial de cada recurso sendo criado, modificado ou deletado, o que é excelente para diagnóstico e auditoria.

### 4. Vantagens do IaC
* A infraestrutura é **versionada** (no GitHub), permitindo rastrear todas as alterações.
* A infraestrutura é **reprodutível**, garantindo que o ambiente de teste seja idêntico ao ambiente de produção.

---
