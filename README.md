<h1 align="center">REESTRUTURAÇÃO COMPLETA DA INFRAESTRUTURA DE REDE / PLÁSTICOS ALKO LTDA</h1>			
<br>
<h4 align="center"> 🚀 Concluído 🚀 </h4>

Tabela de conteúdos
=================
<!--ts-->
   * [Sobre o projeto](#-sobre-o-projeto)
   * [Principais melhorias técnicas](#principais-melhorias-técnicas)
   * [Documentação](#documentação)
* [Sistemas implantados](#sistemas-implantados)
     * [Pi-hole](#pi-hole)
   * [Tecnologias](#-tecnologias)
   * [Autor](#-autor)
   * [Licença](#-licença)
<!--te-->

## 💻 Sobre o projeto

Descrição:
Nesse projeto atuei como analista senior de infraestrutura, sendo o responsavel final por decisões e implantações técnicas realizei uma reestruturação completa da topologia de rede da empresa plásticos alko ltda, onde inicialmente encontrei um ambiente sem qualquer sistema de monitoramento, com diversos hubs interligados em cascata e desempenho extremamente limitado. após análise e planejamento, implementei uma nova infraestrutura baseada em topologia estrela, utilizando switches gerenciáveis e integrando servidor dns próprio (pihole), servidor de virtualização (proxmox) e armazenamento em nuvem interno (nextcloud). além das melhorias técnicas, também conduzi uma renegociação contratual com a operadora, resultando em uma otimização significativa de desempenho e custos.


## Principais melhorias técnicas:
```bash
### Alteração da topologia de rede
- Antes: rede em cascata com hubs e sem monitoramento; o endpoint mais distante do cpd recebia menos de 1 mbps via cabo (em um link contratado de 100 mbps).

- Depois: rede em topologia estrela com switches gerenciáveis e monitoramento ativo; conectando os switches ao CPD via cabeamento de fibra ótica monomodo e os endpoint via cabeamento CAT6 com plano de redundancia e retirada de todos os hubs da rede, todos os endpoints passaram a receber 700 mbps via cabo e wi-fi independente da localização.

- Resumo: Melhoria de desempenho: +600 % na entrega de banda e estabilidade da rede.
```
```bash
### Revisão do contrato de serviço de internet
- Antes: link corporativo de 100 mbps por r$ 2 000,00/mês.

- Depois: link dedicado de 700 mbps, com rota independente da rede de redundância, por r$ 600,00/mês.

- Resumo: Economia mensal: 70% de redução no custo e 600 % de aumento na velocidade contratada.
```
```bash
### Padronização da rede sem fio
- Antes: o Wi-Fi em cada galpão possuia seu próprio SSID e servidores DHCP, resultando em necessidade de reautenticação constante dos usuários, multiplas senhas e configurações, problemas de monitoramento e configurações despadronizadas.

- Depois: unifiquei toda a rede wi-fi, que antes era fragmentada, tornando-a única e estável em um terreno de aproximadamente 800 m de profundidade por 500 m de largura.

- Resumo: Cobertura total e roaming eficiente.
```
```bash
### Implantação de metodologias de segurança e qualidade
- Antes: Falta de informações de velocidade de navegação, tipo de tráfego do usuário, controle de acesso, recebimento de publicidade e fishing em excesso, sem informações de queda de serviço
 
- Depois: com a implantação das ferramentas de monitoramento e filtragem (pihole e sistema próprio de alertas), reduzi em cerca de 90 % as propagandas durante a navegação, identifiquei e eliminei 100 % dos trojans presentes no parque computacional e implementei um sistema desenvolvido por mim para monitorar servidores e o sistema de câmeras, detectando falhas de rede de forma proativa e automatizada.

- Resumo: Aumento da proteção dos dados e na qualidade do ambiente.
```
```bash
### Redução no custo de sistemas internos
- Antes: Excesso de servidores sem uso e/ou com uso superficiais comparados a seu desempenho, NAS cloud contratado com custo de médio de R$ 3.000,00 mensais, VM's contratadas com o custo mensal em R$ 10.000,00, contrato de prestação de serviços para consultorias de SI e servidores com custo de R$ 10.000,00, Firewall Draytek obsoleto, não comportava mais o tráfego de dados, não lia nova regras de segurança e congelava com frequência, possuia uma mensalidade de serviço de R$ 2.500,00 anuais.

Depois: Implantei o sistema Proxmox nos servidores trazendo as VM's para dentro de casa de forma gratuita, implantei o Pi-Hole para atuação como servidor DNS com reduncia via Keepalive d forma gratuita, implantei um banco de baterias com no-breack para autonomia de até 10 horas em nossos servidores, mensurei, documentei e criei uma base de conhecimento interna, trazendo nohall e independência para nossa equipe interna, implantei o Nextcloud para criação do NAS cloud de forma gratuita com saida via proxy reverso do cloudflare, implantei gratuita do firewall PFsense, alterei as politicas do anti-virus Kaspersky já contratada para que ele tambem atuasse como sistema de SI mais eficas

- Resumo: Economia de aproximadamente R$ 25.000,00 Mensais ao final do projeto, retorno do valor total investido no projeto em 7 Meses.
```

## Documentação
### Sistemas implantados
#### Pi-hole
Site Oficial: **[Pi-hole](https://pi-hole.net/)**
<p>Imagem demonstrativa:</p>
<p align="center" style="display: flex; align-items: flex-start; justify-content: center;">
<img alt="Pi-Hole" title="#Pi-Hole" src="https://wp-cdn.pi-hole.net/wp-content/uploads/2020/04/Dashboard.png" style="width:500px";/>
</p>

```bash
Pi-hole é um software de bloqueio de anúncios e rastreadores em nível de rede, funcionando como um servidor DNS recursivo e opcionalmente como servidor DHCP. Ele atua como um "DNS sinkhole", interceptando solicitações de domínios conhecidos por hospedarem anúncios, malwares ou rastreadores, impedindo que esses conteúdos sejam carregados nos dispositivos da rede.

⚙️ Funcionamento Técnico
Resolução DNS:
Quando um dispositivo na rede solicita o endereço IP de um domínio (ex: ads.google.com), o Pi-hole intercepta essa requisição DNS.
Se o domínio estiver em uma lista de bloqueio (blocklist), o Pi-hole retorna um IP nulo (0.0.0.0), bloqueando o carregamento.
Se não estiver bloqueado, o Pi-hole encaminha a solicitação para o servidor DNS upstream (ex: Cloudflare, Google DNS, OpenDNS).

O Pi-hole oferece um painel administrativo via navegador, onde é possível:
Monitorar o tráfego DNS em tempo real.
Adicionar ou remover domínios das listas de bloqueio/permitidos.
Gerar relatórios de estatísticas e desempenho da rede.
É leve e consome poucos recursos de CPU e memória.

🧩 Componentes Principais
FTL (Fast Telemetry Logging): Motor interno que combina as funções de dnsmasq, lighttpd e SQLite, responsável pela resolução DNS, armazenamento em cache e registro estatístico.
Web Admin Interface: Painel gráfico para administração e visualização de logs.
Blocklists: Conjuntos de domínios bloqueados (podem ser importados de listas públicas).
Upstream DNS Servers: Servidores externos para resolução de domínios não bloqueados.

☁️ Benefícios Técnicos
Redução de largura de banda consumida por anúncios e rastreamento.
Melhoria perceptível no tempo de carregamento de páginas.
Aumento da privacidade do usuário e proteção contra malvertising.
Monitoramento centralizado de todas as consultas DNS da rede.
```
#### Nextcloud
Site Oficial: **[Nextcloud](https://nextcloud.com/)**
<p>Imagem demonstrativa:</p>
<p align="center" style="display: flex; align-items: flex-start; justify-content: center;">
<img alt="Nextcloud" title="#Nextcloud" src="https://nextcloud.com/c/uploads/2022/03/nextcloud-data-sheet-user-management-ldap-1024x576.jpg" style="width:500px";/>
</p>

```bash
O Nextcloud é uma plataforma open source de armazenamento, sincronização e colaboração em nuvem, semelhante a serviços como Google Drive, Dropbox e OneDrive, porém com o diferencial de permitir hospedagem própria (self-hosted).

⚙️ Arquitetura e Componentes Principais
Servidor Web (Apache ou Nginx)
Responsável por atender as requisições HTTP/HTTPS.
Serve a interface web e conecta os usuários aos serviços da aplicação.
Aplicação Nextcloud (PHP)
Camada central do sistema.
Gerencia autenticação, permissões, sincronização, compartilhamento e APIs REST.
Banco de Dados (MySQL/MariaDB, PostgreSQL, SQLite)
Armazena metadados, usuários, permissões, tokens de acesso e logs de sincronização.
Armazenamento de Arquivos
Diretório local, rede (NFS, SMB), ou provedores externos (Amazon S3, Google Cloud, etc.).
Os arquivos dos usuários ficam criptografados e organizados no servidor.
Interface Web e Aplicativos
Interface responsiva acessível via navegador, além de apps para Windows, Linux, macOS, Android e iOS.
Sincroniza automaticamente arquivos, contatos e calendários.

🧩 Funcionalidades Principais
Sincronização automática de arquivos entre dispositivos.
Compartilhamento seguro de pastas e links com controle de acesso.
Integração com LDAP/Active Directory para autenticação corporativa.
Criptografia de dados em repouso e em trânsito (SSL/TLS).
Extensões e aplicativos adicionais (Calendário, E-mail, Chat, Documentos, etc.).
APIs abertas (WebDAV, CalDAV, CardDAV) para integração com outros sistemas.

🛠️ Casos de Uso
Ambientes corporativos: substitui soluções comerciais de nuvem com total controle interno.

🔒 Segurança e Privacidade
Suporte a autenticação em dois fatores (2FA).
Criptografia ponta a ponta e controle granular de permissões.
Logs detalhados de acesso e auditoria.
Conformidade com GDPR e boas práticas de segurança de dados.

☁️ Benefícios Técnicos
Total controle sobre dados e infraestrutura.
Extensível via módulos (Nextcloud Talk, Office, Mail, etc.).
Compatível com Docker e Kubernetes, facilitando deploys escaláveis.
Integração com Cloudflare Tunnel ou reverse proxy para acesso remoto seguro.
```
#### pfSense
Site Oficial: **[pfSense](https://www.pfsense.org/)**
<p>Imagem demonstrativa:</p>
<p align="center" style="display: flex; align-items: flex-start; justify-content: center;">
<img alt="pfSense" title="#pfSense" src="https://www.netgate.com/hubfs/Images/pfsense-screen.png" style="width:500px";/>
</p>

```bash
O pfSense é uma plataforma de firewall e roteamento de código aberto baseada em FreeBSD, amplamente utilizada em redes corporativas e residenciais avançadas. Ele oferece um ambiente completo para gerenciamento de tráfego, segurança, segmentação de rede e serviços de rede, podendo ser instalado em hardware dedicado, máquinas virtuais ou appliances de rede.

🧩 Funcionalidades Principais
Firewall e Controle de Tráfego: Permite definir regras detalhadas de acesso entre redes, segmentação de sub-redes e filtragem de pacotes, suportando tanto IPv4 quanto IPv6.
VPN (Virtual Private Network): Suporte nativo a IPsec, OpenVPN e WireGuard, permitindo conexões seguras site-to-site ou acesso remoto de clientes, com criptografia avançada.
Roteamento Avançado: Suporte a rotas estáticas, protocolos dinâmicos (OSPF, BGP) e multi-WAN, garantindo alta disponibilidade e redundância de links.
DHCP e DNS: Servidor DHCP integrado e funções de DNS, incluindo suporte a DNS forwarder e resolver.
Gerenciamento de Banda e QoS: Controle de largura de banda por interface, aplicação ou IP, permitindo priorização de tráfego crítico.
Monitoramento e Logs: Ferramentas integradas para análise de tráfego, eventos de firewall, estatísticas de VPN e alertas, facilitando auditoria e troubleshooting.
Pacotes adicionais: Possibilidade de instalar pacotes extras, como pfBlockerNG (bloqueio de IPs/malware), Squid (proxy caching) e Suricata (IDS/IPS), ampliando funcionalidades de segurança e performance.

☁️ Benefícios Técnicos
Segurança robusta: Controle granular sobre todo o tráfego da rede e proteção contra ameaças externas.
Flexibilidade e escalabilidade: Funciona em ambientes pequenos ou complexos, podendo gerenciar múltiplas VLANs, sub-redes e links WAN simultaneamente.
Centralização da rede: Permite consolidar serviços de firewall, VPN, DHCP, DNS e roteamento em uma única plataforma.
Alta disponibilidade: Suporte a failover e balanceamento de carga em múltiplos links de internet, garantindo continuidade do serviço.Customização e automação: Configurações avançadas via interface web, CLI ou scripts, permitindo adaptação a diferentes cenários de rede.
Integração com home labs e virtualização: Pode ser virtualizado em Proxmox, VMware ou Hyper-V, facilitando testes, segmentação de redes domésticas e acesso remoto seguro.
```
