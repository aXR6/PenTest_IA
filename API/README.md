# API Server para Integração com DeepSeek via Ollama

## Objetivo
Este projeto fornece uma API para a integração com o DeepSeek utilizando o Ollama. Ele permite a análise de dados de scan em um ambiente seguro, eficiente e escalável. O objetivo principal é processar requisições de análise de forma síncrona ou assíncrona, garantindo logs detalhados e um banco de dados para auditoria.

## Funcionalidades
- **Análise de dados** usando DeepSeek via Ollama.
- **Execução síncrona e assíncrona** de análises.
- **Banco de dados SQLite** para armazenar logs de requisições.
- **Compressão de dados** via zlib para otimização de transferência.
- **Registro detalhado de logs** para rastreabilidade.
- **Autenticação via API Key**.
- **Verificação de saúde da API** por meio de um endpoint dedicado.

## Requisitos de Instalação
Antes de rodar o script, certifique-se de instalar os seguintes pacotes e dependências:

### Dependências do Sistema

Este script foi projetado para rodar no **Debian 12**, mas pode ser adaptado para outras distribuições baseadas em Linux.

Instale os pacotes necessários com o seguinte comando:
```sh
sudo apt update && sudo apt install -y python3 python3-pip sqlite3
```

### Dependências Python
As dependências do Python podem ser instaladas com:
```sh
pip3 install flask requests rich
```

### Instalação do Ollama
O Ollama precisa estar instalado e configurado para rodar corretamente. Siga as instruções de instalação na [documentação oficial](https://ollama.ai/).

Certifique-se de que o modelo **deepseek-r1:14b** está baixado e pronto para uso:
```sh
ollama pull deepseek-r1:14b
```

## Como o Script Funciona

1. O servidor Flask é iniciado na porta **5000**.
2. O banco de dados SQLite é inicializado para armazenar logs de requisições.
3. A API expõe dois endpoints principais:
   - `POST /analyze`: Recebe dados para análise e retorna o resultado.
   - `GET /health`: Verifica a saúde do servidor e do Ollama.
4. A análise pode ser executada de forma **síncrona** ou **assíncrona** (via `callback_url`).
5. Os logs de requisições e erros são armazenados no banco de dados e em arquivos de log.

## Executando o Script
Para iniciar a API, execute:
```sh
python3 api_server.py
```

Caso o Ollama não esteja disponível, o servidor será interrompido.

### Testando a API

#### Verificação de Saúde
```sh
curl -X GET http://localhost:5000/health
```

#### Envio de Dados para Análise
```sh
curl -X POST http://localhost:5000/analyze \
     -H "X-API-Key: sk_prod_1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef" \
     -H "Content-Type: application/json" \
     -d '{"scan_data": "exemplo de dados", "context": "detalhes do contexto"}'
```

## Considerações Finais
- Utilize um **reverso proxy** (como Nginx ou Traefik) para expor a API de forma segura.
- Configure um **firewall** para restringir acessos indesejados.
- Utilize **variáveis de ambiente** para armazenar a API Key de forma segura.

Este projeto é um ponto de partida para uma integração robusta com DeepSeek e pode ser expandido conforme as necessidades da aplicação.

## Autor
Desenvolvido por **Thalles Canela**
Última atualização: **08 de fevereiro de 2025**