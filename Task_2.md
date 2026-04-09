# Question

The Nautilus DevOps team is presently immersed in data migrations, transferring data from on-premise storage systems to Azure Blob containers. They have recently received some data that they intend to copy to one of the Blob containers.
A Blob container named datacenter-blob-17398 already exists in the eastus region under the storage account datacenterst26969. Copy the file /tmp/datacenter.txt to the Blob container datacenter-blob-17398.

# Solution

```
~ ➜  cd /tmp

/tmp ➜  ls
access_keys
datacenter.txt
systemd-private-14ca4d8d779d45b68a682adbd7a58c43-systemd-logind.service-dh85uj

/tmp ➜  az storage account list
[
  {
    "accessTier": "Hot",
    "accountMigrationInProgress": null,
    "allowBlobPublicAccess": false,
    "allowCrossTenantReplication": false,
    "allowSharedKeyAccess": null,
    "allowedCopyScope": null,
    "azureFilesIdentityBasedAuthentication": null,
    "blobRestoreStatus": null,
    "creationTime": "2026-04-07T09:44:21.841272+00:00",
    "customDomain": null,
    "defaultToOAuthAuthentication": null,
    "dnsEndpointType": null,
    "enableExtendedGroups": null,
    "enableHttpsTrafficOnly": true,
    "enableNfsV3": null,
    "encryption": {
      "encryptionIdentity": null,
      "keySource": "Microsoft.Storage",
      "keyVaultProperties": null,
      "requireInfrastructureEncryption": null,
      "services": {
        "blob": {
          "enabled": true,
          "keyType": "Account",
          "lastEnabledTime": "2026-04-07T09:44:22.283239+00:00"
        },
        "file": {
          "enabled": true,
          "keyType": "Account",
          "lastEnabledTime": "2026-04-07T09:44:22.283239+00:00"
        },
        "queue": null,
        "table": null
      }
    },
    "extendedLocation": null,
    "failoverInProgress": null,
    "geoReplicationStats": null,
    "id": "/subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-caca5f7490b34683/providers/Microsoft.Storage/storageAccounts/datacenterst26969",
    "identity": null,
    "immutableStorageWithVersioning": null,
    "isHnsEnabled": null,
    "isLocalUserEnabled": null,
    "isSftpEnabled": null,
    "isSkuConversionBlocked": null,
    "keyCreationTime": {
      "key1": "2026-04-07T09:44:22.275096+00:00",
      "key2": "2026-04-07T09:44:22.275096+00:00"
    },
    "keyPolicy": null,
    "kind": "StorageV2",
    "largeFileSharesState": null,
    "lastGeoFailoverTime": null,
    "location": "eastus",
    "minimumTlsVersion": "TLS1_0",
    "name": "datacenterst26969",
    "networkRuleSet": {
      "bypass": "AzureServices",
      "defaultAction": "Allow",
      "ipRules": [],
      "ipv6Rules": [],
      "resourceAccessRules": null,
      "virtualNetworkRules": []
    },
    "primaryEndpoints": {
      "blob": "https://datacenterst26969.blob.core.windows.net/",
      "dfs": "https://datacenterst26969.dfs.core.windows.net/",
      "file": "https://datacenterst26969.file.core.windows.net/",
      "internetEndpoints": null,
      "microsoftEndpoints": null,
      "queue": "https://datacenterst26969.queue.core.windows.net/",
      "table": "https://datacenterst26969.table.core.windows.net/",
      "web": "https://datacenterst26969.z13.web.core.windows.net/"
    },
    "primaryLocation": "eastus",
    "privateEndpointConnections": [],
    "provisioningState": "Succeeded",
    "publicNetworkAccess": null,
    "resourceGroup": "kml_rg_main-caca5f7490b34683",
    "routingPreference": null,
    "sasPolicy": null,
    "secondaryEndpoints": null,
    "secondaryLocation": null,
    "sku": {
      "name": "Standard_LRS",
      "tier": "Standard"
    },
    "statusOfPrimary": "available",
    "statusOfSecondary": null,
    "storageAccountSkuConversionStatus": null,
    "tags": {},
    "type": "Microsoft.Storage/storageAccounts"
  }
]

/tmp ➜  az storage account list | grep name 
    "name": "datacenterst26969",
      "name": "Standard_LRS",

/tmp ➜  az storage blob upload --account-name datacenterst26969 -c datacenter-blob-17398 -f /tmp/datacenter.txt

There are no credentials provided in your command and environment, we will query for account key for your storage account.
It is recommended to provide --connection-string, --account-key or --sas-token in your command as credentials.

You also can add `--auth-mode login` in your command to use Azure Active Directory (Azure AD) for authorization if your login account is assigned required RBAC roles.
For more information about RBAC roles in storage, visit https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-cli.

In addition, setting the corresponding environment variables can avoid inputting credentials in your command. Please use --help to get more information about environment variable usage.
Alive[################################################################] Finished[#############################################################]  100.0000%
{
  "client_request_id": "ec235a90-3267-11f1-ba84-0ab6af73c635",
  "content_md5": "Lu7zilatbGguzSz2Ecn5IQ==",
  "date": "2026-04-07T09:55:35+00:00",
  "encryption_key_sha256": null,
  "encryption_scope": null,
  "etag": "\"0x8DE948BD0A947A3\"",
  "lastModified": "2026-04-07T09:55:35+00:00",
  "request_id": "6a915b34-701e-0020-0974-c6e5e8000000",
  "request_server_encrypted": true,
  "version": "2022-11-02",
  "version_id": null
}

/tmp ➜

```
