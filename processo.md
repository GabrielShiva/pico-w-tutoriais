# COMO CRIAR COMUNICAÇÃO ENTRE O PUTTY E O RASPBERRY PI PICO W

Com o VsCode aberto, crie um projeto em C do zero utilizando a extensão Raspberry Pi Pico Project, como indica a imagem abaixo.

![Criando novo projeto para o raspberry pi pico w](/images/criar_projeto.png)

Após isso, dê um nome para o projeto, selecione a placa do pico w. 

![Configuração do projeto 01](/images/configuracoes_projeto_01.png)

Por fim, na Seção Stdio Support, selecione as duas caixas e aperte no botão **criar**.

![Configuração do projeto 01](/images/configuracoes_projeto_02.png)

Abra o projeto e selecione o arquivo com a extensão **.c**. Nesse arquivo, digite o código abaixo.

![Escrevendo código](/images/escrevendo_codigo.png)

```
#include <stdio.h>
#include "pico/stdlib.h"

int main() {
    stdio_init_all();

    char buffer[1024];

    while (true) {
        scanf("%1024s", buffer);
        printf("ESCRITO: %s!\n", buffer);
        sleep_ms(500);
    }

    return 0;
}

```

Após escrever o código acima, faça o seguinte:

1) Coloque a placa do raspberry pi no modo bootsel, segurando o botão branco e apertando, ao mesmo tempo, o botão de reset da placa. Matenha o USB da placa desconectada do computador.

2) Digite na barra de pesquisa do Windows: gerenciador de dispositivos.
    - Clique na opção Portas (COM e LPT)

![Portas sem o PICO](/images/portas_sem_pico.png)

3) Conecte o pico W no computador por meio do USB. 

4) Compile o projeto.

![Compilando o projeto](/images/compilando.png)

5) Arraste o arquivo **.uf2** que está na pasta **build** para a placa com o nome RPI-RP2.

![Compilando o projeto](/images/carregando_arquivo_para_pico.png)

6) No gerenciador de dispositivos, veja qual porta o pico está conectado. No meu caso foi a porta COM8.

![Compilando o projeto](/images/observando_porta.png)

7) Instale o putty no seguinte link: **[clique aqui](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)**.

8) Selecione uma versão (.exe) do putty se o seu PC é 32bits ou 64bits.

![Compilando o projeto](/images/baixando_putty.png)

9) Abra o programa putty, clique em Serial e digite o seguinte:
    - Em Serial line, digite a porta que a sua placa está conectada (COM8, no meu caso);
    - Em Speed, digite **115200**.

![Compilando o projeto](/images/configurando_putty.png)

8) Após digitar as informações necessárias, clique no botão **Open**.

9) Com o terminal aberto, digite algum texto (como *PEIXE*) e aperte a tecla **Enter**. O seu texto deve aparecer. na tela.

![Compilando o projeto](/images/testando_terminal_serial.png)

> **NOTA**: perceba que, enquanto você estiver digitando o texto, o retorno do que você estiver digitando não aparecerá na tela, apenas quando você clicar na tecla Enter.

Após isso, sempre repita o mesmo processo:
- Modifique o seu código;
- Compile o código;
- Coloque a placa em modo Bootsel;
- Carregue o arquivo .uf2 para a placa;
- Abra o putty, coloque em serial e especifique as infos (PORTA e VELOCIDADE);
- Clique no botão abrir e teste o seu código.

No meu caso, modifiquei o código para ficar exibindo um texto a cada 500ms.

![Compilando o projeto](/images/codigo_modificado.png)

E assim, ficou a exibição no terminal.

![Compilando o projeto](/images/putty_codigo_modificado.png)

Espero que tenha ajudado!

> Aqui, um vídeo que pode ajudar, caso tenha alguma dúvida: **[Talk to Your Pico Over Serial | Raspberry Pi Pico UART Tutorial](https://www.youtube.com/watch?v=pbWhoJdYA1s)**.

