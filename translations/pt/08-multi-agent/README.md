# Padrões de Design para Multiagentes

Assim que você começar a trabalhar em um projeto que envolve múltiplos agentes, será necessário considerar o padrão de design para multiagentes. No entanto, pode não ser imediatamente claro quando mudar para um sistema multiagente e quais são as vantagens disso.

## Introdução

Nesta lição, buscamos responder às seguintes perguntas:

- Quais são os cenários onde os multiagentes são aplicáveis? 
- Quais são as vantagens de usar multiagentes em vez de um único agente realizando múltiplas tarefas? 
- Quais são os componentes fundamentais para implementar o padrão de design para multiagentes? 
- Como podemos ter visibilidade sobre como os múltiplos agentes estão interagindo entre si?

## Objetivos de Aprendizagem

Após esta lição, você deverá ser capaz de:

- Identificar cenários onde os multiagentes são aplicáveis.
- Reconhecer as vantagens de usar multiagentes em vez de um único agente.
- Compreender os componentes fundamentais para implementar o padrão de design para multiagentes.

Qual é o panorama geral?

*Multiagentes são um padrão de design que permite que múltiplos agentes trabalhem juntos para alcançar um objetivo comum.* 

Esse padrão é amplamente utilizado em diversos campos, incluindo robótica, sistemas autônomos e computação distribuída.

## Cenários Onde Multiagentes São Aplicáveis

Então, em quais cenários o uso de multiagentes é uma boa escolha? A resposta é que há muitos cenários onde empregar múltiplos agentes é benéfico, especialmente nos seguintes casos:

- **Grandes volumes de trabalho**: Tarefas extensas podem ser divididas em partes menores e atribuídas a diferentes agentes, permitindo processamento paralelo e conclusão mais rápida. Um exemplo disso é no caso de uma tarefa de processamento de dados em larga escala.
- **Tarefas complexas**: Tarefas complexas, assim como grandes volumes de trabalho, podem ser divididas em subtarefas menores e atribuídas a diferentes agentes, cada um especializado em um aspecto específico da tarefa. Um bom exemplo disso é no caso de veículos autônomos, onde diferentes agentes gerenciam navegação, detecção de obstáculos e comunicação com outros veículos.
- **Diversidade de especialização**: Diferentes agentes podem ter especializações distintas, permitindo que lidem com diferentes aspectos de uma tarefa de forma mais eficaz do que um único agente. Um bom exemplo disso é no setor de saúde, onde agentes podem gerenciar diagnósticos, planos de tratamento e monitoramento de pacientes.

## Vantagens de Usar Multiagentes em Comparação a um Único Agente

Um sistema com um único agente pode funcionar bem para tarefas simples, mas para tarefas mais complexas, usar múltiplos agentes pode oferecer várias vantagens:

- **Especialização**: Cada agente pode ser especializado para uma tarefa específica. A falta de especialização em um único agente significa que ele pode fazer de tudo, mas pode se confundir ao lidar com tarefas complexas. Ele pode, por exemplo, acabar realizando uma tarefa para a qual não é o mais adequado.
- **Escalabilidade**: É mais fácil escalar sistemas adicionando mais agentes em vez de sobrecarregar um único agente.
- **Tolerância a falhas**: Se um agente falhar, outros podem continuar funcionando, garantindo a confiabilidade do sistema.

Vamos a um exemplo: reservar uma viagem para um usuário. Um sistema com um único agente teria que lidar com todos os aspectos do processo de reserva, desde encontrar voos até reservar hotéis e carros de aluguel. Para fazer isso com um único agente, ele precisaria de ferramentas para lidar com todas essas tarefas. Isso poderia levar a um sistema complexo e monolítico, difícil de manter e escalar. Um sistema multiagente, por outro lado, poderia ter diferentes agentes especializados em encontrar voos, reservar hotéis e carros de aluguel. Isso tornaria o sistema mais modular, fácil de manter e escalável.

Compare isso a uma agência de viagens administrada como um pequeno negócio familiar versus uma agência operada como uma franquia. O negócio familiar teria um único agente lidando com todos os aspectos do processo de reserva, enquanto a franquia teria diferentes agentes responsáveis por diferentes aspectos do processo.

## Componentes Fundamentais para Implementar o Padrão de Design para Multiagentes

Antes de implementar o padrão de design para multiagentes, é necessário entender os componentes que compõem esse padrão.

Vamos tornar isso mais concreto analisando novamente o exemplo de reservar uma viagem para um usuário. Nesse caso, os componentes fundamentais incluiriam:

- **Comunicação entre agentes**: Agentes responsáveis por encontrar voos, reservar hotéis e carros de aluguel precisam se comunicar e compartilhar informações sobre as preferências e restrições do usuário. É necessário decidir os protocolos e métodos para essa comunicação. Concretamente, isso significa que o agente responsável por encontrar voos precisa se comunicar com o agente de reservas de hotéis para garantir que o hotel seja reservado para as mesmas datas do voo. Isso significa que os agentes precisam compartilhar informações sobre as datas de viagem do usuário, ou seja, você precisa decidir *quais agentes compartilham informações e como fazem isso*.
- **Mecanismos de coordenação**: Os agentes precisam coordenar suas ações para garantir que as preferências e restrições do usuário sejam atendidas. Por exemplo, uma preferência do usuário pode ser ficar em um hotel próximo ao aeroporto, enquanto uma restrição pode ser que carros de aluguel só estejam disponíveis no aeroporto. Isso significa que o agente de reservas de hotéis precisa coordenar-se com o agente de aluguel de carros para atender às preferências e restrições do usuário. Isso implica decidir *como os agentes coordenam suas ações*.
- **Arquitetura dos agentes**: Os agentes precisam ter uma estrutura interna para tomar decisões e aprender com as interações com o usuário. Por exemplo, o agente responsável por encontrar voos precisa ter a capacidade interna de decidir quais voos recomendar ao usuário. Isso significa que você precisa decidir *como os agentes tomam decisões e aprendem com as interações com o usuário*. Um exemplo de como um agente pode aprender e melhorar seria o uso de um modelo de aprendizado de máquina para recomendar voos com base nas preferências anteriores do usuário.
- **Visibilidade nas interações entre agentes**: É essencial ter visibilidade sobre como os múltiplos agentes estão interagindo entre si. Isso requer ferramentas e técnicas para rastrear as atividades e interações dos agentes. Isso pode incluir ferramentas de registro e monitoramento, ferramentas de visualização e métricas de desempenho.
- **Padrões para sistemas multiagentes**: Existem diferentes padrões para implementar sistemas multiagentes, como arquiteturas centralizadas, descentralizadas e híbridas. É necessário escolher o padrão que melhor se adapta ao seu caso de uso.
- **Humano no ciclo**: Na maioria dos casos, haverá um humano no ciclo, e será necessário instruir os agentes sobre quando pedir intervenção humana. Isso pode incluir, por exemplo, um usuário solicitando um hotel ou voo específico que os agentes não recomendaram ou pedindo confirmação antes de reservar um voo ou hotel.

## Visibilidade nas Interações entre Multiagentes

É importante ter visibilidade sobre como os múltiplos agentes estão interagindo entre si. Essa visibilidade é essencial para depurar, otimizar e garantir a eficácia geral do sistema. Para isso, é necessário ter ferramentas e técnicas para rastrear as atividades e interações dos agentes. Isso pode incluir ferramentas de registro e monitoramento, ferramentas de visualização e métricas de desempenho.

Por exemplo, no caso de reservar uma viagem para um usuário, você poderia ter um painel que mostra o status de cada agente, as preferências e restrições do usuário e as interações entre os agentes. Esse painel poderia exibir as datas de viagem do usuário, os voos recomendados pelo agente de voos, os hotéis recomendados pelo agente de hotéis e os carros de aluguel recomendados pelo agente de aluguel de carros. Isso daria uma visão clara de como os agentes estão interagindo entre si e se as preferências e restrições do usuário estão sendo atendidas.

Vamos analisar cada um desses aspectos com mais detalhes:

- **Ferramentas de Registro e Monitoramento**: É importante registrar cada ação tomada por um agente. Um registro pode armazenar informações sobre o agente que realizou a ação, a ação realizada, o horário em que a ação foi realizada e o resultado da ação. Essas informações podem ser usadas para depuração, otimização e mais.
- **Ferramentas de Visualização**: Ferramentas de visualização podem ajudar a entender as interações entre os agentes de forma mais intuitiva. Por exemplo, um gráfico que mostra o fluxo de informações entre os agentes pode ajudar a identificar gargalos, ineficiências e outros problemas no sistema.
- **Métricas de Desempenho**: Métricas de desempenho ajudam a monitorar a eficácia do sistema multiagente. Por exemplo, você pode rastrear o tempo necessário para concluir uma tarefa, o número de tarefas concluídas por unidade de tempo e a precisão das recomendações feitas pelos agentes. Essas informações podem ajudar a identificar áreas de melhoria e otimizar o sistema.

## Padrões para Multiagentes

Vamos explorar alguns padrões concretos que podem ser usados para criar aplicativos multiagentes. Aqui estão alguns padrões interessantes a considerar:

### Chat em Grupo

Esse padrão é útil quando você deseja criar um aplicativo de chat em grupo onde múltiplos agentes possam se comunicar entre si. Casos típicos de uso incluem colaboração em equipe, suporte ao cliente e redes sociais.

Nesse padrão, cada agente representa um usuário no chat em grupo, e as mensagens são trocadas entre os agentes usando um protocolo de mensagens. Os agentes podem enviar mensagens ao chat em grupo, receber mensagens do chat em grupo e responder a mensagens de outros agentes.

Esse padrão pode ser implementado usando uma arquitetura centralizada, onde todas as mensagens passam por um servidor central, ou uma arquitetura descentralizada, onde as mensagens são trocadas diretamente.

![Chat em grupo](../../../translated_images/multi-agent-group-chat.82d537c5c8dc833abbd252033e60874bc9d00df7193888b3377f8426449a0b20.pt.png)

### Transferência de Tarefas

Esse padrão é útil quando você deseja criar um aplicativo onde múltiplos agentes possam transferir tarefas entre si.

Casos típicos de uso incluem suporte ao cliente, gerenciamento de tarefas e automação de fluxos de trabalho.

Nesse padrão, cada agente representa uma tarefa ou etapa em um fluxo de trabalho, e os agentes podem transferir tarefas para outros agentes com base em regras predefinidas.

![Transferência de tarefas](../../../translated_images/multi-agent-hand-off.ed4f0a5a58614a8a3e962fc476187e630a3ba309d066e460f017b503d0b84cfc.pt.png)

### Filtragem Colaborativa

Esse padrão é útil quando você deseja criar um aplicativo onde múltiplos agentes possam colaborar para fazer recomendações aos usuários.

A razão para ter múltiplos agentes colaborando é que cada agente pode ter uma especialização diferente e contribuir de maneiras distintas para o processo de recomendação.

Vamos tomar como exemplo um usuário que deseja uma recomendação sobre a melhor ação para comprar no mercado financeiro.

- **Especialista em indústria**: Um agente pode ser especialista em um setor específico. 
- **Análise técnica**: Outro agente pode ser especialista em análise técnica. 
- **Análise fundamentalista**: E outro agente pode ser especialista em análise fundamentalista. Colaborando, esses agentes podem fornecer uma recomendação mais abrangente ao usuário.

![Recomendação](../../../translated_images/multi-agent-filtering.719217d169391ddb118bbb726b19d4d89ee139f960f8749ccb2400efb4d0ce79.pt.png)

## Cenário: Processo de Reembolso

Considere um cenário em que um cliente está tentando obter o reembolso de um produto. Pode haver diversos agentes envolvidos nesse processo, mas vamos dividi-los entre agentes específicos para esse processo e agentes gerais que podem ser usados em outros processos.

**Agentes específicos para o processo de reembolso**:

Abaixo estão alguns agentes que poderiam estar envolvidos no processo de reembolso:

- **Agente do cliente**: Representa o cliente e é responsável por iniciar o processo de reembolso.
- **Agente do vendedor**: Representa o vendedor e é responsável por processar o reembolso.
- **Agente de pagamento**: Representa o processo de pagamento e é responsável por reembolsar o pagamento do cliente.
- **Agente de resolução**: Representa o processo de resolução e é responsável por resolver quaisquer problemas que surjam durante o processo de reembolso.
- **Agente de conformidade**: Representa o processo de conformidade e é responsável por garantir que o processo de reembolso esteja em conformidade com regulamentos e políticas.

**Agentes gerais**:

Esses agentes podem ser usados em outras partes do seu negócio.

- **Agente de envio**: Representa o processo de envio e é responsável por enviar o produto de volta ao vendedor. Esse agente pode ser usado tanto no processo de reembolso quanto no envio geral de um produto, como em uma compra.
- **Agente de feedback**: Representa o processo de feedback e é responsável por coletar feedback do cliente. O feedback pode ser coletado a qualquer momento, não apenas durante o processo de reembolso.
- **Agente de escalonamento**: Representa o processo de escalonamento e é responsável por escalar problemas para um nível superior de suporte. Esse tipo de agente pode ser usado em qualquer processo onde seja necessário escalar um problema.
- **Agente de notificações**: Representa o processo de notificações e é responsável por enviar notificações ao cliente em várias etapas do processo de reembolso.
- **Agente de análise**: Representa o processo de análise e é responsável por analisar dados relacionados ao processo de reembolso.
- **Agente de auditoria**: Representa o processo de auditoria e é responsável por auditar o processo de reembolso para garantir que ele esteja sendo conduzido corretamente.
- **Agente de relatórios**: Representa o processo de relatórios e é responsável por gerar relatórios sobre o processo de reembolso.
- **Agente de conhecimento**: Representa o processo de conhecimento e é responsável por manter uma base de conhecimento com informações relacionadas ao processo de reembolso. Esse agente pode ser útil tanto para reembolsos quanto para outras partes do seu negócio.
- **Agente de segurança**: Representa o processo de segurança e é responsável por garantir a segurança do processo de reembolso.
- **Agente de qualidade**: Representa o processo de qualidade e é responsável por garantir a qualidade do processo de reembolso.

Há uma grande variedade de agentes listados acima, tanto para o processo específico de reembolso quanto para os agentes gerais que podem ser usados em outras partes do seu negócio. Esperamos que isso lhe dê uma ideia de como decidir quais agentes usar em seu sistema multiagente.

## Tarefa

Qual seria uma boa tarefa para esta lição?

Projete um sistema multiagente para um processo de suporte ao cliente. Identifique os agentes envolvidos no processo, seus papéis e responsabilidades, e como eles interagem entre si. Considere tanto os agentes específicos para o processo de suporte ao cliente quanto os agentes gerais que podem ser usados em outras partes do seu negócio.

> Pense um pouco antes de ler a solução abaixo; você pode precisar de mais agentes do que imagina.

> TIP: Pense nas diferentes etapas do processo de suporte ao cliente e também considere os agentes necessários para qualquer sistema.

## Solução

[Solução](./solution/solution.md)

## Verificações de Conhecimento

Pergunta: Quando você deve considerar o uso de multiagentes?

- [] A1: Quando você tem uma carga de trabalho pequena e uma tarefa simples.
- [] A2: Quando você tem uma grande carga de trabalho.
- [] A3: Quando você tem uma tarefa simples.

[Quiz de solução](./solution/solution-quiz.md)

## Resumo

Nesta lição, exploramos o padrão de design para multiagentes, incluindo os cenários onde os multiagentes são aplicáveis, as vantagens de usar multiagentes em vez de um único agente, os componentes fundamentais para implementar o padrão de design para multiagentes e como ter visibilidade sobre como os múltiplos agentes estão interagindo entre si.

## Recursos adicionais

- [Padrões de design Autogen](https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/intro.html)
- [Padrões de design agentic](https://www.analyticsvidhya.com/blog/2024/10/agentic-design-patterns/)
```

**Aviso Legal**:  
Este documento foi traduzido usando serviços de tradução automática baseados em IA. Embora nos esforcemos para garantir a precisão, esteja ciente de que traduções automatizadas podem conter erros ou imprecisões. O documento original em seu idioma nativo deve ser considerado a fonte autoritária. Para informações críticas, recomenda-se a tradução profissional feita por humanos. Não nos responsabilizamos por mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.