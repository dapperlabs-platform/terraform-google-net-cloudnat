# Cloud NAT Module

Simple Cloud NAT management, with optional router creation.

## Example

```hcl
module "nat" {
  source         = "github.com/dapperlabs-platform/terraform-google-net-cloudnat?ref=tag"
  project_id     = "my-project"
  region         = "europe-west1"
  name           = "default"
  router_network = "my-vpc"
}
# tftest:modules=1:resources=2
```

<!-- BEGIN_TF_DOCS -->
Copyright 2021 Google LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | ~> 1 |
| <a name="requirement_google"></a> [google](#requirement\_google) | >= 5.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_google"></a> [google](#provider\_google) | >= 5.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [google_compute_router.router](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_router) | resource |
| [google_compute_router_nat.nat](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_router_nat) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_addresses"></a> [addresses](#input\_addresses) | Optional list of external address self links. | `list(string)` | `[]` | no |
| <a name="input_config_enable_dynamic_port_allocation"></a> [config\_enable\_dynamic\_port\_allocation](#input\_config\_enable\_dynamic\_port\_allocation) | Enable Dynamic Port Allocation | `bool` | `true` | no |
| <a name="input_config_enable_endpoint_independent_mapping"></a> [config\_enable\_endpoint\_independent\_mapping](#input\_config\_enable\_endpoint\_independent\_mapping) | Enables endpoint independent mapping | `bool` | `false` | no |
| <a name="input_config_max_ports_per_vm"></a> [config\_max\_ports\_per\_vm](#input\_config\_max\_ports\_per\_vm) | Maximum number of ports allocated to a VM from this NAT config. | `number` | `65536` | no |
| <a name="input_config_min_ports_per_vm"></a> [config\_min\_ports\_per\_vm](#input\_config\_min\_ports\_per\_vm) | Minimum number of ports allocated to a VM from this NAT config. | `number` | `1024` | no |
| <a name="input_config_source_subnets"></a> [config\_source\_subnets](#input\_config\_source\_subnets) | Subnetwork configuration (ALL\_SUBNETWORKS\_ALL\_IP\_RANGES, ALL\_SUBNETWORKS\_ALL\_PRIMARY\_IP\_RANGES, LIST\_OF\_SUBNETWORKS). | `string` | `"ALL_SUBNETWORKS_ALL_IP_RANGES"` | no |
| <a name="input_config_timeouts"></a> [config\_timeouts](#input\_config\_timeouts) | Timeout configurations. | <pre>object({<br>    icmp            = number<br>    tcp_established = number<br>    tcp_transitory  = number<br>    udp             = number<br>  })</pre> | <pre>{<br>  "icmp": 30,<br>  "tcp_established": 1200,<br>  "tcp_transitory": 30,<br>  "udp": 30<br>}</pre> | no |
| <a name="input_logging_filter"></a> [logging\_filter](#input\_logging\_filter) | Enables logging if not null, value is one of 'ERRORS\_ONLY', 'TRANSLATIONS\_ONLY', 'ALL'. | `string` | `null` | no |
| <a name="input_name"></a> [name](#input\_name) | Name of the Cloud NAT resource. | `string` | n/a | yes |
| <a name="input_project_id"></a> [project\_id](#input\_project\_id) | Project where resources will be created. | `string` | n/a | yes |
| <a name="input_region"></a> [region](#input\_region) | Region where resources will be created. | `string` | n/a | yes |
| <a name="input_router_asn"></a> [router\_asn](#input\_router\_asn) | Router ASN used for auto-created router. | `number` | `64514` | no |
| <a name="input_router_create"></a> [router\_create](#input\_router\_create) | Create router. | `bool` | `true` | no |
| <a name="input_router_name"></a> [router\_name](#input\_router\_name) | Router name, leave blank if router will be created to use auto generated name. | `string` | `null` | no |
| <a name="input_router_network"></a> [router\_network](#input\_router\_network) | Name of the VPC used for auto-created router. | `string` | `null` | no |
| <a name="input_rules"></a> [rules](#input\_rules) | List of rules associated with this NAT. | <pre>list(object({<br>    description   = optional(string)<br>    match         = string<br>    source_ips    = optional(list(string))<br>    source_ranges = optional(list(string))<br>  }))</pre> | `[]` | no |
| <a name="input_subnetworks"></a> [subnetworks](#input\_subnetworks) | Subnetworks to NAT, only used when config\_source\_subnets equals LIST\_OF\_SUBNETWORKS. | <pre>list(object({<br>    self_link            = string,<br>    config_source_ranges = list(string)<br>    secondary_ranges     = list(string)<br>  }))</pre> | `[]` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_id"></a> [id](#output\_id) | Fully qualified NAT (router) id. |
| <a name="output_name"></a> [name](#output\_name) | Name of the Cloud NAT. |
| <a name="output_nat_ip_allocate_option"></a> [nat\_ip\_allocate\_option](#output\_nat\_ip\_allocate\_option) | NAT IP allocation mode. |
| <a name="output_region"></a> [region](#output\_region) | Cloud NAT region. |
| <a name="output_router"></a> [router](#output\_router) | Cloud NAT router resources (if auto created). |
| <a name="output_router_name"></a> [router\_name](#output\_router\_name) | Cloud NAT router name. |
<!-- END_TF_DOCS -->