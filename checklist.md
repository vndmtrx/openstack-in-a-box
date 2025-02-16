# Distribuição OpenStack

## Host KVM
- [ ] 3 bridges para as redes:
  - br-prov (172.16.0.1/16) - bridge para rede provider (externa)
  - br-data (172.17.0.1/16) - bridge para rede de dados
  - br-mgmt (172.18.0.1/16) - bridge para rede de management

## Máquinas Virtuais

### Controller Node (8GB RAM, 2 vCPUs, 50GB)
- [ ] 2 interfaces:
  - vnet0 -> br-prov: 172.16.0.10
  - vnet1 -> br-mgmt: 172.18.0.10
- Serviços:
  - [ ] MariaDB
  - [ ] RabbitMQ
  - [ ] Memcached
  - [ ] Keystone
  - [ ] Nova (API + Scheduler)
  - [ ] Neutron Server
  - [ ] Horizon

### Network Node (4GB RAM, 2 vCPUs, 30GB)
- [ ] 3 interfaces:
  - vnet0 -> br-prov: 172.16.0.20
  - vnet1 -> br-data: 172.17.0.20
  - vnet2 -> br-mgmt: 172.18.0.20
- Serviços:
  - [ ] Neutron (L3, DHCP, Metadata)
  - [ ] Open vSwitch

### Compute Node (8GB RAM, 4 vCPUs, 100GB)
- [ ] 2 interfaces:
  - vnet0 -> br-data: 172.17.0.30
  - vnet1 -> br-mgmt: 172.18.0.30
- Serviços:
  - [ ] Nova Compute
  - [ ] Neutron OVS Agent
  - [ ] Libvirt/QEMU-KVM

### Storage Node (4GB RAM, 2 vCPUs, 100GB)
- [ ] 1 interface:
  - vnet0 -> br-mgmt: 172.18.0.40
- Serviços:
  - [ ] Glance
  - [ ] Cinder

## Redes
- Provider (172.16.0.0/16): Acesso externo e floating IPs
- Data (172.17.0.0/16): Comunicação entre VMs e storage
- Management (172.18.0.0/16): Comunicação entre serviços OpenStack e gerenciamento