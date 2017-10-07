---
title: aaaPublish-WebApplicationVM | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy una máquina virtual de web application tooa. Este script crea recursos Hola necesario en su suscripción de Azure si no existen."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (script de Windows PowerShell)
Implementa una máquina virtual de web application tooa. script de Hola crea recursos Hola necesario en su suscripción de Azure si no existen.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configuración
Hola ruta de acceso toohello archivo de configuración JSON que describe los detalles de Hola de implementación de Hola.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |true |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

### <a name="subscriptionname"></a>SubscriptionName
nombre de Hola de Hola suscripción de Azure en que desea que la máquina virtual de toocreate Hola.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Usa Hola primera suscripción en el archivo de suscripción de hello |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
Hola ruta de acceso toohello web implementación paquete toopublish toohello la máquina virtual. Puede crear este paquete con el Asistente de publicación Web de hello en Visual Studio. Consulte [Cómo crear un paquete de implementación web en Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
Si es true, permite el uso de Hola de certificados que no están firmados por una entidad emisora raíz de confianza.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |false |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

### <a name="vmpassword"></a>VMPassword
credenciales de Hola para cuenta de máquina virtual de Hola. Ejemplo: - VMPassword @{nombre = "admin"; Contraseña = "contraseña"}

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
Hola las credenciales de base de datos SQL de hello en Azure. Ejemplo: - DatabaseServerPassword @{nombre = "admin"; Contraseña = "contraseña"}

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Si es true, imprimir mensajes de Hola script toohello flujo de salida.

| Alias | Ninguna |
| --- | --- |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |false |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

## <a name="remarks"></a>Comentarios
Para obtener una explicación completa de cómo toouse Hola script toocreate Dev y entornos de prueba, consulte [entornos de prueba y el uso de Scripts de Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).

archivo de configuración de JSON de Hello especifica detalles de Hola de novedades toobe implementado. Incluye información de Hola que se especificó cuando creó el proyecto de hello, como nombre de hello, grupo de afinidad, imagen de disco duro virtual y el tamaño de máquina virtual de Hola. También incluye los extremos de hello en la máquina virtual de hello, hello tooprovision de bases de datos, si procede y parámetros de implementación web. Hola siguiente código muestra un archivo de configuración de JSON de ejemplo:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Puede editar el archivo de configuración de hello JSON toochange lo que se aprovisiona. Una máquina virtual y un servicio de nube son necesarias, pero la sección de la base de datos de hello es opcional.

