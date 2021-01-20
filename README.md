# DOCUMENTATION

Run STCv traffic generator instances with public and test networks.

Instances can be controlled by the Spirent TestCenter application.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.13.0 |
| azurerm | >=2.37.0 |

## Providers

| Name | Version |
|------|---------|
| azurerm | >=2.37.0 |
| template | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| admin\_username | Administrator user name | `string` | `"azureuser"` | no |
| enable\_accelerated\_networking | Flag to enable or disable accelerated networking on network interface | `string` | `"true"` | no |
| ingress\_cidr\_blocks | List of management interface ingress IPv4/IPv6 CIDR ranges. | `list(string)` | n/a | yes |
| instance\_count | Number of STCv instances to create.. | `string` | n/a | yes |
| instance\_name | Name assigned to the instance.  An instance number will be appended to the name | `string` | `"stcv"` | no |
| instance\_size | Specifies the size of the STCv VM instance. | `string` | `"Standard_DS3_v2"` | no |
| marketplace\_version | The Spirent TestCenter Virtual image version example 5.15.0106. When not specified, the latest marketplace image will be used. | `string` | n/a | yes |
| mgmt\_plane\_subnet | Management public Azure subnet name | `string` | n/a | yes |
| public\_key | File path to public key. | `string` | `"~/.ssh/id_rsa.pub"` | no |
| resource\_group\_location | Resource group location in Azure | `string` | `"West US 2"` | no |
| resource\_group\_name | Resource group name in Azure | `string` | `"default"` | no |
| test\_plane\_subnet | Test or data plane Azure subnet name | `string` | n/a | yes |
| user\_data\_file | File path name containing AWS user data for the instance.  Spirent TestCenter Virtual cloud-init configuration parameters are supported. | `string` | n/a | yes |
| virtual\_network | User provided virtual network | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| instance\_ids | List of IDs of instances |
| instance\_private\_ips | List of private IP addresses assigned to the instances, if applicable |
| instance\_public\_ips | List of public IP addresses assigned to the instances, if applicable |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## User Data (cloud-init)

### Example
```
#cloud-config
spirent:
  driver: dpdk
  speed: 10G
```

### Parameters

| Name | Description |  Type | Default 
|------|-------------|-------------|-------------
| speed | Maximum network interface speed | 1G, 5G, 10G, 25G, 50G, 100G | 1G
| driver | Network driver interface | sockets, dpdk | dpdk (for supported cloud provider instances) 
| rxq | RX queue size for dpdk driver | 1-N | 1
| benchmark | Turn benchmark rate mode on or off for dpdk driver| off, on | off
| ntp | NTP server | IP address | x.x.x.x (cloud provider recommended)
| ipv4mode | IPv4 address mode | none, static, dhcp | dhcp
| ipaddress | IPv4 address (static mode) | IPv4 address | - 
| netmask | IPv4 netmask (static mode) | IPv4 netmaks | -  
| gwaddress | IPv4 gateway address (static mode) | IPv4 gateway address | - 
| ipv6mode | IPv6 address mode | none, static, dhcp | none
| ipv6address | IPv4 address (static mode) | IPv4 address | - 
| ipv6prefixlen | IPv6 prefix length (static mode) | IPv4 netmaks | -  
| ipv6gwaddress | IPv4 gateway address (static mode) | IPv6 gateway address | - 
| gvtap | Turn Gigamon gvtap agent on or off| off, on | off