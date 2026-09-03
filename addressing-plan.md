# Plano de Endereçamento IP

Este documento detalha a divisão da rede **192.168.50.0/24** (Máscara de Sub-rede: `255.255.255.0`) para a NovaHealth Analytics.

## Parâmetros da Rede
* **Gateway Padrão:** `192.168.50.1`
* **Endereço IP da Impressora:** `192.168.50.10`
* **Intervalo DHCP:** `192.168.50.20` até `192.168.50.100`

## Divisão de Dispositivos: Estático vs DHCP

| Dispositivo | Tipo de IP | Endereço IP / Intervalo | Justificativa |
| :--- | :--- | :--- | :--- |
| **Roteador (Gateway)** | Estático | `192.168.50.1` | Precisa de um endereço fixo conhecido por todos os dispositivos para o tráfego de saída. |
| **Switches (Gerenciamento)** | Estático | `192.168.50.2` e `192.168.50.3` | Permite o acesso direto e seguro da equipe de TI para fins de manutenção. |
| **Ponto de Acesso (AP)** | Estático | `192.168.50.5` | Facilita o monitoramento do dispositivo e evita falhas de provisionamento Wi-Fi. |
| **Impressora de Rede** | Estático | `192.168.50.10` | Evita que o IP mude. Se o IP mudasse via DHCP, os usuários perderiam a conexão com a impressora. |
| **Computadores (30)** | DHCP | `192.168.50.20` a `192.168.50.100` | Automatiza a configuração das estações, simplificando o suporte e evitando conflitos de IP. |

## Justificativa para as Escolhas Realizadas
1. **Reserva de IPs Estáticos:** Reservamos o intervalo de `.1` a `.19` para dispositivos de infraestrutura crítica (roteador, switches, AP e impressoras), garantindo organização e previsibilidade.
2. **Dimensionamento do DHCP:** O intervalo configurado (`.20` a `.100`) oferece **81 endereços utilizáveis**, o que atende perfeitamente os 30 computadores iniciais e deixa margem segura para crescimento futuro ou dispositivos móveis de visitantes.

## Diagrama Lógico de Conectividade
```text
                  [ INTERNET ]
                       │
                       ▼
               [ Roteador (GW) ] (192.168.50.1)
                       │
        ┌──────────────┴──────────────┐
        ▼                             ▼
  [ Switch 1 ]                  [ Switch 2 ]
   (192.168.50.2)                (192.168.50.3)
        │                             │
        ├── [ Impressora ] (.10)      ├── [ Ponto de Acesso ] (.5)
        │                             │         ) ) ) (Wi-Fi)
        └── [ PCs 01 a 15 ]           │         ▼
            (DHCP: .20 em diante)     └── [ PCs 16 a 30 ]
                                          (DHCP)
```

## Verificações de Conectividade
Abaixo estão descritos três testes básicos que a equipe de TI deve realizar para validar a infraestrutura:

1. **Teste de Conectividade com o Gateway (`ping 192.168.50.1`):**
   * **O que faz:** Dispara pacotes ICMP a partir de uma estação de trabalho em direção ao roteador.
   * **O que permite verificar:** Valida se a fiação física (ou sinal Wi-Fi), o switch e a interface local do roteador estão operando corretamente na camada local.

2. **Verificação de IP por DHCP (`ipconfig` ou `ifconfig`):**
   * **O que faz:** Executa o comando no terminal do computador do usuário para ler as propriedades de rede ativas.
   * **O que permite verificar:** Confirma se o computador conseguiu se comunicar com o servidor DHCP e recebeu com sucesso um IP dentro do intervalo correto (`192.168.50.20-100`), junto com a máscara e o gateway corretos.

3. **Teste de Acesso à Impressora (`ping 192.168.50.10`):**
   * **O que faz:** Executa um teste de eco ICMP direcionado ao IP fixo da impressora.
   * **O que permite verificar:** Garante que a impressora está ligada, conectada à rede física e pronta para receber requisições de impressão vindas de qualquer sub-rede autorizada.
