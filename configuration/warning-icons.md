# Icons de aviso do Firmware

Sob certas circunstâncias, o firmware do Raspberry Pi exibirá um ícone de aviso no visor, indicando um problema.

Actualmente, existem três ícones que podem ser exibidos.

## Aviso de sob tensão

Se o fornecimento de energia ao Raspberry Pi cair abaixo de 4.63V (+/- 5%), o seguinte ícone é exibido.

![Under Voltage](images/under_volt.png)

## Aviso de temperatura elevada (80-85C)

Se a temperatura do SoC for entre 80C e 85C, o seguinte ícone é exibido. O poder de processamento do processador ARM será reduzidos na tentativa de reduzir a temperatura do núcleo.

![Over Temperature (80-85C)](images/over_temperature_80_85.png)

## Aviso de temperatura muito elevada (mais de 85C)

Se a temperatura do SoC for superior a 85C, o seguinte ícone é exibido. O poder de processamento do processador ARM e o GPU serão reduzidos na tentativa de reduzir a temperatura do núcleo.

![Over Temperature (85C+)](images/over_temperature_85.png)
