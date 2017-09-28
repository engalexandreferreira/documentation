# Configuração da câmera

## Configurando o hardware da câmera

**Aviso**: as câmeras são sensíveis à estática. Descarga a tua electricidade estática antes de manusear o PCB. Uma torneira de pia ou similar deve ser suficiente se tu não tiveres uma pulsei de aterramento.

The camera board attaches to the Raspberry Pi via a 15-way ribbon cable. There are only two connections to make: the ribbon cable needs to be attached to the camera PCB, and to the Raspberry Pi itself. You need to get the cable the right way round, or the camera will not work. On the camera PCB, the blue backing on the cable should face away from the PCB, and on the Raspberry Pi it should face towards the Ethernet connection (or where the Ethernet connector would be if you're using a model A).

A placa da câmera anexa ao Raspberry Pi via um cabo de fita de 15 vias. Existem apenas duas conexões para fazer: o cabo de fita precisa ser conectado à PCB da câmera e ao próprio Raspberry. Você precisa obter o cabo no caminho certo, ou a câmera não funcionará. Na PCB da câmera, o suporte azul do cabo deve se afastar da PCB e, no Raspberry Pi, deve enfrentar a conexão Ethernet (ou onde o conector Ethernet seria se você estiver usando o modelo A).

Although the connectors on the PCB and the Pi are different, they work in a similar way. On the Raspberry Pi itself, pull up the tabs on each end of the connector. It should slide up easily, and be able to pivot around slightly. Fully insert the ribbon cable into the slot, ensuring it is set straight, then gently press down the tabs to clip it into place. The camera PCB connector also requires you to pull the tabs away from the board, gently insert the cable, then push the tabs back. The PCB connector can be a little more awkward than the one on the Pi itself.

Embora os conectores da PCB e do Pi sejam diferentes, eles funcionam da mesma forma. No próprio Raspberry Pi, puxe as abas em cada extremidade do conector. Deve deslizar facilmente, e poder girar ligeiramente. Insira inteiramente o cabo de fita na ranhura, garantindo que ele seja ajustado em linha reta, depois aperte suavemente as abas para encaixá-lo no lugar. O conector da PCB da câmera também exige que você puxe as guias para longe da placa, insira o cabo com cuidado e, em seguida, empurre as abas para trás. O conector do PCB pode ser um pouco mais estranho do que aquele no próprio Pi.

## Configurando o software da câmera

Execute as seguintes instruções na linha de comando para baixar e instalar o kernel, o firmware GPU e as aplicações mais recentes. Tu precisarás de uma conexão com a Internet para que funcione corretamente.

```bash
sudo apt-get update
sudo apt-get upgrade
```

Agora tu precisas ativar o suporte da câmera usando o programa `raspi-config` que tu usarás quando tu configurares o teu Raspberry Pi pela primeira vez.

```bash
sudo raspi-config
```

Use as teclas de cursor para mover para a opção da câmera e seleciona 'enable'. Ao sair do `raspi-config`, pedirá para reiniciar. A opção de "enable" assegurará que, ao reiniciar, o firmware da GPU correto será executado com o driver da câmera e a sintonia e a divisão da memória GPU é suficiente para permitir que a câmera adquira memória suficiente para executar corretamente.

Para testar que o sistema está instalado e funcionando, experimenta o seguinte comando:

```bash
raspistill -v -o test.jpg
```

O ecrã deve mostrar uma pré-visualização de cinco segundos da câmera e depois tirar uma foto, guardar o ficheiro `test.jpg`, enquanto exibe várias mensagens informativas.

## Mais informação

Vê [Camera Software](../raspbian/applications/camera.md).
