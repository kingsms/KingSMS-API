# KingSMS-API

Bem vindo a API SMS da KingSMS. Com ela você pode fazer [Envio de SMS](http://www.kingsms.com.br) para todas
as operadoras de forma simples e prática.

##  Visão Geral

Este documento descreve as características técnicas da API para integração com a
KingSMS, visando permitir o desenvolvimento da comunicação entre as plataformas
envolvidas.


##  Definição do Protocolo

O protocolo está baseado em comunicação REST entre o KingSMS e a plataforma do Cliente.

As mensagens de comunicação deverão ser enviadas para a API em formato
(GET ou POST) é o retorno para cada chamada será um JSON cujo formato
é detalhado ao longo desta documentação.



# Enviar SMS 

|  Campo | Descrição  | Valor  |
|-------|--------|-------|
| acao  |  Identificador do Serviço |  sendsms ou bulksms |
| login | Login de acesso  | (Obrigatório)  |
| token | Token de acesso  | (Obrigatório) |
| numero | Número de destino (DDnumero) | Separar com virgula em caso de bulksms |
| campanha | Nome da Campanha | (Opcional) |
| msg | Mensagem | Até 160 caracteres (Sem Acentuação) |


**Exemplo:**

http://painel.kingsms.com.br/kingsms/api.php?acao=sendsms&login=seulogin&token=seutoken&numero=11999999999&msg=teste


**Resposta (JSON):**

{"status":"success","cause":"SMS Add Queue","id":"189"}

``id: Identificador da mensagem``
***

**Retorno de Erros:**

{"status":"error","cause":"Action Not Informed OR Invalid"}

{"status":"error","cause":"Incorrect Login"}

{"status":"error","cause":"Incorrect Token"}

{"status":"error","cause":"Number Not Informed"}

{"status":"error","cause":"Invalid Number"}

{"status":"error","cause":"Incorrect Number Format"}

{"status":"error","cause":"Number Not Movel"}

{"status":"error","cause":"Message Not Informed"}

{"status":"error","cause":"Number of characters > 160"}

{"status":"error","cause":"Without Credit"}


 
 
# Status de Retorno

|  Campo | Descrição  | Valor  | 
|---|---|---|
| acao  |  Identificador do Serviço |  reportsms |  
| login | Login de acesso  | (Obrigatório)  |   
| id | Identificador da mensagem | (Obrigatório) |   


**Exemplo:**

http://painel.kingsms.com.br/kingsms/api.php?acao=reportsms&login=seulogin&id=181


**Resposta (JSON):**

{"status":"success","cause":"SendingOK"}

{"status":"pending":"SMS still in the send Queue"}
***

**Retorno de Erros:**

{"status":"error","cause":"Action Not Informed OR Invalid"}

{"status":"error","cause":"SendingError"}

{"status":"error","cause":"ID Not Informed"}

{"status":"error","cause":"ID Not Found"}


# Consulta Saldo 

|  Campo | Descrição  | Valor  | 
|---|---|---|
| acao  |  Identificador do Serviço |  saldo |  
| login | Login de acesso  | (Obrigatório)  |   
| token | Token de acesso | (Obrigatório) |   


**Exemplo:**

http://painel.kingsms.com.br/kingsms/api.php?acao=saldo&login=seulogin&token=seutoken

**Resposta (JSON):**

{"status":"success","cause":"Credit 1 SMS"}

***

**Retorno de Erros:**

{"status":"error","cause":"Action Not Informed OR Invalid"}

{"status":"error","cause":"Incorrect Login"}

{"status":"error","cause":"Incorrect Token"}



# Resposta SMS

|  Campo | Descrição  | Valor  | 
|---|---|---|
| acao  |  Identificador do Serviço |  inbox |  
| login | Login de acesso  | (Obrigatório)  |   
| flag | Lista as Respostas recebidas (Lidos e não Lidos) | unread |   


**Exemplo:**

http://painel.kingsms.com.br/kingsms/api.php?acao=inbox&login=seulogin&flag=unread


``Campo: flag``

``read = Lista as Respostas que já foram lidas pela API.``

``unread = Lista as Respostas que ainda não foram lidas pela API.``

**Resposta (JSON):**

{"status":"success","cause":"Inbox Empty"}

[{"ID":"4523244","ReceivingDateTime":"2018-11-16 11:31:02","SenderNumber":"11999999999","Text":"Ok"}]

***

**Retorno de Erros:**

{"status":"error","cause":"Action Not Informed OR Invalid"}

{"status":"error","cause":"Incorrect Login"}



# Exemplo PHP

## Envio via PHP

> ###### `<?php`
> ###### `$login = 'seulogin';`
> ###### `$token = 'seutoken';`
> ###### `$numero = 'seunumero';`
> ###### `$msg = urlencode("teste sms");`
> ###### `$send = file_get_contents("http://painel.kingsms.com.br/kingsms/api.php?acao=sendsms&login=$login&token=$token&numero=$numero&msg=$msg");` 
> ###### `echo $send;`
> ###### `?>`

Substitua onde tem seulogin pelo Login que você se cadastrou e seutoken pelo Token que está no seu Painel em Home >> Informações da Conta.


# KingSMS

A [KingSMS](http://www.kingsms.com.br) é um Provedor de SMS no Brasil com o objetivo de fornecer soluções de baixo custo através do envio de SMS, podendo ser utilizado para: Divulgação de Produtos, Serviços, Alertas, Avisos, Cobrança, Agendamentos dentre outros. Estamos sempre buscando inovações, agregando novas soluções e acompanhando as tendências e novidades do mercado.


[Visite nosso site](http://www.kingsms.com.br)

