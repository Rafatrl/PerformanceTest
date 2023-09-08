# Teste de Performance
## _Avaliação Técnica - South System_
---

Nesse tutorial serão demostrados a configuração e os resultados de um teste de desempenho, utilizando as seguintes ferramentas de testes:

* JMETER
* BlazeMeter Chrome Extension: Record JMeter

### DESCRIÇÃO DO CENÁRIO DE TESTE
---
>Desenvolva um script de performance para o seguinte cenário:
>**URL**: https://www.blazedemo.com
>**Cenário:** Compra de passagem aérea - Passagem comprada com sucesso.
>**Critério de Aceitação:**
>250 requisições por segundo com um tempo de resposta 90th percentil inferior a 2 segundos.

**Instruções**
--Escolha entre JMeter e Gatling
--Monte um teste de carga e um teste de pico que satisfaçam a vazão do critério de aceitação.
--Anexe o relatório da execução e explique se o critério de aceitação foi satisfatório ou não, além dos motivos que te levaram a essa conclusão.
--Crie o repositório no GitHub (público). Desenvolva a automação e suba o código no repositório (dica: crie primeiro o repositório, copie o link, cole neste campo e submeta o formulário).
--Não se esqueça do README.md, que deve conter
   - Instruções para a execução do script
   - Relatório de execução dos testes
   - Demais considerações pertinentes ao teste


**Configuração do Ambiente:** Todos os testes e configurações demostradas nesse tutorial foram executas em uma máquina configurada:
. | .
--------- | ------
Nome do Sistema Operacional    |	Microsoft Windows 10 Pro
Versão	10.0.19045             |    Compilação 19045
Fabricante do sistema          |	Dell Inc.
Tipo do sistema                |	PC baseado em X64
Processador                    |	Intel(R) Core(TM) i5-10210U CPU @ 1.60GHz, 2112 Mhz, 4 Núcleo(s), 8 Processador(es) ógico(s)
Memória Física (RAM) Instalada |	16,0 GB
Browser                        |	"Chromium";v="116", "Not)A;Brand";v="24", "Google Chrome";v="116"
Jmeter                         |	Apache JMeter Versão: 5.6.2
Java                           |	java version "16.0.1" 2021-04-20

**Resumo:** Essa simulação foi projetada pela extensão do BlazeMeter no chrome, carregada e estruturada no Jmeter, segue o método de configuração logo abaixo.

## 1. Configuração do ambiente no Windows:
---
### 1.1 - Instalando Jmeter
O JMeter tem como pré-requisito a instalação da versão mais atual do JVM. Pode ser baixado aqui: [LINK](https://www.java.com/pt-BR/download/manual.jsp)
Baixe a última versão do pacote .zip do [JMETER](https://jmeter.apache.org/download_jmeter.cgi), na data atual seria o 'apache-jmeter-5.6.2_src.zip', e em seguida, descompacte o conteúdo em local do seu computador. Percorra até a pasta 'user\apache-jmeter-5.6.2\bin' para executar o arquivo "jmeter.bat".
### 1.2 - Instalando extensao BlazeMeter | The Continuous Testing Platform
Acesse a página [BlazeMeter | The Continuous Testing Platform](https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi) para instalar a extensão no navegador Chrome.
### 1.3 - Instalando o JMeter Plugins Manager
Baixar o [JAR File](https://jmeter-plugins.org/get/) e salvar na pasta ‘user\apache-jmeter-5.6.2\lib\ext\’


## Execução do Script
---
### Método de estruturação realizada para o loadTest:
    1 - Após abrir a página da simulação: https://www.blazedemo.com;
    2 - Com a extensão instalada, inicei a gravação do cenário a ser testado;
    3 - Exportei o arqvuivo com extensão rodar no Jmeter;
    4 - Abri o Jmeter e carreguei o arquivo salvo;
    5 - O cenário foi estruturado conforme a simulação solicitada:
        5.1 - Escopo do Cenário:
            [1] - Carregando a página;
            [2] - Selecionando o destino;
            [3] - selecionando o voo;
            [4] - cadastrando os dados.
    6 - Relatório foi exportado, examinado e criado o repositório no github.

### Método de estruturação realizada para o stressTest:
    1 - Reutilizei a configuração do loadTest;
    2 - Configurei uma nova simulação para o stressTest: 
    3 - Relatório foi exportado, examinado e adicionado ao repositório no github.
    
## Analisando os resultados e relatórios
---
### No LoadTest:
##### Escopo de Teste
Foi configurada uma simulação de 250 usuários selecionando trajetos aleatórios, selecionando uma linha específica, onde no setp [3] um 'Constant Timer' de 2 segundos e no step [4] de 6 segundos foram inseridos para dar mais conformidade no tempo de seleção e cadastro dos usuários.

##### Métricas Coletadas
Com o dashboard gerado temos as seguintes informações:
[carregar imagem]

Totalizando um número de **1000 usuários**, o valor da mediana estava dentro do critério de aceite exibindo **0.5 segundos** com percentil 90 do tempo de resposta em **1.2 segundos** totalizando uma média de requisições de **0.6 segundos**, **411KB/seg** de pacotes recebidos e **50KB/seg** de pacotes enviados. O tempo médio de resposta  das requisições ao longo do teste foi de **0.6s**. A análise do tempo de resposta em relação ao volume de requisições consta uma média de **68s** tyransações por segundo, concluindo com **0** percento de erros e falhas.

### No stressTest
##### Escopo de Teste
Foi configurado um grupo de 300 usuários, onde 10 iniciaram acesso ao site e a cada 5 segundos mais 50 usuários surgiam em torno de 30 segundos e passaram a fazer requisições estáveis por 3min30s, posteriormente decaindo 50 usuários a cada 5 segundos até complentar o teste em 3min56s. Totalizando uma simulação com 12803 usuários.

##### Métricas Coletadas
Com o dashboard gerado temos as seguintes informações:
[carregar imagem]

No Teste de Pico o valor da mediana está exibindo **0.7s** com percentil 90 do tempo de resposta em **21.6s** totalizando uma média de requisições de **58 segundos**, **304KB/seg** pacotes recebidos e **36KB/seg** enviados. Tempo médio de resposta das requisições ao longo do tempo de teste foi de **5.8s**. A análise do tempo de resposta em relação ao volume de requisições consta uma média de **49s** concluindo com **0** percento de erros e falhas.

## Relatórios e Resultado de testes
---
- Detalhes sobre o relatório dos testes se encontra nas pastas anexadas: 'relatorioLoad' e 'relatorioStress'.
- Detalhes sobre como baixar e acessar a configuração a ser testada está na pasta 'testes' nos arquivos 'cn1-loadTest.jmx' e 'cn2-stressTest.jmx'.

## Conclusões
---
**Sobre o loadTest**
O teste de carga mostrou um desempenho apropriado para a quantidade de usuários dentro do critério de aceitação e por estar dentro do percentil 90, onde a estatística de experiencia do usuário consideravelmente está fluindo e exercendo seu propósito sem falhas.

**Sobre o stressTest**
No teste de estresse foi simulado uma operação além da sua carga habitual que também apresentou um comportamento sem falhas, houve um atraso de resposta do serviço nas steps [1] e [3] que chegavam a 22 segundos de espera de resposta. A recomendação de melhoria para um futuro evento desse tipo de serviço seria melhorar a configuração da infraestrutura da rede ou usar um serviço AMP para trabalhar com um sistema de integração continua e elaborar cenários com maior tráfego de requisições.
