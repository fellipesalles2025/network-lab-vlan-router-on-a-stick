# Projeto de Redes — VLANs, Subnetting e Router-on-a-Stick

## 📌 Sobre o projeto

Este projeto foi desenvolvido com o objetivo de praticar conceitos fundamentais de redes de computadores, utilizando o **Cisco Packet Tracer**.

A atividade envolveu planejamento de endereçamento IP, subnetting, segmentação de rede com VLANs, configuração de switches e roteador, acesso remoto seguro via SSH e implementação do conceito Router-on-a-Stick.

Além da implementação, foram realizados testes de conectividade entre os dispositivos para verificar a comunicação entre diferentes redes e o funcionamento da infraestrutura.

## 🖥️ Topologia da rede

A infraestrutura é composta por:

- 1 roteador Cisco 1941 (R1);
- 2 switches Cisco 2960-24TT (SW1 e SW2);
- 4 computadores (PC1, PC2, PC3 e PC4).

O roteador está conectado ao SW1, que por sua vez está conectado ao SW2. Os enlaces entre os equipamentos de infraestrutura utilizam portas configuradas como trunk para transportar o tráfego das VLANs.

## 🌐 Planejamento de endereçamento IP

Foram utilizadas três redes distintas, organizadas de acordo com suas finalidades.

| VLAN | Finalidade | Rede | Máscara |
|---|---|---|---|
| 10 | Rede de computadores | 192.168.1.0/25 | 255.255.255.128 |
| 20 | Rede de computadores | 192.168.1.128/25 | 255.255.255.128 |
| 50 | Gerenciamento dos switches | 192.168.2.0/28 | 255.255.255.240 |

### Endereçamento dos dispositivos

| Dispositivo | VLAN | Endereço IP |
|---|---:|---|
| PC1 | 10 | 192.168.1.2 |
| PC2 | 10 | 192.168.1.3 |
| PC3 | 20 | 192.168.1.130 |
| PC4 | 20 | 192.168.1.131 |
| R1 — G0/0.10 | 10 | 192.168.1.1 |
| R1 — G0/0.20 | 20 | 192.168.1.129 |
| SW1 — VLAN 50 | 50 | 192.168.2.2 |
| SW2 — VLAN 50 | 50 | 192.168.2.3 |
| R1 — G0/0.50 | 50 | 192.168.2.1 |

A VLAN 50 foi destinada ao gerenciamento dos switches, utilizando uma sub-rede /28 para essa finalidade.

## ⚙️ Configurações implementadas

### 1. VLANs e segmentação de rede

Foram utilizadas três VLANs:

- **VLAN 10:** primeira rede de computadores.
- **VLAN 20:** segunda rede de computadores.
- **VLAN 50:** rede de gerenciamento dos switches.

As portas destinadas aos computadores foram configuradas em modo access, enquanto os enlaces entre os equipamentos de infraestrutura foram configurados em modo trunk.

### 2. Router-on-a-Stick

Foi implementada a técnica Router-on-a-Stick, permitindo que um único roteador realize o roteamento entre diferentes VLANs por meio de subinterfaces.

Foram criadas as seguintes subinterfaces:

- G0/0.10 — VLAN 10;
- G0/0.20 — VLAN 20;
- G0/0.50 — VLAN 50.

Cada subinterface recebeu o encapsulamento IEEE 802.1Q e um endereço IP correspondente à sua rede.

Essa configuração permite a comunicação entre dispositivos pertencentes a diferentes VLANs sem a necessidade de utilizar uma interface física exclusiva para cada rede.

### 3. Gerenciamento dos switches

Foi criada a VLAN 50 para gerenciamento dos switches, com configuração de endereços IP nas interfaces virtuais de gerenciamento (SVI).

Também foi configurado o gateway padrão dos switches, apontando para o endereço 192.168.2.1.

### 4. Acesso remoto via SSH

Foi configurado o acesso remoto seguro via SSH no roteador e nos dois switches.

As configurações incluíram:

- Criação de usuário local;
- Configuração de domínio;
- Geração de chaves RSA;
- Configuração das linhas VTY;
- Autenticação local;
- Restrição do acesso remoto ao protocolo SSH.

Também foram configuradas senhas para proteção do modo privilegiado e das linhas de console.

### 5. Configuração dos computadores

Os computadores receberam endereços IP estáticos, máscaras de sub-rede e gateways padrão de acordo com a VLAN à qual pertencem.

## 🧪 Testes realizados

Foram realizados testes de conectividade entre os computadores, switches e roteador, utilizando os resultados para verificar a comunicação dentro da infraestrutura.

Entre os testes documentados estão:

- PC1 para PC2;
- PC1 para PC3;
- PC1 para PC4;
- PC1 para SW1;
- PC2 para PC1;
- PC2 para PC3;
- PC2 para SW2;
- PC3 para SW1;
- PC4 para PC2.

### Testes de acesso SSH

Também foram realizados testes de acesso remoto via SSH a partir do PC1, tendo como destinos os dois switches e o roteador.

O objetivo foi validar o acesso administrativo seguro aos equipamentos por meio da rede.

### Ocorrências identificadas e soluções

**1. Problema de gateway no PC2**

Durante os testes, foi identificado um problema de comunicação entre PC2 e PC3.

Após análise, foi constatado que o gateway padrão configurado no PC2 estava incorreto.

**Solução:** correção do gateway padrão para 192.168.1.1, restabelecendo a comunicação.

**2. Falha inicial de conexão SSH**

Durante os primeiros testes de acesso remoto, a conexão SSH não foi bem-sucedida devido à ausência das chaves RSA necessárias para estabelecer o serviço.

**Solução:** geração das chaves RSA nos equipamentos, permitindo a utilização do SSH e a realização dos testes de acesso remoto.

Após os ajustes, os testes de SSH nos switches e no roteador foram realizados com êxito.

## 📚 Conhecimentos praticados

Este projeto proporcionou a aplicação prática dos seguintes conceitos:

- Endereçamento IPv4;
- Subnetting e cálculo de sub-redes;
- Máscaras de sub-rede e prefixos CIDR;
- Segmentação de redes com VLANs;
- Configuração de portas Access e Trunk;
- Encapsulamento IEEE 802.1Q;
- Roteamento entre VLANs;
- Router-on-a-Stick;
- Interfaces virtuais de gerenciamento (SVI);
- Configuração de gateway padrão;
- Acesso remoto seguro via SSH;
- Geração de chaves RSA;
- Testes de conectividade e troubleshooting.

## 🛠️ Ferramenta utilizada

- Cisco Packet Tracer.

## 🎯 Considerações finais

O desenvolvimento deste projeto permitiu consolidar conhecimentos fundamentais de redes de computadores, desde o planejamento lógico do endereçamento IP até a configuração dos equipamentos e validação da conectividade.

A implementação de VLANs e Router-on-a-Stick possibilitou compreender, na prática, como diferentes redes podem coexistir em uma mesma infraestrutura física e se comunicar por meio de roteamento.

Além disso, a configuração de SSH e de uma VLAN dedicada ao gerenciamento permitiu praticar conceitos relacionados à administração e segurança de dispositivos de rede.

Este projeto faz parte do meu processo de aprendizado e desenvolvimento de habilidades práticas em infraestrutura e redes de computadores.
