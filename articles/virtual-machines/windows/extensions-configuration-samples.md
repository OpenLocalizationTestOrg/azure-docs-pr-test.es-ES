---
title: "Ejemplo de configuración para extensiones de máquina virtual Windows | Microsoft Docs"
description: "Configuración de ejemplo para crear plantillas con extensiones"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a1cee6c-51ea-4c03-b607-f158586d7175
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: a22962690854d273377f7295ab5dd49419f5a354
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-windows-vm-extension-configuration-samples"></a>Ejemplos de configuración de la extensión de máquina virtual de Windows de Azure.
> [!div class="op_single_selector"]
> * [PowerShell: plantilla](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [CLI: plantilla](../linux/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Este artículo proporciona un ejemplo de configuración para configurar las extensiones de máquina virtual de Azure para máquinas virtuales Windows.

Para más información sobre estas extensiones, consulte [Introducción a las extensiones de máquina virtual de Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para más información sobre la creación de plantillas de extensión, consulte [Creación de plantillas de extensión.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

En este artículo se indican los valores de configuración esperados para algunas de las extensiones de Windows.

## <a name="sample-template-snippet-for-vm-extensions-with-iaas-vms"></a>Fragmento de plantilla de ejemplo para extensiones de VM con máquinas virtuales IaaS.
El fragmento de plantilla para extensiones de implementación tiene el aspecto siguiente:

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a>Fragmento de plantilla de ejemplo para extensiones de VM con conjuntos de escalado de VM.
    {
     "type":"Microsoft.Compute/virtualMachineScaleSets",
    ....
           "extensionProfile":{
           "extensions":[
             {
               "name":"extension Name",
               "properties":{
                 "publisher":"Publisher Namespace",
                 "type":"extension Name",
                 "typeHandlerVersion":"extension version",
                 "autoUpgradeMinorVersion":true,
                 "settings":{
                 // Extension specific configuration goes in here.
                 }
               }
              }
            }
          }

Antes de implementar la extensión, compruebe la versión más reciente de la extensión y reemplace la "typeHandlerVersion" por la versión más reciente actual.

El resto del artículo proporciona ejemplos de configuraciones para las extensiones de máquina virtual de Windows.

Antes de implementar la extensión, compruebe la versión más reciente de la extensión y reemplace la "typeHandlerVersion" por la versión más reciente actual.

### <a name="customscript-extension-14"></a>Extensión CustomScript 1.4.
      {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.4",
          "settings": {
              "fileUris": [
                  "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
              ],
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
          },
          "protectedSettings": {
            "storageAccountName": "yourStorageAccountName",
            "storageAccountKey": "yourStorageAccountKey"
          }
      }

#### <a name="parameter-description"></a>Descripción del parámetro:
* fileUris: lista separada por comas de direcciones URL de los archivos que se descargarán en la máquina virtual por la Extensión. No se descargan los archivos si no se especifica nada. Si los archivos están en Almacenamiento de Azure, fileURLs puede marcarse como privado y los correspondientes storageAccountName y storageAccountKey se pueden pasar como parámetros privados para tener acceso a estos archivos.
* commandToExecute: [parámetro obligatorio]: este es el comando que se ejecutará por la Extensión.
* storageAccountName: [parámetro opcional]: nombre de la cuenta de almacenamiento para tener acceso a fileURLs si están marcados como privados.
* storageAccountKey: [parámetro opcional]: clave de cuenta de almacenamiento para tener acceso a fileURLs, si están marcados como privados.

### <a name="customscript-extension-17"></a>Extensión CustomScript 1.7.
Consulte la versión 1.4 de CustomScript para ver la descripción del parámetro. La versión 1.7 admite el envío de parámetros de script (commandToExecute) como protectedSettings, en cuyo caso se cifrará antes del envío. Puede especificarse el parámetro 'commandToExecute' en la configuración o protectedSettings, pero no en ambos.

        {
            "publisher": "Microsoft.Compute",
            "type": "CustomScriptExtension",
            "typeHandlerVersion": "1.7",
            "settings": {
                "fileUris": [
                    "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
                ],
                "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
            },
            "protectedSettings": {
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1",
              "storageAccountName": "yourStorageAccountName",
              "storageAccountKey": "yourStorageAccountKey"
            }
        }

### <a name="vmaccess-extension"></a>Extensión VMAccess.
      {
          "publisher": "Microsoft.Compute",
          "type": "VMAccessAgent",
          "typeHandlerVersion": "2.0",
          "settings": {
            "UserName" : "New User Name"
          },
          "protectedSettings": {
            "Password" : "New Password"
          }
      }

### <a name="dsc-extension"></a>Extensión DSC.
      {
          "publisher": "Microsoft.Powershell",
          "type": "DSC",
          "typeHandlerVersion": "2.1(Recommendation is to use the latest version)",
          "settings": {
              "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
              "SasToken": "Optional : SAS Token if ModulesUrl points to Azure Blob Storage",
              "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
              "Properties": {
                  "ParameterToConfigurationFunction1": "Value1",
                  "ParameterToConfigurationFunction2": "Value2",
                  "ParameterOfTypePSCredential1": {
                      "UserName": "UsernameValue1",
                      "Password": "PrivateSettingsRef:Key1(Value is a reference to a member of the Items object in the protected settings)"
                  },
                  "ParameterOfTypePSCredential2": {
                      "UserName": "UsernameValue2",
                      "Password": "PrivateSettingsRef:Key2"
                  }
              }
          },
          "protectedSettings": {
              "Items": {
                  "Key1": "PasswordValue1",
                  "Key2": "PasswordValue2"
              },
              "DataBlobUri": "optional : https: //UrlToConfigurationData.psd1"
          }
      }


### <a name="symantec-endpoint-protection"></a>Symantec Endpoint Protection.
      {
        "publisher": "SymantecEndpointProtection",
        "type": "Symantec",
        "typeHandlerVersion": "12.1",
        "settings": {}
      }

### <a name="trend-micro-deep-security-agent"></a>Trend Micro Deep Security Agent.
      {
        "publisher": "TrendMicro.DeepSecurity",
        "type": "TrendMicroDSA",
        "typeHandlerVersion": "9.6",
        "settings": {
          "ManagerAddress" : "Enter the externally accessible DNS name or IP address of the Deep Security Manager. Please enter \"agents.deepsecurity.trendmicro.com\" if using Deep Security as a Service",

          "ActivationPort" : "Enter the port number of the Deep Security Manager, default value - 443",

          "TenantIdentifier" : "Enter the tenant ID, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "TenantActivationPassword" : "Enter the tenant activation password, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "SecurityPolicy" : "Optional : Enter the name or numeric ID of the security policy defined in the Deep Security Manager which will be applied on agent activation to protect this virtual machine (recommended). No security policy will be applied to the virtual machine if this parameter is blank. This parameter is optional if using Deep Security as a Service."
        }
      }

### <a name="vormertric-transparent-encryption-agent"></a>Vormertric Transparent Encryption Agent.
            {
              "publisher": "Vormetric",
              "type": "VormetricTransparentEncryptionAgent",
              "typeHandlerVersion": "5.2",
              "settings": {
              }
            }

### <a name="puppet-enterprise-agent"></a>Puppet Enterprise Agent.
            {
              "publisher": "PuppetLabs",
              "type": "PuppetEnterpriseAgent",
              "typeHandlerVersion": "3.2",
              "settings": {
                "puppet_master_server" : "Puppet Master Server Name"
              }
            }  

### <a name="microsoft-monitoring-agent-for-azure-operational-insights"></a>Microsoft Monitoring Agent para Azure Operational Insights
            {
              "publisher": "Microsoft.EnterpriseCloud.Monitoring",
              "type": "MicrosoftMonitoringAgent",
              "typeHandlerVersion": "1.0",
              "settings": {
                "workspaceId" : "The Workspace ID is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              "protectedSettings": {
                "workspaceKey"  : "The Workspace Key is a string that is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              }
            }

### <a name="mcafee-endpointsecurity"></a>McAfee EndpointSecurity
            {
              "publisher": "McAfee.EndpointSecurity",
              "type": "McAfeeEndpointSecurity",
              "typeHandlerVersion": "6.0",
              "settings": {
                "entitlementKey" : "Optional : Enter a valid entitlement key or leave blank for trial version",
                "featureVS"      : "Choose whether or not to install the Virus and Spyware Protection features : true|false",
                "featureBP"      : "Choose whether or not to install the Browser Protection feature : true|false",
                "featureFW"      : "Choose whether or not to install the Firewall Protection feature :true|false",
                "relayServer"    : "Allows VMs on the local subnet to receive updates through this VM when they are not connected to the internet : true|false"
              }
            }

### <a name="azure-iaas-antimalware"></a>Azure IaaS Antimalware
          {
            "publisher": "Microsoft.Azure.Security",
            "type": "IaaSAntimalware",
            "typeHandlerVersion": "1.2",
            "settings": {
              "AntimalwareEnabled": "true",
              "ExclusionsPaths"        : "Optional : ExclusionsPaths",
              "ExclusionsExtensions"   : "Optional : ExclusionsExtensions",
              "ExclusionsProcesses"   : "Optional : ExclusionsProcesses",
              "RealtimeProtectionEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsIsEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsScanType"   : "Optional : Quick|Full",
              "ScheduledScanSettingsDay"   : "Optional : Sunday-Saturday",
              "ScheduledScanSettingsTime"   : "Optional : When to perform the scheduled scan, measured in minutes from midnight,0-1440"
            }
          }

### <a name="eset-file-security"></a>ESET File Security
          {
            "publisher": "ESET",
            "type": "FileSecurity",
            "typeHandlerVersion": "6.0",
            "settings": {
            }
          }

### <a name="datadog-agent"></a>Agente de Datadog
          {
            "publisher": "Datadog.Agent",
            "type": "DatadogWindowsAgent",
            "typeHandlerVersion": "0.5",
            "settings": {
              "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
            }
          }

### <a name="confer-advanced-threat-prevention-and-incident-response-for-azure"></a>Confer Advanced Threat Prevention y Incident Response para Azure
          {
            "publisher": "Confer",
            "type": "ConferForAzure",
            "typeHandlerVersion": "1.0",
            "settings": {
              "ConferRegisterCode" : "Optional : Valid product registration code or leave it blank to register later",
              "ConferRegisterCode" : "Enter a valid server name if your account requires a dedicated confer backend server or leave it blank"
            }
          }

### <a name="cloudlink-securevm-agent"></a>Agente de SecureVM de CloudLink
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMWindowsAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN to CloudLinkCenter"
            }
          }

### <a name="barracuda-vpn-connectivity-agent-for-microsoft-azure"></a>Barracuda VPN Connectivity Agent para Microsoft Azure
          {
            "publisher": "Barracuda.Azure.ConnectivityAgent",
            "type": "BarracudaConnectivityAgent",
            "typeHandlerVersion": "3.5",
            "settings": {
              "ServerAddress" : "Host name or IP address of the VPN server - AES, AES256, Blowfish,CAST,DES,3DES,None",
              "EncryptionAlgorithm" : "Algorithm used to encrypt VPN traffic - MD5,SHA1,SHA256,None",
              "PKCS12File" : "Url for file containing certificate and private key used to authenticate against the VPN server",
              "PKCS12FilePassword" : "Password for the file containing certificate and private key"
            }
          }

### <a name="alert-logic-log-manager"></a>Alert Logic Log Manager
          {
            "publisher": "AlertLogic.Extension",
            "type": "AlertLogicLM",
            "typeHandlerVersion": "1.9",
            "settings": {
              "registrationKey" : " Alert Logic Log Manager registration key"
            }
          }

### <a name="chef-agent"></a>Chef Agent
          {
            "publisher": "Chef.Bootstrap.WindowsAzure",
            "type": "ChefClient",
            "typeHandlerVersion": "1210.12",
            "settings": {
              "validation_key" : " Validation key",
              "client_rb" : "client_rb file",
              "runlist" : "Optional runlist"
            }
          }

### <a name="azure-diagnostics"></a>Diagnóstico de Azure
Para más información sobre cómo configurar los diagnósticos, consulte [Extensión de Diagnósticos de Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

          {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(variables('wadcfgx'))]",
              "storageAccount": "[parameters('diagnosticsStorageAccount')]"
            },
            "protectedSettings": {
            "storageAccountName": "[parameters('diagnosticsStorageAccount')]",
            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
            "storageAccountEndPoint": "https://core.windows.net"
          }
          }

### <a name="octopus-deploy-tentacle-agent"></a>Agente Tentacle de Octopus Deploy

Para más información sobre cómo configurar Tentacle de Octopus Deploy en Azure, consulte la [documentación de Octopus](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).

          {
            "publisher": "OctopusDeploy.Tentacle",
            "type": "OctopusDeployWindowsTentacle",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": "true",
            "settings": {
              "OctopusServerUrl": "(string, required) The url to the Octopus server portal.",
              "Environments": [ "(array of strings, required) The environments to which the Tentacle should be added." ],
              "Roles": [ "(array of strings, required) The roles to assign to the Tentacle." ],
              "CommunicationMode": "(string, required) Whether the Tentacle should wait for connections from the server ('Listen') or should poll the server ('Poll').",
              "Port": (int, required) The port to listen on for connections from the server (in 'Listen' mode), or the port on which to connect to the Octopus server ('Poll' mode).,
              "PublicHostNameConfiguration": "(string, optional) If in listening mode, how the server should contact the Tentacle. Can be 'PublicIP', 'FQDN', 'ComputerName' or 'Custom'. Defaults to 'PublicIp'.",
              "CustomPublicHostName": "(string, optional) If in listening mode, and 'PublicHostNameConfiguration' is set to 'Custom', the address that the server should use for this Tentacle.",
              "MachinePolicy": "(string, optional) The Machine Policy to assign to the Tentacle. If not specified, uses the default Machine Policy.",
              "Tenants": [ "(array of strings, optional) The tenants to assign to the Tentacle. The tenants feature must be enabled on the Octopus Server." ],
              "TenantTags": [ "(array of strings, optional) The tenant tags to assign to the Tentacle, in the format 'TagSet/TagName'. The tenants feature must be enabled on the Octopus Server." ]
            },
            "protectedSettings": {
              "ApiKey": "(string, required) The Api Key to use to connect to the Octopus server."
            }
          }

En los ejemplos anteriores, reemplace el número de versión por el número de versión más reciente.

Este es un ejemplo de una plantilla de máquina virtual completa con la extensión de script personalizada.

[Extensión de script personalizada en una máquina virtual de Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

