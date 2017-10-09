---
title: aaaPass valores complejos entre plantillas de Azure | Documentos de Microsoft
description: Muestra recomienda enfoques para utilizar datos de estado de objetos complejos tooshare con plantillas del Administrador de recursos de Azure y plantillas vinculadas.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Tooand de estado de recurso compartido de plantillas del Administrador de recursos de Azure
En este tema se muestran los procedimientos recomendados para administrar y compartir el estado en las plantillas. Hello parámetros y variables que se muestran en este tema son ejemplos de tipo hello de objetos se pueden definir tooconveniently organizar los requisitos de implementación. Desde estos ejemplos, puede implementar sus propios objetos con valores de propiedad que tengan sentido para su entorno.

Este tema forma parte de un artículo más extenso. Hola tooread completa papel, descargue [clase recursos el Administrador de plantillas de consideraciones y prácticas comprobadas](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Proporcionar opciones de configuración estándar
En lugar de ofrecer una plantilla que proporciona total flexibilidad y muchas variaciones, un patrón común es tooprovide una selección de configuraciones conocidas. De hecho, los usuarios pueden seleccionar tamaños estándar de camiseta como espacio aislado, pequeño, mediano y grande. Otros ejemplos de tamaños de camiseta son ofertas de productos, como edición para la comunidad o edición para impresa. En otros casos, pueden ser configuraciones de una tecnología específicas de la carga de trabajo, como MapReduce o NoSQL.

Con objetos complejos, puede crear variables que contienen colecciones de datos, a veces conocidos como "los contenedores de propiedades" y usar esa declaración de recurso de datos toodrive hello en la plantilla. Este enfoque proporciona configuraciones bien conocidas de tamaños variables que están preconfiguradas para los clientes. Sin configuraciones conocidas, los usuarios de la plantilla de hello deben determinar el tamaño de clúster en función de su propios, factor en las restricciones de recursos de plataforma y hacer matemáticas tooidentify Hola resultante particiones de las cuentas de almacenamiento y otros recursos (debido a tamaño toocluster y restricciones de recursos). Además toomaking una mejor experiencia de cliente hello, algunas configuraciones conocidas son toosupport más fácil y pueden ayudarle a ofrecer un mayor nivel de densidad.

Hola siguiente ejemplo se muestra cómo las variables de toodefine que contienen objetos complejos para representar las colecciones de datos. colecciones de Hello definen los valores que se usan para el tamaño de la máquina virtual, configuración de red, configuración del sistema operativo y configuración de disponibilidad.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

Tenga en cuenta que hello **tshirtSize** variable concatena el tamaño de la camiseta de hello proporcionan a través de un parámetro (**pequeño**, **medio**, **grande**) texto toohello **tshirtSize**. Utilice esta variable de objeto complejo asociado tooretrieve variable Hola para ese tamaño camiseta.

A continuación, puede hacer referencia a estas variables más adelante en la plantilla de Hola. capacidad de Hello tooreference denominado-variables y sus propiedades simplifica la sintaxis de la plantilla de Hola y resulta fácil toounderstand contexto. Hola siguiente ejemplo define un recurso toodeploy mediante objetos de Hola se ha mostrado anteriormente tooset valores. Por ejemplo, hello tamaño de máquina virtual se establece mediante la recuperación de valor de hello para `variables('tshirtSize').vmSize` mientras el valor de hello para el tamaño del disco de Hola se recupera de `variables('tshirtSize').diskSize`. Además, Hola URI para una plantilla vinculada se establece con el valor de Hola para `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Pase la plantilla de tooa de estado
Comparte el estado en una plantilla mediante parámetros que proporciona directamente durante la implementación.

Hola tabla listas usadas parámetros en las plantillas siguientes.

| Nombre | Valor | Descripción |
| --- | --- | --- |
| location |Cadena de una lista restringida de regiones de Azure |ubicación de Hola donde se implementan los recursos de Hola. |
| storageAccountNamePrefix |String |Nombre DNS único para la cuenta de almacenamiento donde se colocan los discos de la máquina virtual de Hola Hola |
| domainName |String |Nombre de dominio de hello accesible públicamente jumpbox VM en formato de hello: **{domainName}. {} ubicación}.cloudapp.com** por ejemplo: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |String |Nombre de usuario para hello las máquinas virtuales |
| adminPassword |String |Contraseña de hello las máquinas virtuales |
| tshirtSize |Cadena de una lista restringida de tamaños de camiseta ofrecidos |Hola denominado tooprovision de tamaño de unidad de escala. Por ejemplo, "Pequeña", "Mediana", "Grande" |
| virtualNetworkName |String |Nombre de red virtual de Hola que Hola consumidor desea toouse. |
| enableJumpbox |Cadena de una lista restringida (habilitada o deshabilitada) |Parámetro que identifica si tooenable un jumpbox para entorno de Hola. Valores: "habilitado", "deshabilitado" |

Hola **tshirtSize** parámetro usado en la sección anterior de Hola se define como:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Pasar plantillas toolinked de estado
Cuando se conecte toolinked plantillas, a menudo utilizar una combinación de estático y genera las variables.

### <a name="static-variables"></a>Variables estáticas
Variables estáticas a menudo son los valores de base de tooprovide usado, como las direcciones URL, que se utilizan a lo largo de una plantilla.

Hola siguiente extracto de plantilla, `templateBaseUrl` especifica la ubicación de raíz de hello para la plantilla de hello en GitHub. línea siguiente de Hello crea una nueva variable `sharedTemplateUrl` que concatena Hola dirección URL base con el nombre conocido de Hola de plantilla de recursos compartidos de Hola. Por debajo de esa línea, una variable de objeto complejo es toostore usa un tamaño de la camiseta, donde URL base hello es toohello concatenado conoce la ubicación de la plantilla de configuración y se almacenan en hello `vmTemplate` propiedad.

ventaja de Hola de este enfoque es que si cambia la ubicación de la plantilla de hello, solo necesita la variable estática de hello toochange en un solo lugar, que pasa a lo largo de plantillas de hello vinculado.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Variables generadas
En variables de toostatic de adición, varias variables se generan dinámicamente. En esta sección se identifica algunos de los tipos comunes de Hola de variables generados.

#### <a name="tshirtsize"></a>tshirtSize
Está familiarizado con esta variable generada de ejemplos de hello anteriores.

#### <a name="networksettings"></a>networkSettings
En un Hola de capacidad, funcionalidad o plantilla de solución de ámbito de extremo a extremo, plantillas vinculadas normalmente crean recursos que existen en una red. Un enfoque sencillo es toouse una configuración de red de toostore de objeto complejo y pasarlas toolinked plantillas.

A continuación puede verse un ejemplo de comunicación de la configuración de red.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Los recursos creados en las plantillas vinculadas a menudo se colocan en un conjunto de disponibilidad. En el siguiente ejemplo de Hola, nombre del conjunto de disponibilidad de Hola se especifica también Hola dominio de error y actualice toouse de recuento de dominio.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Si tiene varios conjuntos de disponibilidad (por ejemplo, uno para los nodos principales) y otro para los nodos de datos, puede utilizar un nombre como prefijo, especifique varios conjuntos de disponibilidad o seguir modelo Hola mostrado anteriormente para crear una variable para un tamaño específico de la camiseta.

#### <a name="storagesettings"></a>storageSettings
Los detalles de almacenamiento a menudo se comparten con las plantillas vinculadas. En el ejemplo de Hola siguiente, un *storageSettings* objeto proporciona detalles acerca de hello nombres de cuenta y el contenedor de almacenamiento.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Con las plantillas vinculadas, puede que tenga tipos de nodos de toovarious de configuración de sistema operativo de toopass entre los tipos de configuración conocido diferente. Un objeto complejo es una información del sistema operativo toostore y compartir fácilmente y también resulta más fácil toosupport múltiples opciones de sistema operativo para la implementación.

Hello en el ejemplo siguiente se muestra un objeto para *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Una variable generada, *machineSettings* es un objeto complejo que contiene una combinación de variables principales para crear una VM. variables de Hello incluyen el nombre de usuario de administrador y contraseña, un prefijo para los nombres de máquina virtual de Hola y referencia de una imagen de sistema operativo.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Tenga en cuenta que *osImageReference* recupera Hola valores de hello *osSettings* variable definida en la plantilla principal Hola. Esto significa que puede cambiar fácilmente el sistema operativo de Hola para una máquina virtual: completamente o basado en la preferencia de Hola de un consumidor de plantilla.

#### <a name="vmscripts"></a>vmScripts
Hola *vmScripts* objeto contiene los detalles sobre toodownload de secuencias de comandos de Hola y ejecutar en una instancia de máquina virtual, incluidas las referencias exterior e interior. Fuera de las referencias incluyen infraestructura Hola.
Las referencias de interior incluyen configuración y software de hello instalado instalado.

Usar hello *scriptsToDownload* Hola de propiedad toolist scripts toodownload toohello máquina virtual. Este objeto también contiene los argumentos de línea de toocommand de referencias para diferentes tipos de acciones. Estas acciones incluyen la ejecución de la instalación predeterminada de Hola para cada nodo individual, una instalación que se ejecuta después de que se implementan todos los nodos y scripts adicionales que pueden ser tooa específico que proporciona la plantilla.

Este ejemplo es de un toodeploy de plantilla que se usa MongoDB, que requiere un árbitro toodeliver alta disponibilidad. Hola *arbiterNodeInstallCommand* se ha agregado demasiado*vmScripts* tooinstall árbitro de Hola.

sección de variables de Hello es dónde encontrar las variables de Hola que definen la secuencia de comandos de hello texto específico tooexecute Hola con los valores adecuados de Hola.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Devolver el estado de una plantilla
No solo puede pasar datos en una plantilla, también puede plantilla que realiza la llamada de recurso compartido de datos back-toohello. Hola **genera** sección de una plantilla vinculada, puede proporcionar los pares clave/valor que se pueden usar en la plantilla de origen de Hola.

Hello en el ejemplo siguiente se muestra cómo toopass Hola dirección IP privada generada en una plantilla vinculada.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

Dentro de la plantilla principal de hello, puede usar esos datos con la sintaxis de hello:

    "[reference('master-node').outputs.masterip.value]"

Puede utilizar esta expresión en la sección de salidas de Hola o sección de recursos de hello de la plantilla principal Hola. No puede usar expresión de hello en la sección de variables de hello porque se basa en el estado de tiempo de ejecución de Hola. tooreturn este valor de la plantilla principal de hello, utilice:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Para un ejemplo del uso de hello genera sección una plantilla vinculada tooreturn de discos de datos para una máquina virtual, consulte [crear varios discos de datos para una máquina Virtual](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Definir la configuración de autenticación de una máquina virtual
Puede usar hello mismo patrón que se ha mostrado anteriormente para la configuración de autenticación de configuración configuración toospecify Hola para una máquina virtual. Cree un parámetro para pasarlo en tipo hello de autenticación.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Agregue las variables para hello diferentes tipos de autenticación y una variable toostore qué tipo se usa para esta implementación en función del valor Hola de parámetro hello.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Al definir la máquina virtual de hello, establecer hello **osProfile** variable toohello que creó.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de las secciones de Hola de plantilla de hello, consulte [creación de plantillas de administrador de recursos de Azure](resource-group-authoring-templates.md)
* toosee Hola funciones que están disponibles en una plantilla, vea [funciones de plantilla de administrador de recursos de Azure](resource-group-template-functions.md)
