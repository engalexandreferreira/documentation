# Contribuindo para a Documentação do Raspberry Pi

As fontes para toda a documentação do Raspberry Pi são armazenadas online em um site chamado GitHub, localizado aqui:

https://github.com/raspberrypi/documentation

Embora tu não possas alterar a documentação diretamente no repositório oficial, podes dar uma olhada em todos os ficheiros de origem e ver como tudo está organizado. As fontes de ficheiros e pastas seguem a documentação hierárquica encontrada no site da Raspberry Pi.

Antes de fazer qualquer alteração, é aconselhável descobrir se sua contribuição provavelmente será aceita pela verificação [aqui](https://www.raspberrypi.org/documentation/CONTRIBUTING.md).

Para enviar documentação nova ou corrigida, tu tens crie uma conta do GitHub (caso ainda não tenhas uma) e fazer **fork** no repositório original para a tua conta. Tu fazes as mudanças conforme te parecer correcto, salva-as no teu repositório e em seguida, fazes um **pull request** para o repositório original do Raspberry Pi. Este pull request (**PR**) aparece no repositório de Raspberry Pi, onde pode ser avaliado pelos responsáveis pela manutenção, cópiado editado e, se apropriado, fundida com o repositório oficial.

A documentação que aparece no site Raspberry Pi é gerada a partir do repositório GitHub e é atualizada aproximadamente a cada hora.

Tu precisarás de uma conta GitHub para executar qualquer uma das seguintes operações.

## Forking a um repositório

Isso é facil. Vá para o repositório Raspberry Pi, https://github.com/raspberrypi/documentation, e vê o canto superior direito da página. Deve haver um botão denominado **Fork**, que irá abrir uma cópia do repositório na tua própria conta do GitHub.

## Faz mudanças

Na tua própria cópia do repositório, agora tu podes alterar ou adicionar ficheiros. O formato dos ficheiros é o GitHub Markdown e, por esse motivo, novos arquivos devem ter o sufixo `.md`. Há uma descrição do GitHub Markdown [aqui](https://guides.github.com/features/mastering-markdown/).


Para editar um ficheiro, primeiro encontre o ficheiro e cliqua nele. Isso mostra a página totalmente renderizada e, na barra de ferramentas na parte superior do ficheiro (não na parte superior da página), está um ícone pequeno de um lápis. Este é o botão de edição. Cliqua nele e o ficheiro aparecerá no editor Github. Agora tu podes editar para o conteúdo que desejares. Tu podes clicar em **Preview changes** para ver o arquivo totalmente renderizado com as tuas edições.

At the end of the page is a box called **Commit Changes**. You can either commit your changes directly to your own master branch or create a new branch for use as a pull request. Use the master option, as this means you are making changes to your master copy. Using the branch option will create a new branch in your own repository, but that's a little more complicated to deal with so it won't be described here. If you are making a lot of independent changes over time before pushing the changes to Raspberry Pi, you may wish to investigate the branch option. Update the commit title and enter a description of the change at this point. 

No final da página é uma caixa chamada **Commit Changes**. Tu podes comprometer a tuas alterações diretamente em sua própria ramificação mestre ou criar uma nova ramificação para uso como uma solicitação de puxar. Use a opção mestre, pois isso significa que tu está a fazer alterações na tua cópia mestra. A utilização da opção de branch criará um novo ramo no teu próprio repositório, mas isso é um pouco mais complicado de lidar, portanto não será descrito aqui. Se tu estás a fazer muitas mudanças independentes ao longo do tempo antes de pressionar as mudanças para Raspberry Pi, tu podes querer investigar a opção de branch. Atualiza o título de confirmação e insere uma descrição da mudança neste momento.


Selecionando **Commit changes** farão a mudança para a tua ramificação mestre. Agora tu precisa tomar essa mudança e fazer uma pull request dela.

## Abrir um Pull Request

Isso é bastante fácil. Cliqua em **<> Code** na barra de ferramentas. Isso leva-te de volta à página de ficheiros. Deve haver um botão acima da árvore de ficheiros com a etiqueta **New pull request**. Cliqua nisso. Uma página agora aparece que descreve onde o Pull Resquest deve ir. Esta página de Pull Request está realmente na página Raspberry Pi GitHub, e não no colaborador, uma solicitação de Pull Request solicita aos voluntários do repositório Raspberry Pi que "retirem" o repositório do colaborador. O lado esquerdo deve ser o repositório `raspberrypi/documentation`, e o ramo deve ser o mestre. O lado direito é de onde vem o Pull Request: a tua conta GitHub e seu ramo principal. Mais adiante, tu deves ver uma lista dos commits que tu desejas ter no Pull Request e, abaixo disso, as mudanças reais.

Se tu estiveres feliz pelo Pull Request ser criado, clique em **Create pull request**.

E é isso! A lista de Pull Request da documentação Raspberry Pi agora terá a tua entrada nele. Ele será lido, avaliado quanto à correção técnica, aprovado para copiar editores para verificação final e, finalmente, combinado com a árvore de documentação principal.


Este é um guia muito rápido para contribuir com o GitHub, mas irá ajudar a fazer a diferença!

