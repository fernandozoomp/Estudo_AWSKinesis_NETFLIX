# Estudo_AWSKinesis_NETFLIX
Estudo de caso da Netflix e do Amazon Kinesis Data Streams


<H4>A Netflix é a principal rede televisiva online do mundo, com mais de 100 milhões de membros em mais de 190 países aproveitando 125 milhões de horas de programas de TV e filmes por dia. Os membros podem assistir o quanto quiserem, a qualquer hora, em qualquer lugar, em praticamente qualquer dispositivo conectado à Internet.<BR>
  
  ## Monitoramento de aplicações em escala enorme
  
A Netflix utiliza a Amazon Web Services (AWS) para quase todas as suas necessidades de computação e armazenamento, incluindo bancos de dados, análises, mecanismos de recomendação, transcodificação de vídeo e muito mais – centenas de funções que, no total, usam mais de 100.000 instâncias de servidor na AWS.

Isso resulta em um ambiente de rede extremamente complexo e dinâmico, no qual as aplicações estão constantemente se comunicando na AWS e pela Internet. Monitorar e otimizar sua rede é fundamental para a Netflix continuar melhorando a experiência do cliente, aumentando a eficiência e reduzindo custos. Particularmente, a Netflix precisava de uma solução para ingerir, aumentar e analisar os vários terabytes de dados que sua rede gera diariamente na forma de logs de fluxo de Virtual Private Cloud (VPC). Isso permitiria à Netflix identificar oportunidades de melhoria de performance, como identificar aplicações que estão se comunicando entre regiões e colocalizá-las. A empresa também poderia aumentar o tempo de atividade, detectando e mitigando rapidamente o tempo de inatividade da aplicação.

Cada registro de log carrega informações sobre as comunicações entre dois endereços IP. No entanto, em um ambiente dinâmico como o da Netflix, em que um endereço IP pode flutuar entre aplicações todos os dias ou até minuto a minuto, os endereços IP não têm muito sentido. “As fontes de dados que tínhamos antes de tomarmos essa iniciativa eram unilaterais”, conta John Bennett, engenheiro de software sênior da Netflix. “Sabíamos que uma aplicação estava se conectando a outras, mas não conhecíamos os dois lados da conversa nem sabíamos como otimizar essas comunicações ou o posicionamento das aplicações na rede.”

A Netflix decidiu estabelecer uma nova fonte de dados que pudesse fornecer mais informações sobre a comunicação entre aplicações e regiões, combinando os logs de fluxo da VPC com os metadados da aplicação.


<div align="center">


![Painel](https://raw.githubusercontent.com/fernandozoomp/Estudo_AWSKinesis_NETFLIX/main/data/painel_netflix.png)

</div>


## Centralização de logs de fluxo usando o Amazon Kinesis Data Streams

Desde o início, a AWS permitiu à Netflix experimentar diferentes abordagens para analisar seus dados de rede. “No início do processo de design, a flexibilidade para experimentar diferentes maneiras de processar os dados era importante”, diz Bennett. “Experimentamos vários designs e usamos muitos produtos da AWS para chegar até aqui.”

A solução que a Netflix finalmente implantou – conhecida internamente como Dredge – centraliza os logs de fluxo usando o Amazon Kinesis Data Streams. A aplicação lê os dados do Amazon Kinesis Data Streams em tempo real e enriquece os endereços IP com metadados da aplicação para fornecer uma imagem completa do ambiente de rede. “Normalmente, colocaríamos os dados em um banco de dados, o que criaria um índice para permitir consultas mais rápidas”, diz Bennett. “O Dredge une os logs de fluxo aos metadados da aplicação à medida que os transmite e os indexa sem usar um banco de dados, o que elimina grande parte da complexidade.”

Os dados enriquecidos chegam a uma aplicação de análise de código aberto chamada Druid. A Netflix usa a funcionalidade de consulta OLAP do Druid para dividir rapidamente os dados em regiões, zonas de disponibilidade e janelas de tempo para visualizá-los e obter insights sobre o comportamento e a performance da rede.

A AWS foi a escolha lógica para o Dredge em parte porque os dados já estavam na Nuvem AWS. “Seria assustador publicar, transmitir e consumir tanta informação de um sistema externo como o Kafka”, afirma Bennett. “Foram necessárias apenas algumas chamadas à API para centralizar vários terabytes de logs de fluxo no Amazon Kinesis Data Streams. Agora, podemos nos concentrar em obter insights a partir dos dados, em vez de simplesmente obter acesso a eles.”

A escalabilidade do Amazon Kinesis Data Streams foi uma boa opção para a aplicação Dredge, devido à natureza cíclica e elástica do uso da rede na Netflix. “Quando se trata de nossos dados de rede, é mais econômico conseguir aumentar e diminuir a capacidade, o que não é tão fácil de fazer com alternativas diferentes do Amazon Kinesis Data Streams”, conta Bennett.

<div align="center">

![Arquitetura](https://raw.githubusercontent.com/fernandozoomp/Estudo_AWSKinesis_NETFLIX/main/data/arquitetura.png)

</div>

## Melhorar a experiência do cliente com o monitoramento de rede em tempo real

A solução da Netflix baseada no Amazon Kinesis Data Streams provou ser altamente escalável, processando diariamente bilhões de fluxos de tráfego. Normalmente, cerca de 1.000 fragmentos do Amazon Kinesis trabalham paralelamente para processar stream de dados. “O Amazon Kinesis Data Streams processa vários terabytes de dados de logs diariamente; no entanto, os eventos aparecem em nossas análises em segundos”, afirma Bennett. “Nós podemos descobrir e responder problemas em tempo real, garantindo a alta disponibilidade e uma boa experiência de cliente.”

Agora, a Netflix consegue identificar novas maneiras de otimizar suas aplicações, e isso pode resultar em transferências de aplicações de uma região para outra ou adoção de um protocolo de rede mais apropriado para um tipo específico de tráfego. “Nossa solução criada no Amazon Kinesis nos permite identificar maneiras de aumentar a eficiência, reduzir custos e melhorar a resiliência para obter a melhor experiência do cliente”, diz Bennett.

Embora uma solução de streaming de dados não seja nova na indústria de TI, é uma inovação no espaço de rede. “A Netflix investe fortemente na AWS em parte porque abstrai a rede subjacente; portanto, não precisamos lidar com switches e roteadores”, afirma Bennett. “Estamos monitorando, analisando e otimizando em um nível mais alto da pilha, de maneiras que nunca consideraríamos se estivéssemos executando nossos próprios datacenters.”

### Fonte: aws.amazon.com
