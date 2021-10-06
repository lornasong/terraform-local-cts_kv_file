# Local Text File Module monitoring Consul KV for Consul Terraform Sync

This Terraform module creates local text files. Using this module in automation with [Consul Terraform Sync (CTS)](https://www.consul.io/docs/nia) will dynamically create or delete text files based off of configured services. This module is useful for testing CTS to observe how it responds to changes in Consul catalog.

## Feature

The module uses the `local` Terraform provider to create text files. A directory "resources" is created in the CTS generated task subdirectory. The text files are named after the monitored Consul service instances.

## Requirements

### Ecosystem Requirements

| Ecosystem | Version |
|-----------|---------|
| [consul](https://www.consul.io/downloads) | >= 1.8 |
| [consul-terraform-sync](https://www.consul.io/docs/nia) | >= 0.4.0 |
| [terraform](https://www.terraform.io) | >= 0.13 |

### Terraform Providers

| Name | Version |
|------|---------|
| local | >= 2.0.0 |

## Setup

No setup is needed

## Usage

**User Config for Consul Terraform Sync**

See [Securely Configure Terraform Providers](https://www.consul.io/docs/nia/configuration#securely-configure-terraform-providers) for alternatives to directly inserting token in config file.

example.hcl
```hcl
task {
  name           = "task_example"
  services       = ["api"]
  version        = "0.0.1"
  source         = "lornasong/cts_kv_file/local"
  condition "consul-kv" {
		  path = "key"
  		source_includes_var = true
	  	recurse = true
	 }
}
```
