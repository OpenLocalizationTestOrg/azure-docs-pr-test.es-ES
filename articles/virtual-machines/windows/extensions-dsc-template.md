---
title: "Configuración del estado deseado con una plantilla de Resource Manager| Microsoft Docs"
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="3a149-103">VMSS de Windows y configuración de estado deseado con plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a149-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="3a149-104">En este artículo, se describe la plantilla de Resource Manager para el [controlador de extensiones de configuración de estado deseado](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a149-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="3a149-105">Ejemplo de plantilla para una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="3a149-105">Template example for a Windows VM</span></span>
<span data-ttu-id="3a149-106">El siguiente fragmento corresponde a la sección Resource de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="3a149-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="3a149-107">Ejemplo de plantilla para VMSS de Windows</span><span class="sxs-lookup"><span data-stu-id="3a149-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="3a149-108">Un nodo de VMSS tiene una sección "properties" con el atributo "extensionProfile" de "VirtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="3a149-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="3a149-109">DSC se agrega en "extensions".</span><span class="sxs-lookup"><span data-stu-id="3a149-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="3a149-110">Información de configuración detallada</span><span class="sxs-lookup"><span data-stu-id="3a149-110">Detailed Settings Information</span></span>
<span data-ttu-id="3a149-111">Este es el esquema para la parte de configuración (settings) de la extensión DSC de Azure en una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a149-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="3a149-112">Detalles</span><span class="sxs-lookup"><span data-stu-id="3a149-112">Details</span></span>
| <span data-ttu-id="3a149-113">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="3a149-113">Property Name</span></span> | <span data-ttu-id="3a149-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="3a149-114">Type</span></span> | <span data-ttu-id="3a149-115">Description</span><span class="sxs-lookup"><span data-stu-id="3a149-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a149-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="3a149-116">settings.wmfVersion</span></span> |<span data-ttu-id="3a149-117">string</span><span class="sxs-lookup"><span data-stu-id="3a149-117">string</span></span> |<span data-ttu-id="3a149-118">Especifica la versión de Windows Management Framework que debe instalarse en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a149-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="3a149-119">Si se establece esta propiedad en "latest", se instala la versión más reciente de WMF.</span><span class="sxs-lookup"><span data-stu-id="3a149-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="3a149-120">Los únicos valores posibles actuales para esta propiedad son **"4.0", "5.0", "5.0PP" y "latest"**.</span><span class="sxs-lookup"><span data-stu-id="3a149-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="3a149-121">Estos valores posibles están sujetos a actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="3a149-121">These possible values are subject to updates.</span></span> <span data-ttu-id="3a149-122">El valor predeterminado es "latest".</span><span class="sxs-lookup"><span data-stu-id="3a149-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="3a149-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="3a149-123">settings.configuration.url</span></span> |<span data-ttu-id="3a149-124">string</span><span class="sxs-lookup"><span data-stu-id="3a149-124">string</span></span> |<span data-ttu-id="3a149-125">Especifica la ubicación de la dirección URL desde la que descargar el archivo zip de la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="3a149-126">Si la dirección URL proporcionada requiere un token de SAS para el acceso, debe establecer la propiedad protectedSettings.configurationUrlSasToken en el valor de su token de SAS.</span><span class="sxs-lookup"><span data-stu-id="3a149-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="3a149-127">Esta propiedad es necesaria si se definen settings.configuration.script o settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="3a149-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="3a149-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="3a149-128">settings.configuration.script</span></span> |<span data-ttu-id="3a149-129">string</span><span class="sxs-lookup"><span data-stu-id="3a149-129">string</span></span> |<span data-ttu-id="3a149-130">Especifica el nombre de archivo del script que contiene la definición de la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="3a149-131">Este script debe estar en la carpeta raíz del archivo zip descargado de la dirección URL especificada en la propiedad configuration.url.</span><span class="sxs-lookup"><span data-stu-id="3a149-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="3a149-132">Esta propiedad es necesaria si se definen settings.configuration.url o settings.configuration.script.</span><span class="sxs-lookup"><span data-stu-id="3a149-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="3a149-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="3a149-133">settings.configuration.function</span></span> |<span data-ttu-id="3a149-134">string</span><span class="sxs-lookup"><span data-stu-id="3a149-134">string</span></span> |<span data-ttu-id="3a149-135">Especifica el nombre de la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="3a149-136">La configuración con nombre debe incluirse en el script definido en configuration.script.</span><span class="sxs-lookup"><span data-stu-id="3a149-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="3a149-137">Esta propiedad es necesaria si se definen settings.configuration.url o settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="3a149-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="3a149-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3a149-138">settings.configurationArguments</span></span> |<span data-ttu-id="3a149-139">Colección</span><span class="sxs-lookup"><span data-stu-id="3a149-139">Collection</span></span> |<span data-ttu-id="3a149-140">Define los parámetros que desea pasar a la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="3a149-141">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="3a149-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="3a149-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="3a149-142">settings.configurationData.url</span></span> |<span data-ttu-id="3a149-143">string</span><span class="sxs-lookup"><span data-stu-id="3a149-143">string</span></span> |<span data-ttu-id="3a149-144">Especifica la dirección URL desde la que descargar el archivo de datos de configuración (.psd1) que se usará como entrada para la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="3a149-145">Si la dirección URL proporcionada requiere un token de SAS para el acceso, debe establecer la propiedad protectedSettings.configurationDataUrlSasToken en el valor de su token de SAS.</span><span class="sxs-lookup"><span data-stu-id="3a149-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="3a149-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="3a149-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="3a149-147">string</span><span class="sxs-lookup"><span data-stu-id="3a149-147">string</span></span> |<span data-ttu-id="3a149-148">Habilita o deshabilita la recopilación de telemetría.</span><span class="sxs-lookup"><span data-stu-id="3a149-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="3a149-149">Los únicos valores posibles para esta propiedad son **"Enable", "Disable", '' o $null**.</span><span class="sxs-lookup"><span data-stu-id="3a149-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="3a149-150">Si se deja esta propiedad en blanco o como null, se habilita la telemetría.</span><span class="sxs-lookup"><span data-stu-id="3a149-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="3a149-151">El valor predeterminado es ".</span><span class="sxs-lookup"><span data-stu-id="3a149-151">The default value is ''.</span></span> [<span data-ttu-id="3a149-152">Más información</span><span class="sxs-lookup"><span data-stu-id="3a149-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="3a149-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="3a149-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="3a149-154">Colección</span><span class="sxs-lookup"><span data-stu-id="3a149-154">Collection</span></span> |<span data-ttu-id="3a149-155">Define las ubicaciones alternativas desde las que descargar WMF.</span><span class="sxs-lookup"><span data-stu-id="3a149-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="3a149-156">Más información</span><span class="sxs-lookup"><span data-stu-id="3a149-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="3a149-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3a149-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="3a149-158">Colección</span><span class="sxs-lookup"><span data-stu-id="3a149-158">Collection</span></span> |<span data-ttu-id="3a149-159">Define los parámetros que desea pasar a la configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="3a149-160">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="3a149-160">This property is encrypted.</span></span> |
| <span data-ttu-id="3a149-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3a149-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="3a149-162">string</span><span class="sxs-lookup"><span data-stu-id="3a149-162">string</span></span> |<span data-ttu-id="3a149-163">Especifica el token de SAS para acceder a la dirección URL definida en configuration.url.</span><span class="sxs-lookup"><span data-stu-id="3a149-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="3a149-164">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="3a149-164">This property is encrypted.</span></span> |
| <span data-ttu-id="3a149-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3a149-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="3a149-166">string</span><span class="sxs-lookup"><span data-stu-id="3a149-166">string</span></span> |<span data-ttu-id="3a149-167">Especifica el token de SAS para acceder a la dirección URL definida en configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="3a149-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="3a149-168">Esta propiedad no está cifrada.</span><span class="sxs-lookup"><span data-stu-id="3a149-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="3a149-169">Settings frente a ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="3a149-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="3a149-170">Todas las configuraciones se guardan en un archivo de texto de configuración en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a149-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="3a149-171">Las propiedades en "settings" son públicas porque no están cifradas en el archivo de texto de configuración.</span><span class="sxs-lookup"><span data-stu-id="3a149-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="3a149-172">Las propiedades en "protectedSettings" se cifran con un certificado y no se muestran en texto sin formato en este archivo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a149-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="3a149-173">Si la configuración necesita credenciales, pueden incluirse en protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="3a149-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="3a149-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3a149-174">Example</span></span>
<span data-ttu-id="3a149-175">El ejemplo siguiente se deriva de la sección "Introducción" de la [página de introducción al controlador de extensiones DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a149-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="3a149-176">Este ejemplo usa plantillas de Resource Manager en lugar de cmdlets para implementar la extensión.</span><span class="sxs-lookup"><span data-stu-id="3a149-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="3a149-177">Guardar la configuración "IisInstall.ps1", colóquela en un archivo .ZIP y cargue el archivo en una dirección URL accesible.</span><span class="sxs-lookup"><span data-stu-id="3a149-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="3a149-178">Este ejemplo usa el almacenamiento de blobs de Azure, pero es posible descargar archivos .ZIP desde cualquier ubicación.</span><span class="sxs-lookup"><span data-stu-id="3a149-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="3a149-179">En la plantilla de Azure Resource Manager, el siguiente código indica a la máquina virtual que descargue el archivo correcto y ejecute la función de PowerShell adecuada:</span><span class="sxs-lookup"><span data-stu-id="3a149-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="3a149-180">Actualización del formato anterior</span><span class="sxs-lookup"><span data-stu-id="3a149-180">Updating from the Previous Format</span></span>
<span data-ttu-id="3a149-181">Cualquier configuración en el formato anterior (que contiene las propiedades públicas ModulesUrl, ConfigurationFunction, SasToken o Properties) se adaptará automáticamente al formato actual y se ejecutará tal como lo hacía antes.</span><span class="sxs-lookup"><span data-stu-id="3a149-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="3a149-182">El esquema de configuración anterior tenía un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a149-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="3a149-183">Así se adapta el formato anterior al actual:</span><span class="sxs-lookup"><span data-stu-id="3a149-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="3a149-184">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="3a149-184">Property Name</span></span> | <span data-ttu-id="3a149-185">Equivalente en el esquema anterior</span><span class="sxs-lookup"><span data-stu-id="3a149-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="3a149-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="3a149-186">settings.wmfVersion</span></span> |<span data-ttu-id="3a149-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="3a149-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="3a149-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="3a149-188">settings.configuration.url</span></span> |<span data-ttu-id="3a149-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="3a149-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="3a149-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="3a149-190">settings.configuration.script</span></span> |<span data-ttu-id="3a149-191">Primera parte de settings.ConfigurationFunction (antes de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="3a149-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="3a149-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="3a149-192">settings.configuration.function</span></span> |<span data-ttu-id="3a149-193">Segunda parte de settings.ConfigurationFunction (después de '\\\\')</span><span class="sxs-lookup"><span data-stu-id="3a149-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="3a149-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3a149-194">settings.configurationArguments</span></span> |<span data-ttu-id="3a149-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="3a149-195">settings.Properties</span></span> |
| <span data-ttu-id="3a149-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="3a149-196">settings.configurationData.url</span></span> |<span data-ttu-id="3a149-197">protectedSettings.DataBlobUri (sin token de SAS)</span><span class="sxs-lookup"><span data-stu-id="3a149-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="3a149-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="3a149-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="3a149-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="3a149-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="3a149-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="3a149-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="3a149-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="3a149-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="3a149-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3a149-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="3a149-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="3a149-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="3a149-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3a149-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="3a149-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="3a149-205">settings.SasToken</span></span> |
| <span data-ttu-id="3a149-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3a149-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="3a149-207">Token de SAS de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="3a149-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="3a149-208">Solución de problemas: código de error 1100</span><span class="sxs-lookup"><span data-stu-id="3a149-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="3a149-209">El código de error 1100 indica que hay un problema con la entrada del usuario a la extensión DSC.</span><span class="sxs-lookup"><span data-stu-id="3a149-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="3a149-210">El texto de estos errores es variable y puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="3a149-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="3a149-211">Estos son algunos de los errores que pueden surgir y cómo corregirlos.</span><span class="sxs-lookup"><span data-stu-id="3a149-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="3a149-212">Valores no válidos</span><span class="sxs-lookup"><span data-stu-id="3a149-212">Invalid Values</span></span>
<span data-ttu-id="3a149-213">"Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3a149-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="3a149-214">The only possible values are '', 'Enable', and 'Disable'" (Privacy.dataCollection es '{0}'. Los únicos valores posibles son ", "Enable" y "Disable") "WmfVersion is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3a149-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="3a149-215">Los únicos valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="3a149-215">Only possible values are …</span></span> <span data-ttu-id="3a149-216">y "latest".</span><span class="sxs-lookup"><span data-stu-id="3a149-216">and 'latest'"</span></span>

<span data-ttu-id="3a149-217">Problema: No se permite un valor proporcionado.</span><span class="sxs-lookup"><span data-stu-id="3a149-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="3a149-218">Solución: Cambie el valor no válido a uno válido.</span><span class="sxs-lookup"><span data-stu-id="3a149-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="3a149-219">Consulte la tabla en la sección Detalles.</span><span class="sxs-lookup"><span data-stu-id="3a149-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="3a149-220">Dirección URL no válida</span><span class="sxs-lookup"><span data-stu-id="3a149-220">Invalid URL</span></span>
<span data-ttu-id="3a149-221">"ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3a149-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="3a149-222">This is not a valid URL" (ConfigurationData.url es '{0}'. No es una dirección URL válida) "DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3a149-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="3a149-223">This is not a valid URL" (DataBlobUri es '{0}'. No es una dirección URL válida) "Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3a149-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="3a149-224">This is not a valid URL" This is not a valid URL" (Configuration.url es '{0}'. No es una dirección URL válida)</span><span class="sxs-lookup"><span data-stu-id="3a149-224">This is not a valid URL"</span></span>

<span data-ttu-id="3a149-225">Problema: Se ha proporcionado una dirección URL que no es válida.</span><span class="sxs-lookup"><span data-stu-id="3a149-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="3a149-226">Solución: Compruebe todas las direcciones URL proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="3a149-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="3a149-227">Asegúrese de que todas las direcciones URL se resuelvan en ubicaciones válidas a las que la extensión pueda acceder en la máquina remota.</span><span class="sxs-lookup"><span data-stu-id="3a149-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="3a149-228">Tipo de ConfigurationArguments no válido</span><span class="sxs-lookup"><span data-stu-id="3a149-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="3a149-229">"Invalid configurationArguments type {0}" (Tipo de configurationArguments no válido {0})</span><span class="sxs-lookup"><span data-stu-id="3a149-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="3a149-230">Problema: La propiedad ConfigurationArguments no se puede resolver en un objeto Hashtable.</span><span class="sxs-lookup"><span data-stu-id="3a149-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="3a149-231">Solución: Convierta la propiedad ConfigurationArguments en Hashtable.</span><span class="sxs-lookup"><span data-stu-id="3a149-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="3a149-232">Siga el formato proporcionado en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="3a149-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="3a149-233">Esté atento a las comillas, comas y llaves.</span><span class="sxs-lookup"><span data-stu-id="3a149-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="3a149-234">ConfigurationArguments duplicadas</span><span class="sxs-lookup"><span data-stu-id="3a149-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="3a149-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments" (Se encontraron argumentos duplicados '{0}' en propiedades configurationArguments públicas y privadas)</span><span class="sxs-lookup"><span data-stu-id="3a149-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="3a149-236">Problema: La propiedad ConfigurationArguments en la configuración pública y la propiedad ConfigurationArguments en la configuración protegida contienen propiedades con el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="3a149-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="3a149-237">Solución: Quite una de las propiedades duplicadas.</span><span class="sxs-lookup"><span data-stu-id="3a149-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="3a149-238">Propiedades que faltan</span><span class="sxs-lookup"><span data-stu-id="3a149-238">Missing Properties</span></span>
<span data-ttu-id="3a149-239">"Configuration.function requires that configuration.url or configuration.module is specified" (Configuration.function requiere que se especifiquen configuration.url o configuration.module)</span><span class="sxs-lookup"><span data-stu-id="3a149-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="3a149-240">"Configuration.url requires that configuration.script is specified" (Configuration.url requiere que se especifique configuration.script)</span><span class="sxs-lookup"><span data-stu-id="3a149-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="3a149-241">"Configuration.script requires that configuration.url is specified" (Configuration.script requiere que se especifique configuration.url)</span><span class="sxs-lookup"><span data-stu-id="3a149-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="3a149-242">"Configuration.url requires that configuration.function is specified" (Configuration.url requiere que se especifique configuration.function)</span><span class="sxs-lookup"><span data-stu-id="3a149-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="3a149-243">"ConfigurationUrlSasToken requires that configuration.url is specified" (ConfigurationUrlSasToken requiere que se especifique configuration.url)</span><span class="sxs-lookup"><span data-stu-id="3a149-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="3a149-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified" (ConfigurationDataUrlSasToken requiere que se especifique configurationData.url)</span><span class="sxs-lookup"><span data-stu-id="3a149-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="3a149-245">Problema: Una propiedad definida requiere otra propiedad que falta.</span><span class="sxs-lookup"><span data-stu-id="3a149-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="3a149-246">Soluciones:</span><span class="sxs-lookup"><span data-stu-id="3a149-246">Solutions:</span></span> 

* <span data-ttu-id="3a149-247">Proporcione la propiedad que falta.</span><span class="sxs-lookup"><span data-stu-id="3a149-247">Provide the missing property.</span></span>
* <span data-ttu-id="3a149-248">Quite la propiedad que necesita la propiedad que falta.</span><span class="sxs-lookup"><span data-stu-id="3a149-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a149-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a149-249">Next Steps</span></span>
<span data-ttu-id="3a149-250">Aprenda sobre DSC y los conjuntos de escalado de máquina virtual en [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="3a149-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="3a149-251">Puede encontrar más información en el artículo sobre [administración segura de credenciales de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a149-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3a149-252">Para más información sobre el controlador de extensiones DSC de Azure, consulte [Introducción al controlador de extensiones de configuración de estado deseado de Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a149-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3a149-253">Para más información sobre DSC de PowerShell, [visite el centro de documentación de PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="3a149-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

