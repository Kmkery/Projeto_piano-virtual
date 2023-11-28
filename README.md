# Projeto Piano Virtual :musical_keyboard:

Este projeto de piano virtual faz uso do framework de áudio _**Tone.js**_, cuja biblioteca permite gerar sons e trabalhar com diversos tipos de efeitos e filtros pré-definidos, dispensando a necessidade de uso de samplers.

## Características do projeto
* Interruptor Standby/on;
* Controle de volume;
* Seletor com 3 opções de som;
* Guia com as escalas das notas;
* Controle de visibilidade de marcação de teclas.
* 24 teclas ativáveis por clique, toque ou teclado físico. 

<br />

Mapa das notas musicais para uso do teclado físico:


|Nota |Tecla|   |Nota  |Tecla|
| :-: | :-: |:-:| :-:  | :-: |
|  C  |  A  |   |  C+  |  K  |
|  C# |  Q  |   |  C#+ |  Y  |
|  D  |  S  |   |  D+  |  L  |
|  D# |  W  |   |  D#+ |  U  |
|  E  |  D  |   |  E+  |  Ç  |
|  F  |  F  |   |  F+  |  M  |
|  F# |  E  |   |  F#+ |  I  |
|  G  |  G  |   |  G+  |  ,  |
|  G# |  R  |   |  G#+ |  O  |
|  A  |  H  |   |  A+  |  .  |
|  A# |  T  |   |  A#+ |  P  |
|  B  |  J  |   |  B+  |  ;  |

<br />

## Configurações gerais:

O interruptor _Standby--on`_ foi inserido para habilitar a inicialização do contexto de áudio. Isto se fez necessário uma vez que os navegadores exigem que haja uma prévia interação do usuário para a execução de áudios. Além disto, a inserção deste permite liberar recursos, caso a aplicação esteja aberta mas não sendo utilizada.

O array `allowedKeys` armazenado no objeto `piano` contém os nomes das teclas físicas utilizadas para acionamento das teclas do piano. A referência de cada uma é feita por meio dos atributos `data-keys` dos elementos `li` do index.html, e devem receber como valores os códigos das teclas físicas usadas. Deve-se notar que os elementos `<span>` que se aninham em cada um dos elementos `<li>` devem conter o nome da tecla a qual o `data-keys` se refere, estes serão exibidos quando o interruptor `Teclas` estiver acionado.

Os atributos `data-note` referem-se às notas musicais que devem ser executadas e estão dispostas em ordem de acordo com a posição de teclas de um piano real, portanto, não devem ser alterados.

A seleção do tipo de som é feita pela chave _Seletor_. A mudança de valor do `input` atrelado a ele aciona o callback responsável pelo acesso ao `chooseTypeOfSound(option)`, cujas propriedades nele presentes referem-se à criação de um sintetizador específico. 

Ao criar um novo sintetizador, ele é armazenado na propriedade `synth` do objeto `piano`, executado pela chamada da função `activeNote(key)` e é "descartado" sempre que alteramos o seletor, para liberação dos recursos.

Neste projeto, foram incluídos os sintetizadores `Synth`, `MonoSynth` e `FMSynth`, seguindo as recomendações da documentação do framework Tone.js [^1].

O controle de volume é feito pelo `input` da chave _Volume_, que aciona a função `adjustVolume()` toda vez que o valor de entrada é alterado. O valor máximo fixado neste projeto é o valor "normal" da saída de áudio e a redução do som se dá pela diminuição de ganho (em dB) aplicado a `synth`. A redução máxima é estabelecida por meio da propriedade `volumeRange` do objeto `piano`.

### Referências e inspirações 🤩:
* [Repositório de desafios DIO Potência Tech - Felipe Aguiar](https://github.com/felipeAguiarCode/js-music-keyboard-virtual.git)
* [Documentação do Tone.Js](https://tonejs.github.io/)
* [Tone.js Examples](https://tonejs.github.io/examples/)

[^1]: O framework Tone.js inclui o ScriptProcessorMode (interface obsoleta), porém apenas para verificação de recursos, não impactando no processamento de áudio, desta forma, as mensagens de aviso no console referentes a esta interface podem ser ignoradas.  
