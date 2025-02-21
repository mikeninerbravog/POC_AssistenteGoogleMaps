# Assistente Virtual - Prova de Conceito (POC)

## Aluno
Marcello dos Santos

## Bootcamp
BairesDev - Machine Learning Practitioner - Fevereiro 2025

## Descrição
Este projeto consiste na criação de um assistente virtual baseado em **Processamento de Linguagem Natural (NLP)**. O sistema é capaz de converter áudio em texto (*Speech-to-Text*), identificar intenções e realizar buscas no Google Maps com base nos comandos de voz do usuário.

### Funcionalidades
- Captura de áudio via microfone e conversão para texto
- Interpretação do comando e busca no Google Maps
- Resposta por voz confirmando a pesquisa antes de abrir o navegador
- Loop contínuo até o usuário encerrar

## Requisitos
O sistema foi desenvolvido e testado no **Python 3.11**. Para garantir a execução correta, instale as dependências abaixo.

### Dependências
Instale os pacotes necessários com:
```bash
pip install -r requirements.txt
```
Se ainda não gerou o arquivo `requirements.txt`, utilize:
```bash
pip freeze > requirements.txt
```

### Instalação de Pacotes Específicos
Caso tenha problemas com **PyAudio** no Linux, instale a biblioteca **PortAudio** antes:
```bash
sudo apt update
sudo apt install portaudio19-dev
pip install pyaudio
```
No Windows, pode ser necessário instalar via **pipwin**:
```bash
pip install pipwin
pipwin install pyaudio
```
Além disso, foi necessário instalar o **pygobject** para compatibilidade com o sistema:
```bash
pip install pygobject
```

## Uso
Para rodar o assistente virtual, execute:
```bash
python nome_do_script.py
```
O assistente iniciará perguntando **"O que você deseja procurar no Google Maps?"**. Basta falar um local ou serviço desejado. O sistema continuará capturando comandos até que o usuário diga **"fim"**, **"encerrar"** ou **"sair"**.

### Exemplo de Comandos
- "Restaurante japonês no Leblon"
- "Gesseiro perto de mim"
- "Farmácia 24 horas em Copacabana"

## Estrutura do Código
### 1. Conversão de Texto em Fala (*Text-to-Speech - TTS*)
Utiliza `gTTS` para transformar texto em áudio, permitindo que o assistente responda confirmando a busca.

### 2. Captura e Reconhecimento de Voz (*Speech-to-Text - STT*)
Usa `speech_recognition` para capturar a fala e converter para texto. Ajustes foram feitos para evitar cortes na captura.

### 3. Busca no Google Maps
Gera a URL dinâmica para pesquisa no Google Maps e a abre automaticamente no navegador.

### 4. Loop Principal
Mantém o sistema ativo, ouvindo novos comandos até que o usuário decida encerrar.

## Erros Comuns e Soluções
### Erro `speech_recognition.exceptions.WaitTimeoutError`
Se ocorrer erro de timeout ao esperar o áudio, remova o `timeout` na função de captura:
```python
audio = recognizer.listen(source)
```
### Mensagens de Erro do ALSA no Linux
Para suprimir mensagens como **"unable to open slave"**, execute:
```bash
sudo apt update
sudo apt install alsa-utils pulseaudio libasound2-plugins
pulseaudio --kill
pulseaudio --start
```
Se quiser apenas ocultar os avisos sem corrigir, rode o script com:
```bash
python nome_do_script.py 2>/dev/null
```

## Conclusão
Este projeto demonstra a aplicação de **Machine Learning e NLP** para criar um assistente de voz funcional. O código foi otimizado para evitar cortes no reconhecimento de fala e melhorar a precisão da busca. O assistente pode ser facilmente expandido para outras aplicações como bots conversacionais, automação de tarefas e integração com APIs externas.

