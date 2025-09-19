# Push da imegem da sua máquina para Amazon ECR

Mandar a imagem criada na sua máquina para o reposiório da ECR da Amazon
```
## ☁️ Fase 1: Configuração do Amazon ECR

### Passo 1.1: Acessar o Console AWS

1. Acesse [console.aws.amazon.com](https://console.aws.amazon.com)
2. Faça login com suas credenciais

*[Espaço para print: Console AWS]*

### Passo 1.2: Navegar para o ECR

1. Na barra de busca superior, digite "ECR"
2. Clique em "Elastic Container Registry"

*[Espaço para print: Busca pelo ECR]*

### Passo 1.3: Criar um repositório

1. Clique em "Create repository"
2. Configure:
   - **Visibility settings**: Private
   - **Repository name**: `meu-website`
   - **Tag immutability**: Disabled (padrão)
   - **Scan on push**: Enabled (recomendado para segurança)
3. Clique em "Create repository"

*[Espaço para print: Formulário de criação do repositório]*

### Passo 1.4: Anotar a URI do repositório

Após criar, você verá algo como:
```
123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website
```

⚠️ **Importante**: Copie e guarde esta URI, você precisará dela!

*[Espaço para print: Repositório criado com a URI visível]*

---

## 📤 Fase 2: Push da Imagem para o ECR

### Passo 2.1: Configurar AWS CLI

Se ainda não configurou, execute:
```bash
aws configure
```

Você precisará fornecer:
- **AWS Access Key ID**: Obtida no IAM
- **AWS Secret Access Key**: Obtida no IAM
- **Default region**: ex: us-east-1
- **Default output format**: json

### Passo 2.2: Autenticar Docker com ECR

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com
```

⚠️ **Substitua**: 
- `us-east-1` pela sua região
- `123456789012` pelo seu Account ID

Você deve ver:
```
Login Succeeded
```

*[Espaço para print: Login bem-sucedido no ECR]*

### Passo 2.3: Tagar a imagem para o ECR

```bash
docker tag meu-website:v1.0 123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website:v1.0
```

### Passo 2.4: Push da imagem

```bash
docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website:v1.0
```

Você verá o progresso do upload:
```
The push refers to repository [123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website]
abc123: Pushed
def456: Pushed
v1.0: digest: sha256:xyz789... size: 1234
```

*[Espaço para print: Push concluído]*

### Passo 2.5: Verificar no Console AWS

1. Volte ao ECR no console AWS
2. Clique no seu repositório
3. Você deve ver a imagem com a tag v1.0

*[Espaço para print: Imagem no ECR]*

---
