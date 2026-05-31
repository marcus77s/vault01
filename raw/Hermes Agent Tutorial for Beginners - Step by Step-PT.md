---
title: "Hermes Agent Tutorial for Beginners - Step by Step"
source: "https://www.youtube.com/watch?v=LvWobwr0Neg"
author:
  - "[[Metics Media]]"
published: 2026-05-28
created: 2026-05-30
description: "Hermes Agent tutorial for beginners — learn how to install Hermes Agent on a VPS, complete Hermes Agent setup with Telegram, give it skills, and schedule jobs that run while you sleep. No coding neede"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=LvWobwr0Neg)

Tutorial do Hermes Agent para iniciantes — aprenda a instalar o Hermes Agent em um VPS, conclua a configuração do Hermes Agent com o Telegram, capacite-o e agende trabalhos que sejam executados enquanto você dorme. Não é necessário codificar.
✅ Hermes VPS (Desconto Exclusivo): https://meticsmedia.com/hermes-YFC
  
Este vídeo aborda:
✔️ O que é o Hermes Agent? — agente de IA de código aberto da Nous Research
Agente ✔️ Hermes vs ChatGPT — principais diferenças explicadas
✔️ Instale o Hermes Agent em um VPS — implantação automática do Hostinger com um clique
✔️ Melhor plano de VPS para agentes de IA — por que KVM2 com Docker
Configuração do ✔️ Hermes Agent — passo a passo completo do terminal do navegador
✔️ Conecte o Hermes Agent ao Telegram — converse com sua IA a partir do seu telefone
✔️ Escolha um modelo de IA no OpenRouter — DeepSeek, Claude Opus 4.7 e mais
✔️ Ensine ao seu agente habilidades reutilizáveis — automatize tarefas repetidas
Memória de IA ✔️ persistente — salva preferências em todos os bate-papos
✔️ Agende trabalhos cron de IA — deixe seu agente trabalhar enquanto você dorme
Exemplo ✔️ do mundo real — pesquisa semanal automatizada de concorrentes
✔️ Acompanhe seus custos de IA — monitore os gastos com OpenRouter e Hostinger
✔️ Mude os modelos de IA em tempo real — usando o comando/model +
✔️ Migre do OpenClaw para o Hermes — com um único comando
✔️ Proteja seu agente de IA auto-hospedado — bloqueie-o apenas para você
  
🔗 Links mencionados no vídeo
Documentação do Agente Hermes: https://hermes-agent.nousresearch.com/docs/
OpenRouter: https://openrouter.ai
Telegram: https://telegram.org/apps
BotFather: https://t.me/BotFather
Bot de Informações do Usuário: https://t.me/userinfobot
  
📍 Ofertas e descontos exclusivos: https://meticsmedia.com/deals
  
* ️ Carimbos de data/hora
00:00 Introdução
00:45 O que é o agente Hermes?
02:44 Inscreva-se no VPS da Hostinger e implante o Hermes
06:29 Abrir o terminal Web e iniciar a configuração
09:23 Escolha o OpenRouter como seu provedor de IA
13:32 Escolha seu modelo de IA
19:13 Inicie o Gateway e Envie Sua Primeira Mensagem
22:29 Habilidades e Memória — Torne o Hermes Útil
28:26 Agendar um trabalho recorrente
30:54 Onde rastrear seus custos
32:59 Outras coisas que seu agente pode fazer
  
Divulgação
Alguns dos links são links de afiliados. Se você fizer uma compra através deles, ganhamos uma pequena comissão sem nenhum custo extra para você. Isso nos ajuda a manter nossos vídeos gratuitos para todos.

Transcrição

Vinheta

**0:00** · Se você está procurando um guia passo a passo claro para configurar seu próprio Agente Hermes, você está no lugar certo. Eu sou Matt e, neste vídeo, vamos colocar seu agente em execução em um pequeno servidor em nuvem, conectá-lo ao Telegram para que você possa enviar mensagens do seu telefone e explicar como dar a ele habilidades que ele pode usar de novo e de novo.

**0:16** · Também mostrarei como agendar trabalhos para que ele possa fazer as coisas por você sozinho, mesmo enquanto você dorme. Se você está preocupado que o vídeo cubra apenas a configuração, não é. Assim que seu agente estiver em execução, analisaremos como realmente usá-lo, quanto custa continuar funcionando e como garantir que ninguém mais possa falar com ele.

**0:33** · No momento em que terminarmos hoje, você terá um agente que escuta no Telegram, executa o trabalho para você em segundo plano e fica um pouco melhor quanto mais você o usa. Você não precisa de nenhuma experiência em codificação para acompanhar, apenas a capacidade de copiar e colar. Antes de tocarmos no servidor, vamos abordar rapidamente o que é um Agente Hermes e por que alguém gostaria de executá-lo.

### O que é o agente Hermes?

**0:51** · O Hermes Agent é um agente de IA gratuito e de código aberto criado por uma equipe chamada Nous Research. A maneira mais simples de pensar sobre isso é esta. É como ter uma versão pessoal do ChatGPT ou QuAD que vive em seu próprio servidor, conversa com você por meio de aplicativos de bate-papo que você já usa e melhora quanto mais você o usa. Há três coisas que o tornam diferente de um chatbot comum. Primeiro, ele funciona sozinho o tempo todo.

**1:13** · Isso significa que ele pode enviar uma mensagem primeiro quando algo acontecer e pode funcionar para você em um cronograma. Um chatbot normal só faz qualquer coisa quando você abre o aplicativo. Em segundo lugar, ele se lembra de como você trabalha. Não apenas os fatos que você conta, a maneira como você gosta que as coisas sejam feitas. Isso cria uma imagem de você em todas as conversas. Terceiro, ele escreve suas próprias habilidades.

**1:33** · Quando você pede para ele fazer algo complexo, ele pode salvar as etapas e reutilizá-las mais tarde, para que fique mais rápido e preciso quanto mais tempo você tiver. Nota rápida sobre onde você pode executar o Hermes. Existem três opções. Seu próprio laptop, uma máquina sobressalente sempre ativa, como um desktop ou um pequeno servidor doméstico, ou um VPS, um pequeno computador na nuvem. Estamos usando um VPS neste vídeo por um motivo específico.

**1:55** · Tudo o que configuramos aqui, as mensagens do Telegram, os trabalhos agendados, o agente entrando em contato com você quando algo acontece, só funciona enquanto o Hermes está funcionando. Um laptop não vai funcionar porque vai dormir. Um sobressalente sempre ligado em uma máquina funciona, mas apenas se você já tiver um, e você estará lidando com sua própria rede e atualizações. Um VPS remove esses dois problemas por menos de $ 10 por mês.

**2:17** · Agora, se você preferir ir pela rota local, a documentação oficial da Hermes orienta você por esse caminho e eu coloquei o link na descrição abaixo. Para todos os outros, o restante deste vídeo orienta você passo a passo pelo caminho do VPS. Agora, mais uma coisa antes de seguirmos em frente. Se você já usou uma ferramenta chamada OpenClaw antes, Hermes é a mesma ideia, mas com memória mais forte, o sistema de habilidades que acabei de mencionar e maior segurança.

**2:39** · O Hermes também pode importar sua configuração do OpenClaw com um comando se você quiser alternar. Agora, a primeira coisa que precisamos é o próprio servidor, então deixe-me mostrar como configurar isso. Vamos usar a Hostinger. O primeiro link na descrição abre uma página que já tem o Hermes Agent pré-selecionado para instalação automática, então não precisamos configurar isso manualmente.

### Inscreva-se no VPS da Hostinger e implante o Hermes

**2:58** · O link também acumula um desconto extra de 10% em cima de qualquer venda que a Hostinger esteja executando no momento, o que torna essa a maneira mais barata de colocar um Agente Hermes online a qualquer momento. Então vá em frente e use o link na tela ou clique no primeiro link na descrição abaixo. Ao clicar nesse link, você acessará esta página aqui e, se clicar no botão Escolher plano, verá as opções de preço.

**3:20** · Você verá alguns planos VPS listados lado a lado. Vamos escolher o KVM 2. Ele vem com dois núcleos de CPU, 8 gigabytes de memória e 100 gigabytes de armazenamento. Quero ser direto com você sobre por que não estamos escolhendo o plano mais barato. Mais adiante neste vídeo, vamos dar ao agente as habilidades que o permitem navegar na web, e o agente já é executado dentro de um contêiner Docker na Hostinger por segurança.

**3:41** · Ambos usam recursos reais. O plano menor pode tecnicamente executar o Hermes, mas não pode executar tudo isso ao mesmo tempo sem desacelerar ou congelar. O KVM 2 também é o plano que a própria Hostinger recomenda para a Hermes. Então vá em frente e clique em Escolher Plano na opção KVM 2. Você será levado para a página do carrinho e a primeira coisa que você quer fazer é selecionar o período para o seu registro.

**4:03** · Você pode escolher 1 mês, 12 meses ou 24 meses, e geralmente obtém o melhor valor, o menor preço por mês em geral se selecionar 24 meses. Mas se isso é demais para você começar, entenda totalmente, eu recomendo selecionar a opção de 12 meses. Esse é o prazo mais baixo que eles permitirão que você selecione e ainda aproveite nosso cupom. Se você selecionar 1 mês, eles não permitem que você use esse desconto extra de 10%.

**4:26** · Em seguida, você pode ver que eles já têm as implantações automáticas do Agente Hermes configuradas para esta opção específica, o que é ótimo. Por último, escolha a localização do seu servidor. Você geralmente quer escolher um local de servidor mais próximo de você ou qualquer outro que tenha a menor latência. Aqui vou selecionar uma dessas opções dos Estados Unidos - Boston, que me dá apenas oito milissegundos de latência, o que é fantástico. Se você quiser proteger sua configuração, você pode também ativar backups automáticos diários.

**4:50** · Por padrão, você recebe backups automáticos semanais. Para mim, tudo bem. Mas se você quiser ter certeza de que tudo está protegido, você pode ligar isso. Quando estiver pronto, clique em Continuar. Na próxima página, registre sua conta.

**5:02** · Na próxima página, insira o seu endereço de faturação e as suas informações de pagamento para concluir o check-out e gostaria de salientar que existe uma garantia de reembolso de 30 dias, por isso, a qualquer momento nos próximos 30 dias, se tiver algum problema, pode entrar em contacto com a Hostinger e receber o seu dinheiro de volta. Ao concluir o checkout, você receberá esta confirmação. Em seguida, a Hostinger coloca você em um pequeno formulário de configuração.

**5:21** · Agora só precisamos escolher as credenciais de administrador para o terminal web Hermes e deixar o servidor construir a si mesmo. Por padrão, eles preenchem o nome de usuário do administrador como Hermes, o que funciona muito bem, e eles fornecem uma senha segura gerada sob medida. Agora clique no ícone do olho para revelar a senha gerada automaticamente.

**5:41** · Estou mostrando a minha aqui porque vou excluir esta conta mais tarde, mas definitivamente certifique-se de não compartilhar isso com ninguém, é assim que você acessa seu agente. Vá em frente e copie este nome de usuário e senha e salve-os em algum lugar seguro e, em seguida, basta clicar em Implantar. A Hostinger agora está construindo seu servidor e instalando o Hermes nele. Isso leva alguns minutos, então vou avançar rapidamente para quando estiver concluído.

**6:04** · Quando terminar, você será encaminhado para o painel da Hostinger e poderá receber uma pesquisa. Você pode preenchê-lo se quiser ou simplesmente clicar em Pular. Há também talvez um pop-up ou dois e você pode simplesmente descartá-los. Bem-vindo ao Docker Manager da Hostinger.

**6:17** · Você pode ver aqui que seu Agente Hermes já está sendo executado em um novo projeto do Docker e tem o tráfego configurado como um proxy reverso para garantir que você possa acessar seu agente de qualquer lugar da web com segurança. Agora precisamos abrir uma janela no servidor para que possamos falar diretamente com o Hermes. Vamos usar o que é chamado de terminal. Essa é a janela somente de texto onde você digita comandos.

### Abra o terminal Web e inicie a configuração

**6:37** · A Hostinger tem um embutido diretamente no navegador, por isso não precisamos instalar nada extra no seu computador. Para abri-lo, basta clicar no botão Terminal no canto superior direito, mas antes de fazer isso, copie as últimas quatro letras do nome do seu projeto Docker aqui. Então deve dizer hermes-agent e depois ter quatro letras. Vá em frente e selecione e, em seguida, copie essas quatro letras.

**6:59** · Tudo bem, agora vá em frente e abra o terminal. Uma nova guia será aberta com uma janela de terminal preta e você já está conectado. Agora, se você nunca usou um terminal antes, ele pode parecer um pouco assustador ou avassalador.

**7:11** · Parece um pouco antiquado ou até mesmo um tipo de hacker, certo?

**7:15** · Mas na verdade é simples. Em vez de clicar com pastas e ícones para interagir com um computador, você está simplesmente digitando texto. É como interagir com um chatbot, mas você precisa inserir comandos muito precisos. Você não pode simplesmente digitar o que quiser. Então, primeiro o que a gente vai fazer é garantir que a gente tenha um cursor piscando aqui. E se isso não estiver piscando, vá em frente e clique na tela do seu terminal e ele deve andamento, ir

**7:42** · Em seguida, digitaremos cd /docker/hermes-agent- e, em seguida, colaremos os quatro caracteres que você copiou anteriormente e, em seguida, pressionaremos Enter ou Return no teclado. Acabamos de fazer isso porque, quando você aterrissa no terminal, todos os comandos digitados vão para o VPS em alto nível, quase como a área de trabalho do seu computador.

**8:14** · Para enviar quaisquer comandos para o seu aplicativo Hermes Agent especificamente, temos que dizer ao terminal para acessar esse programa primeiro, então foi isso que acabamos de fazer. Agora precisamos acessar o contêiner Hermes. Para fazer isso, digite docker compose exec soletrado E-X-E-C, hermes-agent /bin/bash e pressione Enter. Tudo bem, agora vamos ativar o assistente de configuração. Para fazer isso, digite hermes setup e pressione Enter.

**8:59** · Isso inicia o assistente de configuração. É um questionário que o agente executa na primeira vez que inicializa. Ele pergunta qual provedor de IA você deseja usar, qual modelo você deseja por padrão e qual aplicativo de mensagens você deseja falar com ele. Responderemos a cada pergunta juntos. Para começar, o assistente perguntará se você deseja uma configuração rápida ou completa. Vamos seguir em frente e fazer a configuração rápida.

**9:19** · Já está selecionado aqui, então tudo o que você precisa fazer é clicar em Enter.

### Escolha o OpenRouter como seu provedor de IA

**9:23** · A primeira coisa que o assistente pergunta é: qual provedor de IA você deseja usar?

**9:27** · Um provedor é a empresa que executa o modelo real de IA que o agente usa para pensar. Existem mais de 20 opções aqui. Vamos usar um chamado OpenRouter porque dá acesso a muitos modelos diferentes com uma única conta e uma única fatura. Isso significa que você pode alternar entre modelos de IA mais tarde sem se inscrever em nenhum outro lugar.

**9:48** · No assistente aqui, use as teclas de seta do teclado, para cima e para baixo, para realçar o OpenRouter e pressione Enter. O assistente agora solicita sua chave de API do OpenRouter. Deixe a tela aberta no terminal, voltaremos a ela em um minuto. Abra uma nova guia do navegador e acesse openrouter.ai. Você pode digitar isso manualmente ou usar o link na descrição do vídeo abaixo.

**10:14** · Este aqui é o OpenRouter e é a plataforma que nos permite acessar vários modelos diferentes de IA em um só lugar. Agora, o assistente está pedindo o que é chamado de chave de API. Uma chave de API é uma longa string secreta que informa ao OpenRouter que as solicitações estão vindo de você. O Hermes usa uma chave para chamar o modelo de IA e o OpenRouter cobra sua conta pelo que é usado. Trate a chave como uma senha, não a compartilhe com ninguém.

**10:39** · Neste site, clique em Inscrever-se no canto superior direito. Em seguida, siga as etapas para criar uma conta ou entrar. Se você estiver se cadastrando pela primeira vez, precisará verificar seu e-mail. Abra sua caixa de entrada e clique no link. Veja como é esse e-mail, deve ser algo assim.

**10:56** · O sujeito dirá: "Seu link de inscrição" e, em seguida, haverá um botão dentro que diz: "Inscreva-se no OpenRouter." Vá em frente e clique nisso. Na página que abrir, você receberá uma pesquisa. Vá em frente e selecione uma opção e clique em Continuar. E você deve receber uma confirmação. Em seguida, precisaremos adicionar créditos à nossa conta.

**11:12** · Precisamos de apenas uma pequena quantia para começar, então vamos em frente e clicar em Comprar Créditos e depois em Adicionar Créditos. Adicione as suas informações de faturação e, em seguida, adicione uma forma de pagamento. Depois de adicionar a sua forma de pagamento, teremos de adicionar um montante para começar. O padrão é $ 10, o que é muito para começarmos, então vá em frente e clique em Comprar. E você vai receber essa pequena confirmação, você pode simplesmente clicar em OK.

**11:36** · Quando a transação for concluída, você verá que o saldo da sua conta foi atualizado. Ótimo, agora temos crédito. Em seguida, precisamos obter nossa chave. No lado esquerdo, clique em Chaves de API. Em seguida, no canto superior direito, clique em Nova Chave. Você precisará dar um nome à sua chave. Podemos chamá-la de algo como Hermes Agent. Agora, você pode definir um limite de crédito aqui se quiser garantir que sua conta tenha um teto máximo.

**11:59** · Por exemplo, você poderia definir um limite de $20 e então redefini-lo a cada dia, semana ou mês. Vou definir o meu como mensal. E você pode defini-lo para expirar em uma data específica ou deixá-lo como está. Agora, isso é uma proteção de custo. É ótimo porque garante que você nunca gaste mais do que deseja.

**12:18** · Agora, você precisa adicionar créditos, então isso funciona principalmente como uma proteção para quando você tem mais crédito na conta e quer gerenciar como ele é usado ao longo do tempo. Por exemplo, se você tiver 100 créditos na conta e quiser gastar apenas 20 por mês, é assim que você pode gerenciar isso. Você pode deixar em branco se não quiser ter esse limite.

**12:36** · De qualquer forma, configure do jeito que quiser e clique em Criar. Agora, aqui você verá uma longa sequência começando com sk. Esta é sua chave de API. Novamente, é como uma senha, não a compartilhe com ninguém. Vá em frente e copie e salve em algum lugar seguro porque você não poderá vê-la novamente. Se você fechar esta janela sem copiá-la, precisará começar do zero e criar uma nova chave.

**13:00** · Então certifique-se de copiá-la antes de fazer qualquer outra coisa. Tudo bem, vá em frente e volte para a guia do terminal, clique no terminal e cole sua chave de API. Agora, quero destacar que você não verá nada acontecer depois de colá-la. Isso é apenas por questões de segurança para que ninguém que esteja assistindo possa ver informações privadas sendo inseridas no seu terminal, mas ela está lá.

**13:25** · Então, depois de colar, vá em frente e pressione Enter no teclado. E você verá que a chave de API foi salva. Em seguida, o assistente pergunta qual modelo de IA você quer que o Hermes use por padrão. Um modelo é o cérebro de IA específico que o agente usará para pensar. Diferentes modelos têm diferentes pontos fortes e diferentes preços. Alguns são muito inteligentes, mas caros. Outros são baratos, mas não são ótimos para o tipo de trabalho estruturado que um agente faz.

### Escolha Seu Modelo de IA

**13:51** · Para uma configuração inicial, recomendo o DeepSeek-V4. É esse aqui. É barato, cerca de 43 centavos por milhão de palavras de entrada e 87 centavos por milhão de palavras de saída. E é confiável para o tipo de trabalho em múltiplas etapas que o Hermes faz. Você não terá uma surpresa com uma conta grande no primeiro dia. Agora, uma dica rápida. Nem todo modelo no OpenRouter funciona bem como agente.

**14:17** · Dois a evitar por enquanto são o GPT-5.4 mini, que tem dificuldade com as chamadas de ferramentas que o Hermes precisa, e as versões de raciocínio do Qwen3.x com as tags de pensamento ativadas. Esses tendem a se convencer a não usar ferramentas. Você pode alterar o modelo mais tarde com um único comando, vou mostrar como fazer isso, então não se preocupe muito com isso agora. Estamos escolhendo o DeepSeek porque é barato e razoavelmente poderoso.

**14:44** · Para selecioná-lo na lista, use as teclas de seta até que esteja selecionado e pressione Enter no teclado. Em seguida, ele perguntará onde você deseja ter seu backend de terminal. Vamos manter o atual, Local, então vá em frente e pressione Enter no teclado. E agora ele perguntará se você deseja conectar uma plataforma de mensagens, então vá em frente e pressione Enter no teclado para configurar as mensagens agora.

**15:09** · Você pode conectar o Hermes ao Telegram, Discord, Slack, WhatsApp e alguns outros. Vamos usar o Telegram porque é gratuito, rápido de configurar e funciona em todos os telefones e computadores. Para conectar o Hermes ao Telegram, precisamos criar algo chamado bot do Telegram. Um bot é uma conta do Telegram controlada por um software em vez de uma pessoa. O Hermes usará o bot para enviar e receber suas mensagens.

**15:32** · Tudo bem, então primeiro neste assistente, digite 1 no terminal para selecionar o Telegram e pressione Enter. Ele pedirá que você pressione Enter para confirmar novamente, então vá em frente e pressione Enter, e agora ele pede o token do bot do Telegram. Tudo bem, deixe o terminal onde está por enquanto e alterne para o Telegram. Você pode usar o Telegram no seu telefone ou computador.

**15:53** · Se você ainda não tem o Telegram, tenho um link na descrição abaixo onde você pode baixá-lo. Então baixe no seu dispositivo preferido. No meu caso, vou executá-lo no computador aqui. E então cadastre-se ou faça login na sua conta. Assim que o Telegram estiver aberto, vá até a barra de pesquisa e procure o BotFather, ou você pode clicar no link na descrição abaixo para abrir um chat diretamente com o BotFather.

**16:20** · É o que tem o selo de verificação azul. Vá em frente e clique nele e depois clique em Iniciar. Você pode digitar o comando /newbot ou clicar na mensagem.

**16:34** · Você receberá uma resposta do BotFather perguntando como vamos chamar o bot?

**16:37** · Então vou chamar o meu de MattHermesBot. Agora precisamos escolher um nome de usuário para o seu bot e o nome do bot deve ser único no ecossistema do Telegram, então tente escolher algo que não seja apenas genérico. Caso contrário, talvez você precise tentar algumas vezes até encontrar um nome de usuário único. Vou chamar o meu de MattHermesWonderBot. E recebemos uma confirmação dizendo que o bot foi criado. Essa mensagem contém esta longa sequência aqui.

**17:02** · Este é o seu token para acessar a API HTTP. É isso que o Hermes está pedindo, então vá em frente e copie. E uma coisa importante aqui: se você usou outro agente como o OpenClaw antes com um bot do Telegram, não use o mesmo token de bot. Crie um novo bot para o Hermes. Se você reutilizar o antigo, ambos os agentes brigarão pelo mesmo bot e nenhum funcionará corretamente.

**17:24** · Tudo bem, agora vá em frente e volte para a guia do terminal. Clique e cole. Novamente, você não verá sendo colado, apenas vá em frente e pressione Enter no teclado e o assistente confirmará o token e continuará.

**17:39** · Em seguida, o assistente pergunta: quais contas do Telegram têm permissão para falar com o seu agente?

**17:44** · Isso é importante.

**17:45** · Sem esta etapa, qualquer pessoa na internet que encontrar o nome de usuário do seu bot poderia enviar mensagens e usar seus créditos de IA. Precisamos dizer ao Hermes que apenas sua conta do Telegram é permitida. Para fazer isso, precisamos do seu ID pessoal do Telegram. O Telegram tem um bot que fornece o seu em cerca de 10 segundos. Volte ao Telegram e procure o UserInfoBot. É este aqui com o perfil verde e o ID no rosto.

**18:16** · Em seguida, toque em Iniciar.

**18:18** · O bot responde com seus dados. Vá em frente e copie seu ID, volte para o terminal, cole seu ID e pressione Enter. Em seguida, o assistente pergunta se você deseja que este ID seja definido como seu canal home. É para onde o Hermes enviará os resultados de trabalhos agendados e quaisquer mensagens que ele envie por conta própria. Pressione Y no teclado para sim e depois pressione Enter. E a configuração está completa.

**18:45** · O assistente agora mostra um resumo de tudo que foi configurado. A disponibilidade das suas ferramentas, onde suas configurações estão armazenadas e uma lista de comandos úteis. Em seguida, vamos iniciar a interface de chat do Hermes. Para fazer isso, digite hermes e pressione Enter. Tudo bem, e a interface de chat abre dentro do seu terminal. Você verá seu modelo, suas ferramentas e suas habilidades instaladas listadas no topo. Agora iniciamos o que é chamado de gateway.

### Inicie o Gateway e Envie Sua Primeira Mensagem

**19:15** · O gateway é a parte do Hermes que escuta mensagens do Telegram e as passa para o agente. Uma vez em execução, você pode fechar o terminal e falar com seu agente diretamente do seu telefone. No terminal, na parte inferior onde você tem o cursor, digite hermes gateway instal e pressione Enter. Isso conecta o Telegram ao gateway. Pode levar alguns momentos, então aguarde até que seja concluído.

**19:41** · Em seguida, digite hermes gateway run e pressione Enter. Novamente, isso pode levar alguns minutos. Agora encontramos um erro de permissão porque estamos executando como usuário root e o gateway quer ser executado como usuário Hermes por segurança. Observe que o próprio agente diagnosticou o problema e me deu três maneiras de corrigi-lo. A mais simples é a primeira: executar o gateway como usuário Hermes, então é isso que farei.

**20:04** · E você pode simplesmente copiar o comando aqui da saída, selecioná-lo, pressionar Ctrl+C e depois colar no seu terminal. Ou se por algum motivo não mostrar a versão que você pode copiar e colar, aqui está o comando: sudo -u hermes /opt/hermes/.venv/bin/hermes gateway run. Sei que é muito, mas é por isso que é mais fácil apenas copiar e colar, e pressionar Enter para executar. Novamente, isso levará um momento para processar.

**20:44** · E agora temos uma confirmação dizendo que o gateway está funcionando. O gateway está ativo. Ok, vamos enviar ao agente sua primeira mensagem do Telegram. Abra o Telegram e procure o nome de usuário que você deu ao seu bot, ou volte à sua conversa com o BotFather e clique no Telegram vinculado diretamente ao seu bot. Em seguida, clique em Iniciar e você pode receber esta mensagem dizendo "Comando desconhecido."

**21:10** · Isso é normal.

**21:11** · O Hermes não usa um comando /start integrado, então ele está apenas informando. Agora vamos enviar uma primeira mensagem de verdade. Vamos digitar: "Você está rodando em um VPS da Hostinger dentro do Docker. Diga-me quais ferramentas e habilidades você tem disponíveis atualmente."

**21:26** · E envie.

**21:28** · Estamos fazendo isso para dar ao agente seu contexto inicial para que ele saiba exatamente onde está rodando. E você pode ver aqui que ele está digitando. Isso realmente significa que ele está pensando e está apenas informando. Ele responderá em um minuto. E recebemos uma resposta, é bem longa. É uma lista de todas as diferentes habilidades e tudo que nosso agente tem acesso.

**21:51** · Agora, se você recebeu uma resposta, seu agente está funcionando, a parte difícil está feita. Se não recebeu uma resposta, não se preocupe. As três coisas que mais frequentemente dão errado são uma chave de API que não foi colada corretamente, um ID de usuário ausente na lista de permissões ou o gateway não iniciando corretamente. A maneira mais rápida de descobrir é voltar ao terminal e digitar hermes doctor e enviar.

**22:16** · Ele verificará sua configuração e apontará o que está errado. E se isso não resolver, execute hermes setup novamente e percorra o assistente. Tudo bem, a partir daqui vamos fazer o agente trabalhar de verdade para você. As duas coisas que tornam o Hermes mais do que um chatbot comum são as habilidades e a memória. Uma habilidade é um fluxo de trabalho salvo que o agente pode executar por conta própria.

### Habilidades e Memória — Torne o Hermes Útil

**22:38** · Algumas vêm incorporadas, outras são criadas quando você pede ao agente para fazer algo complexo. O agente salva as etapas para poder executar o mesmo fluxo de trabalho novamente sem precisar pensar do zero. A memória é como o agente acompanha as coisas sobre você em conversas separadas. Quero mostrar algo que torna a configuração do seu próprio agente digna do esforço.

**22:58** · O agente fará pesquisas reais para você na web aberta, salvará o que encontrou em um arquivo no seu servidor e automatizará o mesmo trabalho para ser executado em um cronograma. Agora, eu faço vídeos no YouTube, então para mim, quero que meu bot pesquise os cinco principais vídeos do YouTube classificados agora para algo como marketing por e-mail e depois me apresente um relatório. Mas você pode ter seu bot pesquisando o que quiser.

**23:25** · Então pense sobre isso agora e depois vou mostrar um prompt que você pode executar e modificar para funcionar melhor na sua situação. Aqui eu digitei: "Encontre os cinco principais vídeos do YouTube classificados agora para 'tutorial de email marketing para iniciantes'. Para cada um, salve o título, canal e o que aborda em um arquivo. Depois me diga quais lacunas você notou." Vamos em frente e clicar em Enviar e ele decide usar a habilidade youtube-content.

**23:52** · Ele percebe que ainda não tem o Chrome instalado, então vai configurá-lo por si mesmo. E você verá a saída de pensamento enquanto está trabalhando. O agente passará um ou dois minutos fazendo a pesquisa. Deixe-o trabalhar e, quando terminar, responderá com um resumo no chat e confirmará onde o arquivo está salvo.

**24:08** · Agora, se por algum motivo seu agente não tiver acesso às ferramentas necessárias para executar a tarefa que você pediu, ele dirá isso e apresentará opções sobre o que você pode fazer juntos para que ele realmente consiga fazer o trabalho pedido. Para mim, após alguns minutos ele volta e diz onde salvou o arquivo aqui, /opt/data/email-marketing-top5-youtube.md — md é apenas um arquivo markdown, é apenas um arquivo de texto.

**24:37** · Então aqui está o resumo, voltou com cinco vídeos diferentes do YouTube, um de Alex Hormozi, HubSpot Marketing, oh e acho que meu vídeo aqui no canal Metics Media é o número três, o que é bem legal. Tem o número quatro e o número cinco, Jade Beason e LYFE Marketing. Identificou algumas grandes lacunas de coisas que precisam ser abordadas em vídeos futuros se alguém fosse fazer um vídeo, e destaca todas as coisas diferentes.

**25:05** · Por que isso importa, resumo, e perguntou se queremos etapas de acompanhamento adicionais. Então vamos pausar no que o agente acabou de fazer. Ele foi à web aberta, abriu cinco páginas diferentes, extraiu as mesmas informações estruturadas de cada uma, fez um julgamento sobre quais tópicos todos estão cobrindo e o que está faltando, e salvou tudo em um arquivo no servidor. O arquivo agora está no seu próprio servidor.

**25:30** · Não na sandbox de nuvem de outra pessoa, não atrás de um conector para um serviço de terceiros. Na máquina que você controla. Ainda estará lá na próxima vez que você falar com o Hermes, mesmo em uma conversa completamente diferente. E em um minuto vamos configurar o agente para fazer esta mesma pesquisa por conta própria em um cronograma, para que o arquivo se acumule semana a semana sem você fazer nada.

**25:52** · Agora vamos salvar todo esse fluxo de trabalho como uma habilidade para que o agente possa executar a mesma pesquisa sobre qualquer tópico sem que você precise digitar o prompt longo novamente. Então agora diremos: "Salve esse fluxo de trabalho como uma habilidade chamada competitor-watch. De agora em diante, quando eu lhe der um termo de pesquisa, encontre os cinco principais vídeos do YouTube, salve as mesmas informações no arquivo e aponte as lacunas." Vamos em frente e enviar isso.

**26:18** · Tudo bem, o agente confirma que salvou a habilidade e nos diz o que ela faz. Ele lista, o gatilho diz: "Você me dá qualquer termo de pesquisa, por exemplo, 'dicas de SEO para SaaS,' e eu seguirei estas etapas aqui." Há quatro etapas e inclui um script reutilizável, um script Python.

**26:35** · Isso é muito legal.

**26:36** · Agora, uma coisa importante sobre habilidades. Quando o agente escreve uma habilidade a partir do seu próprio trabalho como acabamos de fazer, ela é segura por padrão. Mas se você alguma vez instalar uma habilidade que outra pessoa escreveu, o Hermes a verificará em busca de código inseguro primeiro, e você ainda deve instalar apenas habilidades de fontes em que confia. Tudo bem, última parte, memória. O agente pode salvar coisas sobre você e trazê-las para cada tarefa futura.

**27:02** · Vamos dar a ele uma preferência real que moldará como esse fluxo de trabalho de pesquisa realmente funciona para você. Você pode dizer ao seu bot o que quiser sobre você. Mas para mim, é isso que direi: "Lembre-se de que faço vídeos tutoriais do YouTube sobre software, principalmente para iniciantes completos. Quando você analisar lacunas na pesquisa de concorrentes, enquadre-as em termos do que ajudaria especificamente um iniciante completo."

**27:28** · Vamos em frente e enviar isso, e ele confirma que salvou essa preferência. Agora, vamos verificar sua memória.

**27:35** · Vamos enviar: "O que você se lembra sobre mim?"

**27:39** · E o agente responderá com o que armazenou, incluindo a descrição do nicho. Diz que sou Matt, faço vídeos no YouTube. Precisa enquadrar a análise de lacunas de concorrentes em torno das necessidades específicas de iniciantes, e continua incluindo detalhes sobre o fato de que este é um Hermes Agent rodando em um VPS da Hostinger, estamos usando o Telegram, etc. Portanto, agora essa preferência está salva para cada conversa futura.

**28:06** · Na próxima vez que o agente fizer essa pesquisa, já saberá o contexto adicional que você forneceu. No meu caso, ele saberá para quem faço vídeos, e a análise de lacunas será enquadrada em torno do que os iniciantes precisam. Quanto mais tempo você tiver o Hermes, mais ele acumula, mais contexto, mais conhecimento e menos você precisa se repetir.

### Agendar um Trabalho Recorrente

**28:26** · Um dos melhores recursos do Hermes é que ele pode trabalhar para você em um cronograma, não apenas quando você pede. Esses são chamados de trabalhos agendados, ou cron jobs. O agente executa o trabalho na hora que você escolher, mesmo que você esteja dormindo, mesmo que seu laptop esteja desligado, e envia o resultado pelo Telegram. Você não precisa escrever nenhum código ou sintaxe de agendamento.

**28:45** · Você apenas diz ao agente em linguagem simples o que quer e quando quer. Vamos automatizar o fluxo de pesquisa que acabamos de configurar. No Telegram, podemos dizer algo como: "Toda segunda-feira às 9h, execute minha habilidade competitor-watch em três termos de pesquisa. 'Tutorial de email marketing para iniciantes', 'tutorial de WordPress para iniciantes' e 'tutorial de SEO para iniciantes'. Envie-me um resumo no Telegram com as lacunas que se destacaram."

**29:10** · Claro, modifique a tarefa de pesquisa ou a tarefa agendada para ser o que você quiser em um cronograma. Este é apenas meu caso de uso particular. O agente confirma o cronograma e informa quando o trabalho será executado a seguir. Ele pode pedir para confirmar seu fuso horário. Você pode responder com o seu. Por exemplo, posso dizer: "Vamos usar o Horário Central dos EUA."

**29:34** · E vemos que foi atualizado para ser executado toda segunda-feira às 9h no horário central. O fuso horário foi salvo, então outros trabalhos futuros usarão esse padrão. Para ver todos os seus trabalhos agendados, você pode simplesmente perguntar. Você pode dizer algo como: "Mostre-me meus trabalhos agendados." E o agente os listará com o horário de execução. Por enquanto, é apenas este "Monitor de Concorrentes de Segunda de Manhã."

**29:53** · Agora, se você quiser ver uma amostra de como é a saída completa, você também pode pedir ao bot para executar um trabalho a qualquer momento. Então poderíamos dizer algo como: "Execute esse trabalho completo agora." E ele inicia o cron job. Esta é uma ótima maneira de revisar a saída do trabalho para garantir que você está obtendo tudo no formato certo e da forma que deseja que seja apresentado.

**30:15** · Se não voltar da maneira que você quer, você pode simplesmente dizer ao bot e ele fará os ajustes para a próxima vez. Vamos pausar um momento para reconhecer o que acabamos de configurar. Toda segunda-feira às 9h, este agente vai pesquisar três tópicos por conta própria, salvar os resultados em um arquivo no servidor e enviar um resumo ao Telegram, tudo no modelo de IA escolhido anteriormente, DeepSeek.

**30:36** · E esse arquivo vai crescer semana a semana, então você vai começar a ter uma imagem de pesquisa realmente robusta. Você também pode acumular quantos desses trabalhos quiser. Você poderia receber um resumo matinal, um relatório semanal, uma verificação de preços em algo que você está monitorando. Qualquer coisa que você possa descrever em uma frase, o agente pode agendar. Tudo bem, há dois lugares para acompanhar quanto tudo isso custa.

### Onde Rastrear Seus Custos

**30:58** · Primeiro, sua página de atividades do OpenRouter para uso de IA e seu painel da Hostinger para o próprio servidor. De volta ao OpenRouter na página de Chaves de API, você pode ver o uso até o momento para essa chave específica. Você também pode clicar em Atividade no lado esquerdo em Conta e ver seus gastos atuais, número de solicitações e total de tokens usados, e por padrão divide por hora do dia.

**31:27** · Você também pode alterá-lo para diferentes períodos de tempo, para que você possa ter uma boa noção de quais tipos de atividades e solicitações estão custando muito dinheiro. Seu modelo de IA é o maior fator individual na sua conta. O DeepSeek-V4, o que escolhemos, é uma das opções confiáveis mais baratas. Se você precisar de mais capacidade de raciocínio para uma tarefa difícil, no Telegram, envie /model como um comando para mudar para um modelo diferente.

**31:57** · A partir daí, você pode clicar em OpenRouter e obter uma lista de todos os modelos disponíveis para você. Se precisar de mais capacidade, você pode subir para algo como o Claude Opus 4.7. Tenha em mente que mais poder vem com mais custo. Ou se quiser mudar para algo mais barato, você também pode fazer isso. Para mim, vou voltar ao DeepSeek já que é um ótimo LLM para uso diário.

**32:22** · Você também pode dizer ao agente para usar um modelo específico para um trabalho agendado específico, para que seu trabalho de rotina permaneça barato enquanto tarefas mais pesadas obtêm o modelo mais inteligente. Agora, de volta ao painel da Hostinger, você pode acompanhar seus custos clicando no seu perfil no canto superior direito e depois em Faturamento para ver suas informações anteriores, bem como assinaturas futuras e o preço de renovação. Esse é o que você pagará quando o período introdutório terminar.

**32:49** · Recomendo verificar a página de Atividade do OpenRouter a cada poucos dias enquanto você está começando, dessa forma você pode ver o uso real e ajustar os modelos que usa antes que qualquer coisa te surpreenda. Agora, o fluxo de trabalho de pesquisa que construímos é apenas um exemplo. O Hermes pode fazer muito mais. A maneira mais fácil de descobrir o que é útil para você é perguntar diretamente ao agente.

### Outras Coisas que Seu Agente Pode Fazer

**33:11** · Envie algo como: "Para que tipo de tarefas você é bom?"

**33:15** · E então deixe-o sugerir ideias. Aqui ele volta com uma lista do que é bom. Execução prática, trabalho de fundo de longa duração, tarefas recorrentes agendadas, geração e edição de código, pesquisa e síntese, e memória entre sessões. Ele também lista algumas coisas em que é razoável e coisas para as quais não foi construído. Tudo bem, seu agente está funcionando e aprendendo com a forma como você o usa.

**33:36** · O primeiro link na descrição oferece 10% extra de desconto no seu VPS se você ainda não o pegou, além de qualquer promoção que a Hostinger já esteja executando.

**33:45** · Obrigado por assistir.