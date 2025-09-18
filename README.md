# AWS-criando-stacks-no-cloudFormation

## 📚 Conteúdo Programático


➡️ Dentro do módulo de **Gerenciamento e Governança na AWS**, estudamos:  
- **CloudWatch** → monitoramento e métricas.  
- **CloudTrail** → auditoria e logs de ações.  
- **CloudFormation** → automação de criação de recursos.  
- **IAM** (Identity and Access Management) → gerenciamento de identidades.  
- **Policies e Roles** → controle de permissões.  
- **Well-Architected Framework** → boas práticas de arquitetura.  
- **CAF (Cloud Adoption Framework)** → estratégia de adoção da nuvem.  

---

## ⚡ O que é o AWS CloudFormation


➡️ O **AWS CloudFormation** é um serviço que **automatiza a criação de recursos na AWS** usando **templates em JSON ou YAML**.  
- Podemos reutilizar templates quantas vezes quisermos.  
- O custo está relacionado apenas aos **recursos criados (stacks)**, como EC2, RDS, S3 etc.  

---

## 🏗️ Automação e Versionamento


➡️ Com o CloudFormation:  
- Conseguimos **versionar templates** (controle de mudanças).  
- Podemos criar desde um **único recurso simples** (ex.: instância EC2) até uma **arquitetura robusta** com múltiplos recursos.  
- O fluxo geral é:  
  - **Template** → define os recursos.  
  - **CloudFormation** → processa o template.  
  - **Stack** → conjunto de recursos criados na AWS.  

---


# 🚀 Como Criar uma Stack no AWS CloudFormation


## 📌 O que é uma Stack?
- Uma **Stack** é o conjunto de recursos da AWS criado e gerenciado pelo CloudFormation a partir de um **template** (JSON ou YAML).  
- Exemplo: uma stack pode incluir uma instância **EC2**, um banco **RDS** e um bucket **S3**, todos definidos no mesmo template.  

---

## 🔹 Criando uma Stack pelo Console da AWS
1. Acesse o serviço **CloudFormation** no console AWS.  
2. Clique em **Create stack → With new resources (standard)**.  
3. Escolha como enviar o template:
   - **Upload a template file** → faça upload de um arquivo `.json` ou `.yaml`.  
   - **Specify an Amazon S3 URL** → use um template hospedado no S3.  
   - **Create template in Designer** → desenhe direto no console.  
4. Configure:  
   - **Stack name** → nome da sua stack.  
   - **Parameters** → variáveis do template (se existirem).  
   - **IAM Role** (opcional) → permissões para criar recursos.  
5. Clique em **Next** e revise.  
6. Confirme em **Create stack** → a AWS provisionará todos os recursos definidos.  

---

## 🔹 Criando uma Stack pela AWS CLI
Você também pode criar stacks diretamente pelo terminal.

### Exemplo:
```bash
aws cloudformation create-stack \
  --stack-name MinhaPrimeiraStack \
  --template-body file://template.json


➡️ Exemplo de arquivo **JSON** para criar buckets no **S3**:  

```json
"S3BackupBucket": {
  "Type": "AWS::S3::Bucket",
  "DeletionPolicy": "Retain",
  "Properties": {
    "AccessControl": "Private",
    "BucketName": "opentodo-backups",
    "LifecycleConfiguration": {
      "Rules": [
        {
          "ExpirationInDays": 15,
          "Status": "Enabled"
        }
      ]
    }
  }
}
