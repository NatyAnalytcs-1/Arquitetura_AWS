# Arquitetura AWS - Upload de Arquivos com Presigned URL

Esta arquitetura permite que usuários façam **upload de arquivos diretamente no Amazon S3**, de forma segura e escalável, utilizando **Presigned URLs**.


<div align="center">
  <img src="imagem_2025-09-15_102327089.PNG" alt="c" height="300">
</div>



## Fluxo da Arquitetura

1. **Requisição de URL de Upload**  
   - O usuário faz uma requisição **HTTP GET** para o endpoint `/getUploadUrl`.  
   - A requisição chega ao **API Gateway**, que invoca uma **AWS Lambda**.  
   - A função Lambda gera uma **Presigned URL** do S3 (um link temporário com permissões controladas).  

2. **Upload do Arquivo**  
   - O usuário recebe a Presigned URL e realiza uma requisição **HTTP PUT** diretamente no **Amazon S3**.  
   - Dessa forma, o arquivo é armazenado sem passar pelo servidor da aplicação, garantindo mais performance e menor custo.

## Benefícios

- **Escalabilidade**: O upload vai diretamente para o S3, sem sobrecarregar servidores intermediários.  
- **Segurança**: As Presigned URLs expiram em um tempo configurado, limitando o acesso.  
- **Custo otimizado**: Reduz a necessidade de infraestrutura adicional para processar uploads.  
- **Simplicidade**: O controle de autenticação e autorização pode ser delegado ao API Gateway e Lambda.  

---
**Resumo:**  
O usuário solicita uma Presigned URL via **API Gateway + Lambda** e faz o upload direto para o **Amazon S3**, sem necessidade de que o backend manipule os arquivos.
