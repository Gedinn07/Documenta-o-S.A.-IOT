# Bengala Eletrônica Assistiva — Arduino

## 1. Descrição do Projeto

O projeto consiste no desenvolvimento de um protótipo de bengala eletrônica assistiva, utilizando um Arduino Uno R3 e um sensor ultrassônico para detectar obstáculos e auxiliar na percepção do ambiente durante a locomoção.

O sistema realiza medições contínuas de distância e utiliza um buzzer para emitir alertas sonoros de acordo com a proximidade de obstáculos. Quanto menor a distância identificada, mais frequentes se tornam os alertas, permitindo que o usuário perceba a aproximação de objetos.

O protótipo também possui um botão para alternar entre o modo normal e o modo silencioso.

## 2. Objetivos

- Auxiliar na identificação de obstáculos.
- Realizar medições de distância utilizando ondas ultrassônicas.
- Emitir alertas sonoros de acordo com a distância detectada.
- Permitir alternância entre modo normal e silencioso.
- Desenvolver uma solução de tecnologia assistiva utilizando componentes acessíveis.

## 3. Componentes Utilizados

| Componente | Função |
|---|---|
| Arduino Uno R3 | Processamento das informações e controle do sistema. |
| HC-SR04 | Sensor ultrassônico responsável pela detecção e medição de distância. |
| Buzzer passivo | Emissão de alertas sonoros em diferentes frequências. |
| Botão | Alternância entre modo normal e modo silencioso. |
| Bateria de 9 V | Alimentação externa do circuito. |

## 4. Tecnologias Utilizadas

- Arduino Uno R3
- Linguagem C/C++
- Arduino IDE
- Sensor ultrassônico HC-SR04
- Buzzer
- Circuitos eletrônicos

## 5. Funcionamento do Sistema

O sistema funciona a partir da leitura contínua realizada pelo sensor ultrassônico HC-SR04.

O sensor emite um pulso ultrassônico e aguarda o retorno da onda refletida por algum objeto. A partir do tempo de retorno, o Arduino calcula a distância aproximada entre o sensor e o obstáculo.

A distância obtida é armazenada e utilizada pelo sistema para determinar o comportamento do buzzer.

Quando um obstáculo é identificado dentro das faixas configuradas, o buzzer emite sinais sonoros. A frequência dos alertas aumenta conforme o objeto se aproxima.

O sistema possui dois modos de operação:

- **Modo normal:** permite a emissão dos alertas sonoros.
- **Modo silencioso:** desativa os alertas do buzzer.

A alternância entre os modos é realizada por meio de um botão físico, cuja leitura é tratada com uma técnica de debounce para evitar múltiplas ativações decorrentes de oscilações elétricas durante o acionamento.

## 6. Lógica de Detecção de Obstáculos

O sistema utiliza diferentes faixas de distância para determinar a frequência dos alertas sonoros.

| Distância | Frequência do buzzer | Intervalo entre alertas |
|---|---:|---:|
| Até 10 cm | 1800 Hz | 120 ms |
| Acima de 10 até 30 cm | 1600 Hz | 200 ms |
| Acima de 30 até 50 cm | 1400 Hz | 300 ms |
| Acima de 50 até 100 cm | 1200 Hz | 450 ms |
| Acima de 100 até 150 cm | Sem alerta | Sem alerta |
| Acima de 150 até 200 cm | Sem alerta | Sem alerta |
| Acima de 200 cm | Sem alerta | Sem alerta |

Os alertas sonoros possuem duração de aproximadamente 100 ms, sendo controlados pela função `millis()`, permitindo o gerenciamento dos intervalos sem interromper continuamente a execução do programa.

## 7. Sistema de Alimentação

O protótipo utiliza uma bateria externa de 9 V conectada à entrada VIN e ao GND do Arduino Uno.

A placa utiliza seu regulador interno de tensão para fornecer a alimentação necessária ao funcionamento dos componentes compatíveis.

A alimentação externa permite que o dispositivo funcione de maneira independente de um computador, proporcionando maior mobilidade durante os testes.

## 8. Mapeamento de Pinos

| Arduino | Componente | Descrição |
|---|---|---|
| D13 | Buzzer | Saída dos alertas sonoros. |
| D12 | Botão | Alternância entre modos. |
| D11 | HC-SR04 TRIG | Emissão do pulso de disparo. |
| D10 | HC-SR04 ECHO | Recepção do sinal refletido. |
| VIN | Bateria 9 V (+) | Alimentação externa. |
| GND | Bateria 9 V (-) | Referência elétrica do circuito. |

## 9. Estrutura do Código

O código foi organizado em funções para facilitar a manutenção, leitura e compreensão do sistema.

| Função | Responsabilidade |
|---|---|
| `setup()` | Inicialização dos pinos, comunicação serial e componentes. |
| `verificarBotao()` | Leitura do botão e alternância entre os modos. |
| `lerSensor()` | Realização da leitura ultrassônica e validação da distância. |
| `desligarBuzzer()` | Desativação do buzzer. |
| `controlarBuzzer()` | Gerenciamento da frequência, duração e intervalo dos alertas. |
| `controlarSistema()` | Interpretação da distância e definição do comportamento dos alertas. |
| `loop()` | Execução contínua das funções principais do sistema. |

## 10. Tratamento de Leituras

O sistema utiliza um tempo limite de 25.000 microssegundos para aguardar o retorno do sinal ultrassônico.

Leituras inválidas, valores nulos ou distâncias fora da faixa de 2 a 400 cm são descartados.

Quando uma leitura inválida ocorre, o sistema mantém a última distância válida armazenada. Caso ainda não exista uma leitura válida, o buzzer permanece desligado.

A comunicação serial, configurada em 9600 baud, permite acompanhar as distâncias identificadas e o estado de operação do sistema durante os testes.

## 11. Limitações

- O alcance e a precisão dependem das características do objeto detectado.
- Objetos estreitos, inclinados ou com superfícies que absorvem ondas sonoras podem dificultar a detecção.
- O sensor possui uma área de detecção limitada.
- O sistema não identifica o tipo de obstáculo.
- A autonomia depende da capacidade da bateria e do consumo dos componentes.
- O protótipo ainda não foi desenvolvido para garantir segurança em ambientes reais.

## 12. Possíveis Melhorias

- Otimização do consumo de energia.
- Melhorias na estrutura física e ergonomia.
- Implementação de novos sensores para ampliar a área de detecção.
- Ajustes nos níveis de alerta sonoro.
- Melhorias na proteção dos componentes eletrônicos.
- Testes de precisão e confiabilidade em diferentes ambientes.

## 13. Considerações Finais

O desenvolvimento do protótipo demonstra a aplicação de conhecimentos de programação, eletrônica e sistemas embarcados na criação de uma ferramenta voltada à acessibilidade.

A bengala eletrônica utiliza sensores e processamento de dados para identificar obstáculos e emitir alertas, demonstrando como tecnologias de baixo custo podem ser aplicadas em projetos com potencial impacto social.

O dispositivo deve ser considerado uma ferramenta complementar, não substituindo a bengala tradicional, técnicas de orientação e mobilidade ou outros recursos de segurança utilizados por pessoas com deficiência visual.

---

**Projeto acadêmico — protótipo experimental de tecnologia assistiva.**
