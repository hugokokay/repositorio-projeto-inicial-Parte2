# Push da imegem da sua máquina para Amazon ECR

Mandar a imagem criada na sua máquina para o reposiório da ECR da Amazon


Fase 1: Configuração do Amazon ECR
Passo 1.1: Acessar o Console AWS
Acesse console.aws.amazon.com
Faça login com suas credenciais
[Espaço para print: Console AWS]

Passo 1.2: Navegar para o ECR
Na barra de busca superior, digite "ECR"
Clique em "Elastic Container Registry"
[Espaço para print: Busca pelo ECR]

Passo 1.3: Criar um repositório
Clique em "Create repository"
Configure:
Visibility settings: Private
Repository name: meu-website
Tag immutability: Disabled (padrão)
Scan on push: Enabled (recomendado para segurança)
Clique em "Create repository"
[Espaço para print: Formulário de criação do repositório]

Passo 1.4: Anotar a URI do repositório
Após criar, você verá algo como:

123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website
⚠️ Importante: Copie e guarde esta URI, você precisará dela!

[Espaço para print: Repositório criado com a URI visível]

📤 Fase 2: Push da Imagem para o ECR
Passo 2.1: Configurar AWS CLI
Se ainda não configurou, execute:

aws configure
Você precisará fornecer:

AWS Access Key ID: Obtida no IAM
AWS Secret Access Key: Obtida no IAM
Default region: ex: us-east-1
Default output format: json
Passo 5.2: Autenticar Docker com ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com
⚠️ Substitua:

us-east-1 pela sua região
123456789012 pelo seu Account ID
Você deve ver:

Login Succeeded
[Espaço para print: Login bem-sucedido no ECR]

Passo 2.3: Tagar a imagem para o ECR
docker tag meu-website:v1.0 123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website:v1.0
Passo 2.4: Push da imagem
docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website:v1.0
Você verá o progresso do upload:

The push refers to repository [123456789012.dkr.ecr.us-east-1.amazonaws.com/meu-website]
abc123: Pushed
def456: Pushed
v1.0: digest: sha256:xyz789... size: 1234
[Espaço para print: Push concluído]

Passo 2.5: Verificar no Console AWS
Volte ao ECR no console AWS
Clique no seu repositório
Você deve ver a imagem com a tag v1.0
