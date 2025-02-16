# 🏗️ OpenStack in a Box

Implementação manual do OpenStack usando Ansible, evitando ferramentas como DevStack para melhor compreensão da arquitetura.

## Sobre o Projeto

Este projeto visa criar um ambiente OpenStack completo para estudos e laboratório, utilizando 24GB de RAM distribuídos em 4 VMs. A instalação é feita via Ansible, permitindo melhor entendimento dos componentes e suas relações.

## Pré-requisitos

- Host Debian Bookworm com KVM configurado
- 24GB RAM disponíveis
- Ansible 2.10+
- Vagrant 2.3+ (opcional, para criação automatizada do ambiente)
- Acesso SSH às VMs (preferencialmente com chaves)
- Conhecimento básico de redes e virtualização

## Arquitetura

O ambiente é composto por 4 nodes:

- **Controller Node (8GB)**: Serviços centrais de controle
- **Network Node (4GB)**: Gerenciamento de rede e conectividade
- **Compute Node (8GB)**: Execução das VMs
- **Storage Node (4GB)**: Armazenamento de imagens e volumes

## Redes

- **Provider (172.16.0.0/16)**: Acesso externo e floating IPs
- **Data (172.17.0.0/16)**: Comunicação entre VMs e storage
- **Management (172.18.0.0/16)**: Comunicação entre serviços OpenStack

## Como Usar

### Usando Vagrant (Recomendado)

O projeto inclui um Vagrantfile configurado para KVM que automaticamente:
- Cria as 4 VMs com as especificações corretas
- Configura as redes necessárias
- Estabelece as bridges no host
- Prepara o acesso SSH

```bash
vagrant up
ansible-playbook playbooks/site.yml
```

### Configuração Manual

1. Clone este repositório
```bash
git clone https://github.com/vndmtrx/openstack-in-a-box.git
cd openstack-in-a-box
```

2. Configure suas VMs no KVM
3. Ajuste o inventário em `inventory/hosts`
4. Execute o playbook:
```bash
ansible-playbook playbooks/site.yml
```

## Contribuindo

Contribuições são bem-vindas! Por favor, leia o arquivo CONTRIBUTING.md antes de enviar pull requests.

## Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Desenvolvido por [vndmtrx](https://github.com/vndmtrx)