---
title: "aaaDesired plantilla de estado del Administrador de recursos de configuración | Documentos de Microsoft"
description: "Definición de la plantilla de Resource Manager para la configuración de estado deseado en Azure con ejemplos y solución de problemas"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="cf7f3-103">VMSS de Windows y configuración de estado deseado con plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf7f3-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="cf7f3-104">Este artículo describe la plantilla de administrador de recursos de Hola para hello [controlador de extensión de configuración de estado deseado](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cf7f3-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="cf7f3-105">Ejemplo de plantilla para una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="cf7f3-105">Template example for a Windows VM</span></span>
<span data-ttu-id="cf7f3-106">Hello fragmento de código siguiente va en hello sección de recursos de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="cf7f3-107">Ejemplo de plantilla para VMSS de Windows</span><span class="sxs-lookup"><span data-stu-id="cf7f3-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="cf7f3-108">Un nodo VMSS tiene una sección "propiedades" con hello "VirtualMachineProfile", "extensionProfile" atributo.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="cf7f3-109">DSC se agrega en "extensions".</span><span class="sxs-lookup"><span data-stu-id="cf7f3-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="cf7f3-110">Información de configuración detallada</span><span class="sxs-lookup"><span data-stu-id="cf7f3-110">Detailed Settings Information</span></span>
<span data-ttu-id="cf7f3-111">Hola esquema siguiente es para la parte de la configuración de Hola de hello extensión de DSC de Azure en una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="cf7f3-112">Detalles</span><span class="sxs-lookup"><span data-stu-id="cf7f3-112">Details</span></span>
| <span data-ttu-id="cf7f3-113">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="cf7f3-113">Property Name</span></span> | <span data-ttu-id="cf7f3-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="cf7f3-114">Type</span></span> | <span data-ttu-id="cf7f3-115">Description</span><span class="sxs-lookup"><span data-stu-id="cf7f3-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf7f3-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="cf7f3-116">settings.wmfVersion</span></span> |<span data-ttu-id="cf7f3-117">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-117">string</span></span> |<span data-ttu-id="cf7f3-118">Especifica la versión de Hola de hello Windows Management Framework que debe instalarse en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="cf7f3-119">Establecer esta propiedad too'latest' instala Hola versión más actualizada de WMF.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="cf7f3-120">Hola, solo actual, valores posibles para esta propiedad son **'4.0', '5.0', ' 5.0PP' y 'última ' hora**.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="cf7f3-121">Estos valores posibles son tooupdates de asunto.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="cf7f3-122">valor predeterminado de Hello es 'última'.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="cf7f3-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="cf7f3-123">settings.configuration.url</span></span> |<span data-ttu-id="cf7f3-124">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-124">string</span></span> |<span data-ttu-id="cf7f3-125">Especifica el archivo zip de configuración de DSC de ubicación de dirección URL de Hola desde qué toodownload.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="cf7f3-126">Si la dirección URL de hello proporcionada requiere un token de SAS para el acceso, debe tooset hello protectedSettings.configurationUrlSasToken toohello valor de propiedad su token SAS.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="cf7f3-127">Esta propiedad es necesaria si se definen settings.configuration.script o settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="cf7f3-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="cf7f3-128">settings.configuration.script</span></span> |<span data-ttu-id="cf7f3-129">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-129">string</span></span> |<span data-ttu-id="cf7f3-130">Especifica el nombre de archivo de hello del script de Hola que contiene la definición de saludo de la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="cf7f3-131">Esta secuencia de comandos debe estar en la carpeta raíz de hello del archivo zip de hello descargado de dirección URL de hello especificada por la propiedad de configuration.url Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="cf7f3-132">Esta propiedad es necesaria si se definen settings.configuration.url o settings.configuration.script.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="cf7f3-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="cf7f3-133">settings.configuration.function</span></span> |<span data-ttu-id="cf7f3-134">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-134">string</span></span> |<span data-ttu-id="cf7f3-135">Especifica el nombre de saludo de la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="cf7f3-136">configuración de Hello denominada debe estar contenido en script de Hola definido por configuration.script.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="cf7f3-137">Esta propiedad es necesaria si se definen settings.configuration.url o settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="cf7f3-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="cf7f3-138">settings.configurationArguments</span></span> |<span data-ttu-id="cf7f3-139">Colección</span><span class="sxs-lookup"><span data-stu-id="cf7f3-139">Collection</span></span> |<span data-ttu-id="cf7f3-140">Define los parámetros que le gustaría toopass tooyour la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="cf7f3-141">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="cf7f3-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="cf7f3-142">settings.configurationData.url</span></span> |<span data-ttu-id="cf7f3-143">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-143">string</span></span> |<span data-ttu-id="cf7f3-144">Especifica la dirección de URL de Hola desde qué toodownload los datos de configuración (. psd1) de archivos toouse como entrada para la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="cf7f3-145">Si la dirección URL de hello proporcionada requiere un token de SAS para el acceso, debe tooset hello protectedSettings.configurationDataUrlSasToken toohello valor de propiedad su token SAS.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="cf7f3-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="cf7f3-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="cf7f3-147">string</span><span class="sxs-lookup"><span data-stu-id="cf7f3-147">string</span></span> |<span data-ttu-id="cf7f3-148">Habilita o deshabilita la recopilación de telemetría.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="cf7f3-149">Hello solo los valores posibles para esta propiedad son **'Enable', 'Disable', '', o $null**.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="cf7f3-150">Si se deja esta propiedad en blanco o como null, se habilita la telemetría.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="cf7f3-151">valor predeterminado de Hello es ''.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-151">hello default value is ''.</span></span> [<span data-ttu-id="cf7f3-152">Más información</span><span class="sxs-lookup"><span data-stu-id="cf7f3-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="cf7f3-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="cf7f3-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="cf7f3-154">Colección</span><span class="sxs-lookup"><span data-stu-id="cf7f3-154">Collection</span></span> |<span data-ttu-id="cf7f3-155">Define las ubicaciones alternativas que desde qué toodownload Hola WMF.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="cf7f3-156">Más información</span><span class="sxs-lookup"><span data-stu-id="cf7f3-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="cf7f3-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="cf7f3-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="cf7f3-158">Colección</span><span class="sxs-lookup"><span data-stu-id="cf7f3-158">Collection</span></span> |<span data-ttu-id="cf7f3-159">Define los parámetros que le gustaría toopass tooyour la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="cf7f3-160">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-160">This property is encrypted.</span></span> |
| <span data-ttu-id="cf7f3-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="cf7f3-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="cf7f3-162">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-162">string</span></span> |<span data-ttu-id="cf7f3-163">Especifica Hola SAS tooaccess token Hola dirección URL definida por configuration.url.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="cf7f3-164">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-164">This property is encrypted.</span></span> |
| <span data-ttu-id="cf7f3-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="cf7f3-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="cf7f3-166">cadena</span><span class="sxs-lookup"><span data-stu-id="cf7f3-166">string</span></span> |<span data-ttu-id="cf7f3-167">Especifica Hola SAS tooaccess token Hola dirección URL definida por configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="cf7f3-168">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="cf7f3-169">Settings frente a ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="cf7f3-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="cf7f3-170">Todas las configuraciones se guardan en un archivo de texto de configuración en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="cf7f3-171">Propiedades, en "configuración" son propiedades públicas porque no se cifran en el archivo de texto de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="cf7f3-172">Propiedades de 'protectedSettings' se cifran con un certificado y no se muestran en texto sin formato de este archivo en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="cf7f3-173">Si la configuración de hello necesita credenciales, pueden incluirse en protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="cf7f3-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="cf7f3-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cf7f3-174">Example</span></span>
<span data-ttu-id="cf7f3-175">Hello en el ejemplo siguiente se deriva de sección "Introducción" de Hola de hello [página información general sobre el controlador de extensión de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cf7f3-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="cf7f3-176">Este ejemplo utiliza plantillas de administrador de recursos en lugar de cmdlets toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="cf7f3-177">Guardar configuración de "IisInstall.ps1" Hola, colóquelo en una. COMPRIMIR archivos y cargue el archivo de hello en una dirección URL accesible.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="cf7f3-178">Este ejemplo utiliza el almacenamiento de blobs de Azure, pero es posible toodownload. Archivos ZIP desde cualquier ubicación arbitraria.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="cf7f3-179">En plantilla de Azure Resource Manager hello, hello código siguiente indica al archivo correcto de hello VM toodownload Hola y ejecuta la función de PowerShell adecuado de hello:</span><span class="sxs-lookup"><span data-stu-id="cf7f3-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="cf7f3-180">Actualizar desde Hola formato anterior</span><span class="sxs-lookup"><span data-stu-id="cf7f3-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="cf7f3-181">Cualquier opción de hello formato anterior (que contiene propiedades públicas de hello ModulesUrl, ConfigurationFunction, SasToken o propiedades) automáticamente adapta toohello actual formato y ejecuta tal y como lo hacían antes.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="cf7f3-182">Hola después de esquema es qué esquema de configuración anterior de hello tenía el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="cf7f3-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
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
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="cf7f3-183">Le mostramos cómo formato anterior de Hola adapta toohello actual formato:</span><span class="sxs-lookup"><span data-stu-id="cf7f3-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="cf7f3-184">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="cf7f3-184">Property Name</span></span> | <span data-ttu-id="cf7f3-185">Equivalente en el esquema anterior</span><span class="sxs-lookup"><span data-stu-id="cf7f3-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="cf7f3-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="cf7f3-186">settings.wmfVersion</span></span> |<span data-ttu-id="cf7f3-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="cf7f3-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="cf7f3-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="cf7f3-188">settings.configuration.url</span></span> |<span data-ttu-id="cf7f3-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="cf7f3-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="cf7f3-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="cf7f3-190">settings.configuration.script</span></span> |<span data-ttu-id="cf7f3-191">Primera parte de settings.ConfigurationFunction (antes de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="cf7f3-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="cf7f3-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="cf7f3-192">settings.configuration.function</span></span> |<span data-ttu-id="cf7f3-193">Segunda parte de settings.ConfigurationFunction (después de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="cf7f3-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="cf7f3-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="cf7f3-194">settings.configurationArguments</span></span> |<span data-ttu-id="cf7f3-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="cf7f3-195">settings.Properties</span></span> |
| <span data-ttu-id="cf7f3-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="cf7f3-196">settings.configurationData.url</span></span> |<span data-ttu-id="cf7f3-197">protectedSettings.DataBlobUri (sin token de SAS)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="cf7f3-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="cf7f3-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="cf7f3-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="cf7f3-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="cf7f3-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="cf7f3-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="cf7f3-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="cf7f3-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="cf7f3-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="cf7f3-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="cf7f3-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="cf7f3-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="cf7f3-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="cf7f3-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="cf7f3-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="cf7f3-205">settings.SasToken</span></span> |
| <span data-ttu-id="cf7f3-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="cf7f3-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="cf7f3-207">Token de SAS de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="cf7f3-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="cf7f3-208">Solución de problemas: código de error 1100</span><span class="sxs-lookup"><span data-stu-id="cf7f3-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="cf7f3-209">Código de error 1100 indica que hay un problema con hello extensión toohello DSC de intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="cf7f3-210">texto Hello de estos errores es variable y se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="cf7f3-211">Estas son algunas de los errores de hello con que puede encontrarse y cómo corregirlos.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="cf7f3-212">Valores no válidos</span><span class="sxs-lookup"><span data-stu-id="cf7f3-212">Invalid Values</span></span>
<span data-ttu-id="cf7f3-213">"Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="cf7f3-214">Hello solo los valores posibles son ","Habilitar"y"Deshabilitar"" "WmfVersion es '{0}'.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="cf7f3-215">Los únicos valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="cf7f3-215">Only possible values are …</span></span> <span data-ttu-id="cf7f3-216">y "latest".</span><span class="sxs-lookup"><span data-stu-id="cf7f3-216">and 'latest'"</span></span>

<span data-ttu-id="cf7f3-217">Problema: No se permite un valor proporcionado.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="cf7f3-218">Solución: Cambie el valor válido de tooa de valor no válido de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="cf7f3-219">Vea la tabla de hello en la sección de detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="cf7f3-220">Dirección URL no válida</span><span class="sxs-lookup"><span data-stu-id="cf7f3-220">Invalid URL</span></span>
<span data-ttu-id="cf7f3-221">"ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="cf7f3-222">This is not a valid URL" (ConfigurationData.url es '{0}'. No es una dirección URL válida) "DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="cf7f3-223">This is not a valid URL" (DataBlobUri es '{0}'. No es una dirección URL válida) "Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="cf7f3-224">This is not a valid URL" This is not a valid URL" (Configuration.url es '{0}'. No es una dirección URL válida)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-224">This is not a valid URL"</span></span>

<span data-ttu-id="cf7f3-225">Problema: Se ha proporcionado una dirección URL que no es válida.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="cf7f3-226">Solución: Compruebe todas las direcciones URL proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="cf7f3-227">Asegúrese de que todas las direcciones URL resolver las ubicaciones de toovalid que puede tener acceso extensión hello en el equipo remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="cf7f3-228">Tipo de ConfigurationArguments no válido</span><span class="sxs-lookup"><span data-stu-id="cf7f3-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="cf7f3-229">"Invalid configurationArguments type {0}" (Tipo de configurationArguments no válido {0})</span><span class="sxs-lookup"><span data-stu-id="cf7f3-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="cf7f3-230">Problema: Hola ConfigurationArguments propiedad no puede resolver tooa objeto de tabla hash.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="cf7f3-231">Solución: Convierta la propiedad ConfigurationArguments en Hashtable.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="cf7f3-232">Tener el formato de hello proporcionada en el ejemplo de Hola precedente.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="cf7f3-233">Esté atento a las comillas, comas y llaves.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="cf7f3-234">ConfigurationArguments duplicadas</span><span class="sxs-lookup"><span data-stu-id="cf7f3-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="cf7f3-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments" (Se encontraron argumentos duplicados '{0}' en propiedades configurationArguments públicas y privadas)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="cf7f3-236">Problema: Hola ConfigurationArguments en la configuración pública y ConfigurationArguments en configuración protegida hello contienen propiedades con hello mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="cf7f3-237">Solución: Quite una de las propiedades duplicadas Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="cf7f3-238">Propiedades que faltan</span><span class="sxs-lookup"><span data-stu-id="cf7f3-238">Missing Properties</span></span>
<span data-ttu-id="cf7f3-239">"Configuration.function requires that configuration.url or configuration.module is specified" (Configuration.function requiere que se especifiquen configuration.url o configuration.module)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="cf7f3-240">"Configuration.url requires that configuration.script is specified" (Configuration.url requiere que se especifique configuration.script)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="cf7f3-241">"Configuration.script requires that configuration.url is specified" (Configuration.script requiere que se especifique configuration.url)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="cf7f3-242">"Configuration.url requires that configuration.function is specified" (Configuration.url requiere que se especifique configuration.function)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="cf7f3-243">"ConfigurationUrlSasToken requires that configuration.url is specified" (ConfigurationUrlSasToken requiere que se especifique configuration.url)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="cf7f3-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified" (ConfigurationDataUrlSasToken requiere que se especifique configurationData.url)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="cf7f3-245">Problema: Una propiedad definida requiere otra propiedad que falta.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="cf7f3-246">Soluciones:</span><span class="sxs-lookup"><span data-stu-id="cf7f3-246">Solutions:</span></span> 

* <span data-ttu-id="cf7f3-247">Proporcionar falta la propiedad Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-247">Provide hello missing property.</span></span>
* <span data-ttu-id="cf7f3-248">Quite la propiedad de Hola que necesita la propiedad que falta Hola.</span><span class="sxs-lookup"><span data-stu-id="cf7f3-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf7f3-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf7f3-249">Next Steps</span></span>
<span data-ttu-id="cf7f3-250">Obtenga información sobre DSC y escalas de máquina virtual se establece [usar escala conjuntos de máquina Virtual con hello extensión de DSC de Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="cf7f3-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="cf7f3-251">Puede encontrar más información en el artículo sobre [administración segura de credenciales de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cf7f3-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="cf7f3-252">Para obtener más información sobre el controlador de extensión de DSC de Azure de hello, consulte [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cf7f3-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="cf7f3-253">Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="cf7f3-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

