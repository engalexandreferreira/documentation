# Configuração Audio

O Raspberry Pi possui dois modos de saída de áudio: HDMI e tomada de fone de ouvido. Tu podes alternar entre esses modos a qualquer momento.

Se o seu monitor HDMI ou TV tiver alto-falantes embutidos, o áudio pode ser reproduzido através do cabo HDMI, mas tu podes alternar para um conjunto de fones de ouvido ou outros alto-falantes conectados à tomada de fone de ouvido. Se o teu monitor afirma ter alto-falantes, o som é emitido via HDMI por padrão, caso contrário, é emitido através da tomada de fone de ouvido. Esta pode não ser a configuração de saída desejada ou a auto-detecção é imprecisa, caso em que tu podes alternar manualmente a saída.

## Alterar a saída de áudio

Existem duas maneiras de configurar a saída de áudio.

### Linha de comandos

O comando a seguir, inserido na linha de comando, alternará a saída de áudio para HDMI:

```
amixer cset numid=3 2
```

Aqui, a saída está sendo configurada para `2`, que é HDMI. Configurando a saída para `1` muda para analógico (tomada de fone de ouvido). A configuração padrão é `0`, que é automática.

### raspi-config

Abra [raspi-config](raspi-config.md) digitando o seguinte na linha de comando:

```
sudo raspi-config
```

Isso abrirá a tela de configuração:

![raspi-config screen](images/raspi-config.png)

Select Option 8 `Advanced Options` and press `Enter`, then select Option A6: `Audio` and press `Enter`:

Selecione a opção 8 `Advanced Options` e pressione `Enter`, depois selecione opção A6: `Audio` e pressione `Enter`:

![Audio configuration screen](images/raspi-config-audio.png)

Agora você é apresentado com os dois modos explicados acima como uma alternativa à opção por padrão `Auto`. Selecione um modo, pressiona `Enter` e pressione a tecla de seta para a direita para sair da lista de opções e selecione `Finish` para sair da ferramenta de configuração.

## Se tu ainda não estás recebendo som via HDMI

Em alguns casos raros, é necessário editar o ficheiro `config.txt` para forçar o modo HDMI (em oposição ao modo DVI, que não envia som). Tu podes fazer isso editando `/boot/config.txt` e configurando `hdmi_drive=2` e reiniciando para que a alteração entre em vigor.
