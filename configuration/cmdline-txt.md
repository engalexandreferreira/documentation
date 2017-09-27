# A Linha de Comando do Kernel

O kernel do Linux aceita uma linha de comando de parâmetros durante a inicialização. No Raspberry Pi, esta linha de comando é definida em um ficheiro na partição de inicialização (boot partition), chamado cmdline.txt. Este é um ficheiro de texto simples que pode ser editado usando qualquer editor de texto, por exemplo o Nano.

```
sudo nano /boot/cmdline.txt
```

Observe que devemos usar `sudo` para editar qualquer coisa na partição de inicialização.

## Opções na Linha de Comando

Existem muitos parâmetros da linha de comando do kernel, alguns dos quais são definidos pelo kernel. Outros são definidos por código que o kernel pode usar, tais como o "Plymouth splash screen system".

#### Entradas Padrão

 - console: define o console serial. Geralmente, há duas entradas:
     - `console=serial0,115200`
     - `console=tty1`
 - root: define a localização do sistema de ficheiros de raiz, por exemplo `root=/dev/mmcblk0p2` significa bloco de cartão multimídia 0 partição 2.
 - rootfstype: define o tipo de sistema de ficheiros que o rootfs usa, por exemplo `rootfstype=ext4`
 - elevator: especifica a agenda de Entrada/Saida para usar. `elevator=deadline` significa que o kernel impõe um prazo para todas as operações de Entrada/Saida para evitar "request starvation".
 - quiet: define o nível de log do kernel padrão para `KERN_WARNING`, o que suprime todas as mensagens de registro, exceto muito graves, durante a inicialização.

#### Outras entradas (não exaustivas)

 - splash: informa a inicialização para usar uma tela inicial através do módulo Plymouth.
 - plymouth.ignore_serial_console
 - dwc_otg.lpm_enable: desliga o LPM na driver dwc_otg(On the Go).
 - dwc_otg.speed: define a velocidade correcta para o USB. `dwc_otg.speed=1` será definda como a velocidade para USBv1.0.
 - smsc95xx.turbo_mode: Ativa / desativa o modo de turbo do driver de rede com fio. `smsc95xx.turbo_mode=N` desliga o modo turbo.
 - usbhid.mousepoll: especifica o intervalo de pesquisa do rato. Se tu tiveres problemas com um rato sem fio lento ou errático, configurar isso para 0 pode ajudar: `usbhid.mousepoll=0`.
 
