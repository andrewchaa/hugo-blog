---
title: "Provision Azure Storage with Terraform"
date: 2020-11-15T19:45:09Z
draft: false
---
# Provision Azure Storage with Terraform

I need to store all the domain / integration events as json blob on the storage. This is the terraform script to provision the storage account for it.

```bash
resource "azurerm_resource_group" "events_rg" {
  name     = "${var.organisation}-${var.system}-${var.environment}-events-${var.location}"
  location = var.location
  tags     = var.tags
}

resource "azurerm_storage_account" "events_ac" {
  name                     = lower("${var.environment}events")
  resource_group_name      = azurerm_resource_group.events_rg.name
  location                 = var.location
  account_tier             = "Standard"
  account_replication_type = "GRS"
}

resource "azurerm_storage_container" "events_container" {
  name                  = "events"
  storage_account_name  = azurerm_storage_account.events_ac.name
  container_access_type = "private"
}

output "storage_blob_endpoint" {
  value       = "${azurerm_storage_account.events_ac.primary_blob_endpoint}"
  description = "blob_endpoint"
}

output "storage_blob_connection_string" {
  value       = "${azurerm_storage_account.events_ac.primary_blob_connection_string}"
  sensitive   = false
  description = "connection string"
}

```

