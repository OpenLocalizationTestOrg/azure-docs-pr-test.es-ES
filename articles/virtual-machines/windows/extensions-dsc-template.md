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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>VMSS de Windows y configuración de estado deseado con plantillas de Azure Resource Manager
Este artículo describe la plantilla de administrador de recursos de Hola para hello [controlador de extensión de configuración de estado deseado](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Ejemplo de plantilla para una máquina virtual de Windows
Hello fragmento de código siguiente va en hello sección de recursos de plantilla de Hola.

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

## <a name="template-example-for-windows-vmss"></a>Ejemplo de plantilla para VMSS de Windows
Un nodo VMSS tiene una sección "propiedades" con hello "VirtualMachineProfile", "extensionProfile" atributo. DSC se agrega en "extensions". 

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

## <a name="detailed-settings-information"></a>Información de configuración detallada
Hola esquema siguiente es para la parte de la configuración de Hola de hello extensión de DSC de Azure en una plantilla de Azure Resource Manager.

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

## <a name="details"></a>Detalles
| Nombre de propiedad | Tipo | Description |
| --- | --- | --- |
| settings.wmfVersion |cadena |Especifica la versión de Hola de hello Windows Management Framework que debe instalarse en la máquina virtual. Establecer esta propiedad too'latest' instala Hola versión más actualizada de WMF. Hola, solo actual, valores posibles para esta propiedad son **'4.0', '5.0', ' 5.0PP' y 'última ' hora**. Estos valores posibles son tooupdates de asunto. valor predeterminado de Hello es 'última'. |
| settings.configuration.url |cadena |Especifica el archivo zip de configuración de DSC de ubicación de dirección URL de Hola desde qué toodownload. Si la dirección URL de hello proporcionada requiere un token de SAS para el acceso, debe tooset hello protectedSettings.configurationUrlSasToken toohello valor de propiedad su token SAS. Esta propiedad es necesaria si se definen settings.configuration.script o settings.configuration.function. |
| settings.configuration.script |cadena |Especifica el nombre de archivo de hello del script de Hola que contiene la definición de saludo de la configuración de DSC. Esta secuencia de comandos debe estar en la carpeta raíz de hello del archivo zip de hello descargado de dirección URL de hello especificada por la propiedad de configuration.url Hola. Esta propiedad es necesaria si se definen settings.configuration.url o settings.configuration.script. |
| settings.configuration.function |cadena |Especifica el nombre de saludo de la configuración de DSC. configuración de Hello denominada debe estar contenido en script de Hola definido por configuration.script. Esta propiedad es necesaria si se definen settings.configuration.url o settings.configuration.function. |
| settings.configurationArguments |Colección |Define los parámetros que le gustaría toopass tooyour la configuración de DSC. Esta propiedad no está cifrada. |
| settings.configurationData.url |cadena |Especifica la dirección de URL de Hola desde qué toodownload los datos de configuración (. psd1) de archivos toouse como entrada para la configuración de DSC. Si la dirección URL de hello proporcionada requiere un token de SAS para el acceso, debe tooset hello protectedSettings.configurationDataUrlSasToken toohello valor de propiedad su token SAS. |
| settings.privacy.dataEnabled |string |Habilita o deshabilita la recopilación de telemetría. Hello solo los valores posibles para esta propiedad son **'Enable', 'Disable', '', o $null**. Si se deja esta propiedad en blanco o como null, se habilita la telemetría. valor predeterminado de Hello es ''. [Más información](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Colección |Define las ubicaciones alternativas que desde qué toodownload Hola WMF. [Más información](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Colección |Define los parámetros que le gustaría toopass tooyour la configuración de DSC. Esta propiedad no está cifrada. |
| protectedSettings.configurationUrlSasToken |cadena |Especifica Hola SAS tooaccess token Hola dirección URL definida por configuration.url. Esta propiedad no está cifrada. |
| protectedSettings.configurationDataUrlSasToken |cadena |Especifica Hola SAS tooaccess token Hola dirección URL definida por configurationData.url. Esta propiedad no está cifrada. |

## <a name="settings-vs-protectedsettings"></a>Settings frente a ProtectedSettings
Todas las configuraciones se guardan en un archivo de texto de configuración en hello máquina virtual.
Propiedades, en "configuración" son propiedades públicas porque no se cifran en el archivo de texto de configuración de Hola.
Propiedades de 'protectedSettings' se cifran con un certificado y no se muestran en texto sin formato de este archivo en hello máquina virtual.

Si la configuración de hello necesita credenciales, pueden incluirse en protectedSettings:

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

## <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se deriva de sección "Introducción" de Hola de hello [página información general sobre el controlador de extensión de DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Este ejemplo utiliza plantillas de administrador de recursos en lugar de cmdlets toodeploy Hola. Guardar configuración de "IisInstall.ps1" Hola, colóquelo en una. COMPRIMIR archivos y cargue el archivo de hello en una dirección URL accesible. Este ejemplo utiliza el almacenamiento de blobs de Azure, pero es posible toodownload. Archivos ZIP desde cualquier ubicación arbitraria.

En plantilla de Azure Resource Manager hello, hello código siguiente indica al archivo correcto de hello VM toodownload Hola y ejecuta la función de PowerShell adecuado de hello:

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

## <a name="updating-from-hello-previous-format"></a>Actualizar desde Hola formato anterior
Cualquier opción de hello formato anterior (que contiene propiedades públicas de hello ModulesUrl, ConfigurationFunction, SasToken o propiedades) automáticamente adapta toohello actual formato y ejecuta tal y como lo hacían antes.

Hola después de esquema es qué esquema de configuración anterior de hello tenía el siguiente aspecto:

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

Le mostramos cómo formato anterior de Hola adapta toohello actual formato:

| Nombre de propiedad | Equivalente en el esquema anterior |
| --- | --- |
| settings.wmfVersion |settings.wmfVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |Primera parte de settings.ConfigurationFunction (antes de '\\\\') |
| settings.configuration.function |Segunda parte de settings.ConfigurationFunction (después de '\\\\') |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri (sin token de SAS) |
| settings.privacy.dataEnabled |settings.privacy.dataEnabled |
| settings.advancedOptions.downloadMappings |settings.advancedOptions.downloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |Token de SAS de protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Solución de problemas: código de error 1100
Código de error 1100 indica que hay un problema con hello extensión toohello DSC de intervención del usuario.
texto Hello de estos errores es variable y se puede cambiar.
Estas son algunas de los errores de hello con que puede encontrarse y cómo corregirlos.

### <a name="invalid-values"></a>Valores no válidos
"Privacy.dataCollection is '{0}'. Hello solo los valores posibles son ","Habilitar"y"Deshabilitar"" "WmfVersion es '{0}'. Los únicos valores posibles son: y "latest".

Problema: No se permite un valor proporcionado.

Solución: Cambie el valor válido de tooa de valor no válido de Hola. Vea la tabla de hello en la sección de detalles de Hola.

### <a name="invalid-url"></a>Dirección URL no válida
"ConfigurationData.url is '{0}'. This is not a valid URL" (ConfigurationData.url es '{0}'. No es una dirección URL válida) "DataBlobUri is '{0}'. This is not a valid URL" (DataBlobUri es '{0}'. No es una dirección URL válida) "Configuration.url is '{0}'. This is not a valid URL" This is not a valid URL" (Configuration.url es '{0}'. No es una dirección URL válida)

Problema: Se ha proporcionado una dirección URL que no es válida.

Solución: Compruebe todas las direcciones URL proporcionadas. Asegúrese de que todas las direcciones URL resolver las ubicaciones de toovalid que puede tener acceso extensión hello en el equipo remoto de Hola.

### <a name="invalid-configurationargument-type"></a>Tipo de ConfigurationArguments no válido
"Invalid configurationArguments type {0}" (Tipo de configurationArguments no válido {0})

Problema: Hola ConfigurationArguments propiedad no puede resolver tooa objeto de tabla hash. 

Solución: Convierta la propiedad ConfigurationArguments en Hashtable. Tener el formato de hello proporcionada en el ejemplo de Hola precedente. Esté atento a las comillas, comas y llaves.

### <a name="duplicate-configurationarguments"></a>ConfigurationArguments duplicadas
"Found duplicate arguments '{0}' in both public and protected configurationArguments" (Se encontraron argumentos duplicados '{0}' en propiedades configurationArguments públicas y privadas)

Problema: Hola ConfigurationArguments en la configuración pública y ConfigurationArguments en configuración protegida hello contienen propiedades con hello mismo nombre.

Solución: Quite una de las propiedades duplicadas Hola.

### <a name="missing-properties"></a>Propiedades que faltan
"Configuration.function requires that configuration.url or configuration.module is specified" (Configuration.function requiere que se especifiquen configuration.url o configuration.module)

"Configuration.url requires that configuration.script is specified" (Configuration.url requiere que se especifique configuration.script)

"Configuration.script requires that configuration.url is specified" (Configuration.script requiere que se especifique configuration.url)

"Configuration.url requires that configuration.function is specified" (Configuration.url requiere que se especifique configuration.function)

"ConfigurationUrlSasToken requires that configuration.url is specified" (ConfigurationUrlSasToken requiere que se especifique configuration.url)

"ConfigurationDataUrlSasToken requires that configurationData.url is specified" (ConfigurationDataUrlSasToken requiere que se especifique configurationData.url)

Problema: Una propiedad definida requiere otra propiedad que falta.

Soluciones: 

* Proporcionar falta la propiedad Hola.
* Quite la propiedad de Hola que necesita la propiedad que falta Hola.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información sobre DSC y escalas de máquina virtual se establece [usar escala conjuntos de máquina Virtual con hello extensión de DSC de Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Puede encontrar más información en el artículo sobre [administración segura de credenciales de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obtener más información sobre el controlador de extensión de DSC de Azure de hello, consulte [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview). 

