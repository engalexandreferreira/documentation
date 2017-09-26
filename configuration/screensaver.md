# Configurar o protector de ecrã / desligar ecrã

## Na consola

Se tu estiver usando o Raspberry Pi exclusivamente na console (sem GUI de área de trabalho), tu precisas configurar o bloqueio da console. A configuração atual, em segundos, pode ser exibida usando

```
cat /sys/module/kernel/parameters/consoleblank
```

Aqui, `consoleblank` é um parâmetro de kernel. Para ser definido permanentemente, ele precisa ser definido na linha de comando do kernel.

```
sudo nano /boot/cmdline.txt
```

Adiciona `consoleblank=0` para desligar a tela completamente ou editá-la para definir o número de segundos de inatividade antes que o console fique desligada. Observa que a linha de comando do kernel deve ser uma única linha de texto.

## No ambiente de trabalho (PIXEL)

Por padrão, o PIXEL não possui nenhum software de proteção de tela fácil de usar instalado, embora o protetor de tela esteja habilitado. Em primeiro lugar, tu deves instalar a aplicação "X Windows screensaver".

```
sudo apt-get install xscreensaver
```

Isso pode levar alguns minutos.

Uma vez que isso foi instalado, tu podes encontrar a aplicação do protector de ecrã sob a opção Preferências no menu principal da área de trabalho. Isso oferece muitas opções para configurar o protector de ecrã ou desativá-lo completamente.
