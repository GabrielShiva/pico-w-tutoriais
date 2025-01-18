# COMO CRIAR COMUNICAÇÃO ENTRE O PUTTY E O RASPBERRY PI PICO W

## SUMÁRIO
1. **[Configurando Putty e o Projeto](#configurando-putty-e-o-projeto)**
2. **[Sobre o Zaddig](#sobre-o-zadig)**


## Configurando Putty e o Projeto
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

- Ligue a placa do raspberry pi (colocando a chave na posição LIGAR) e, em seguida, coloque a placa no modo bootsel, segurando o botão branco e apertando, ao mesmo tempo, o botão de reset da placa. Matenha o USB da placa desconectada do computador.

- Digite na barra de pesquisa do Windows: gerenciador de dispositivos.

- Na aba de gerenciador de dispositivos, clique em *Exibir > Mostrar dispositivos ocultos*.

![Listando dispositivos ocultos](/images/dispositivos_ocultos.png)

- Após listar os dispositivos ocultos, clique na opção Portas (COM e LPT).

![Portas sem o PICO](/images/portas_sem_pico.png)

- Conecte o pico W no computador por meio do USB. 

- APós conectar a placa via USB ao seu PC, compile o projeto.

![Compilando o projeto](/images/compilando.png)

- Com o projeto compilado, vá até a pasta que o seu projeto está localizado, entre na pasta build e arraste o arquivo **.uf2** para o dispositivo com o nome *RPI-RP2* que se localiza no menu da esquerda.

![Carrengando arquivos .uf2 para o pico w](/images/carregando_arquivo_para_pico.png)

- De volta ao *gerenciador de dispositivos*, veja a qual porta o pico está conectado. No meu caso foi a porta *COM8* e anote esta informação.

![Verificando porta da placa](/images/observando_porta.png)

- Instale o putty no seguinte link: **[clique aqui](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)**.

- Selecione uma versão (.exe) do putty de acordo com o seu PC (se ele é 32bits ou 64bits).

![Fazendo o download do executável do putty](/images/baixando_putty.png)

- Após isso, abra o programa putty, clique na opção *Serial* e digite o seguinte:
    - Em *Serial line*, digite a porta que a sua placa está conectada (COM8, no meu caso);
    - Em *Speed*, digite **115200**.

![Configurando o putty](/images/configurando_putty.png)

- Após digitar as informações necessárias, clique no botão **Open**.

- Com o terminal aberto, digite algum texto com o seu teclado (como *PEIXE*) e aperte a tecla **Enter**. O seu texto que você escreveu deve aparecer na tela de comando.

![Testando o código no putty](/images/testando_terminal_serial.png)

> **NOTA**: perceba que, enquanto você estiver digitando o texto, o retorno do que você estiver digitando não aparecerá na tela, apenas quando você clicar na tecla Enter.

Após isso, sempre repita o mesmo processo:
- Modifique o seu código;
- Compile o código;
- Coloque a placa em modo Bootsel;
- Carregue o arquivo .uf2 para a placa;
- Abra o putty, coloque em serial e especifique as infos (PORTA e VELOCIDADE);
- Clique no botão abrir e teste o seu código.

No meu caso, modifiquei o código para ficar exibindo um texto a cada 500ms.

![Compilando novo código do projeto](/images/codigo_modificado.png)

E assim, ficou a exibição no terminal do código modificado.

![Exibindo o código modificado no putty](/images/putty_codigo_modificado.png)

# Sobre o Zadig

Colocando a placa no modo Bootsel, abra o zadig e clique na opção para listar todos os dispositivos.

![Listar todos os dispositivos no zadig](/images/zadig_dispositivos.png)

Aparecerá o dispositivo RP2 com duas interfaces, *Interface 0* e a *Interface 1*. 

![Exibindo a lista com os dispositivos no zadig](/images/zadig_lista.png)

Não importa o que aconteça, não mexa na **Interface 0**. Selecione a Interface 1 e clique em **Install Driver**. Caso para você apareça **Reinstall Driver**, não será necessário fazer nada. Após isso, se quiser desinstale esse programa, pois ele não será mas necessário.

![Exibindo o driver da interface 01 no zadig](/images/zadig_reinstall.png)

A título de curiosidade, o driver que deve aparecer para a Interface 0 é a presente na imagem abaixo.

![Exibindo o driver da interface 02 no zadig](/images/zadig_interface_0.png)

Espero que tenha ajudado!

> Aqui, um vídeo que pode ajudar, caso tenha alguma dúvida: **[Talk to Your Pico Over Serial | Raspberry Pi Pico UART Tutorial](https://www.youtube.com/watch?v=pbWhoJdYA1s)**.

