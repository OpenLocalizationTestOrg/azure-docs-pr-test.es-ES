---
title: aaaPublish-WebApplicationWebSite (script de Windows PowerShell) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toopublish un sitio web del proyecto tooan sitio Web de Azure. Este script crea recursos Hola necesario en su suscripción de Azure si no existen."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publicación de WebApplicationWebSite (script de Windows PowerShell)
## <a name="syntax"></a>Sintaxis
Publica un tooan de proyecto web sitio Web de Azure. script de Hola crea recursos Hola necesario en su suscripción de Azure si no existen.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuración
Hola ruta de acceso toohello archivo de configuración JSON que describe los detalles de Hola de implementación de Hola.

| Parámetro | Valor predeterminado |
| --- | --- |
| Alias |Ninguna |
| ¿Necesario? |true |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

## <a name="subscriptionname"></a>SubscriptionName
nombre de Hola de suscripción de Azure que desea incluir el sitio Web de hello toocreate en hello.

| Parámetro | Valor predeterminado |
| --- | --- |
| Alias |Ninguna |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
Hola ruta de acceso toohello web paquete toopublish toohello sitio Web de implementación. Puede crear este paquete con el Asistente de publicación Web de hello en Visual Studio. Para obtener más información, consulte [Introducción a Servicios en la nube de Azure y ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parámetro | Valor predeterminado |
| --- | --- |
| Alias |Ninguna |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
nombre de usuario de Hola y la contraseña de base de datos SQL de hello en Azure.

| Parámetro | Valor predeterminado |
| --- | --- |
| Alias |Ninguna |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |Ninguna |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Si es true, imprimir mensajes de Hola script toohello flujo de salida.

| Parámetro | Valor predeterminado |
| --- | --- |
| Alias |Ninguna |
| ¿Necesario? |false |
| Posición |con nombre |
| Valor predeterminado |false |
| ¿Aceptar la entrada de la canalización? |false |
| ¿Aceptar caracteres comodín? |false |

## <a name="remarks"></a>Comentarios
Para obtener una explicación completa de cómo toouse Hola script toocreate Dev y entornos de prueba, consulte [entornos de prueba y el uso de Scripts de Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).

archivo de configuración de JSON de Hello especifica detalles de Hola de novedades toobe implementado. Incluye información de Hola que se especificó cuando creó el proyecto de hello, como el nombre de Hola y el nombre de usuario para el sitio Web de Hola. También incluye hello tooprovision de base de datos, si lo hay. Hola siguiente código muestra un archivo de configuración de JSON de ejemplo:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Puede editar el archivo de configuración de hello JSON toochange lo que se implementa. Se requiere una sección del sitio Web, pero Hola sección de base de datos es opcional.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, consulte [Publish-WebApplicationVM (script de Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

