# NovaHealth Network - Configuração Básica

## Descrição do cenário e visão geral da solução
Este repositório contém a proposta técnica de conectividade e a documentação básica de rede para o novo escritório da **NovaHealth Analytics**, 
projetado para atender **30 colaboradores**. A infraestrutura foi planejada para garantir acesso estável à rede corporativa, à Internet, 
aos serviços de impressão compartilhada e à conectividade sem fio (Wi-Fi). A rede utiliza o bloco de endereçamento **192.168.50.0/24**, 
oferecendo até 254 endereços utilizáveis. A topologia foi desenhada com redundância e distribuição de carga locais 
utilizando dois switches para interconectar as estações de trabalho e os periféricos, centralizados sob um roteador principal que realiza a comunicação externa 
e o gerenciamento lógico dos endereços via DHCP.

## Função de Cada Dispositivo de Rede
* **Roteador (1 unidade):** Funciona como a borda da rede. É responsável por interconectar a rede local (LAN) à Internet (WAN),
realizar o roteamento de pacotes e atuar como o Gateway Padrão e servidor DHCP para a distribuição automatizada de IPs.

* **Switches (2 unidades):** Dispositivos responsáveis pela comutação de dados dentro da rede local (LAN).
Eles conectam fisicamente os computadores e a impressora via cabos de rede, garantindo alta velocidade e encaminhamento de dados direto ao destino via endereços MAC.

* **Ponto de Acesso / AP (1 unidade):** Fornece conectividade sem fio (Wi-Fi) de alta performance para o escritório,
permitindo que os colaboradores se conectem à rede corporativa sem a necessidade de cabos.

* **Impressora de Rede (1 unidade):** Periférico compartilhado que centraliza os serviços de impressão do escritório,
configurado de forma estática para estar sempre disponível.

* **Computadores (30 unidades):** As estações de trabalho dos usuários que consomem os serviços da rede, internet e ferramentas corporativas.
