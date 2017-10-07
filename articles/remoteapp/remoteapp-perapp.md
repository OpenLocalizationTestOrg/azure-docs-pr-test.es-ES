---
title: "aplicaciones que aaaPublish tooindividual los usuarios en una colección de RemoteApp de Azure (versión preliminar) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede publicar los usuarios tooindividual de aplicaciones, en lugar de función grupos en Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Publicar aplicaciones que los usuarios tooindividual en una colección de RemoteApp de Azure (vista previa)
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Este artículo se explica cómo los usuarios de toopublish aplicaciones tooindividual en una colección de RemoteApp de Azure. Esto es una nueva funcionalidad en Azure RemoteApp, actualmente en vista previa privada y pioneros disponible tooselect solo para fines de evaluación.

Originalmente Azure RemoteApp habilitado solo un modo de publicación de aplicaciones: Administrador de hello podría publicar aplicaciones de imagen de Hola y estarían tooall visible a los usuarios en la colección de Hola.

Un escenario común es tooinclude muchas aplicaciones en una sola imagen e implementación una colección de los costos de administración de tooreduce de orden. A menudo no todas las aplicaciones son usuarios de tooall relevante: administradores preferirían a los usuarios de toopublish aplicaciones tooindividual no ver aplicaciones innecesarias en su aplicación de fuentes de distribución.

Ahora, esto es posible en Azure RemoteApp: actualmente solo como una característica de versión preliminar limitada. Este es un breve resumen de la nueva funcionalidad de hello:

1. Una colección se puede establecer de uno de estos dos modos:
   
   * modo de recopilación original Hello, donde pueden ver todos los usuarios de una colección de todas las aplicaciones publicadas. Se trata de modo predeterminado de Hola.
   * nuevo modo de aplicación Hola, donde los usuarios sólo verán las aplicaciones que se han asignado explícitamente toothem
2. En el momento de hello en modo de aplicación Hola solo puede habilitarse mediante cmdlets de PowerShell de Azure RemoteApp.
   
   * Al establecer el modo de tooapplication, asignación de usuario en el conjunto de hello no se pueden administrar a través de Hola portal de Azure. Asignación de usuario tiene toobe administra a través de los cmdlets de PowerShell.
3. Los usuarios sólo verán las aplicaciones de hello directamente publican toothem. Sin embargo, es aún posible para un usuario toolaunch Hola otras aplicaciones disponibles en la imagen de hello mediante el acceso a ellos directamente en el sistema operativo de Hola.
   
   * Esta característica no proporciona un bloqueo seguro de aplicaciones; sólo limita la visibilidad en la aplicación hello fuente de distribución.
   * Si necesita tooisolate a los usuarios de aplicaciones, necesitará toouse de colecciones independientes para.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>¿Cómo tooget cmdlets de PowerShell de Azure RemoteApp
tootry Hola nueva funcionalidad de vista previa, necesitará toouse cmdlets de PowerShell de Azure. Actualmente no es toouse posibles hello Azure Management portal tooenable Hola nueva publicación modo de aplicación.

En primer lugar, asegúrese de que tiene hello [módulo Azure PowerShell](/powershell/azure/overview) instalado.

A continuación, iniciar la consola de PowerShell de hello en modo de administrador y ejecución Hola siguiente cmdlet:

        Add-AzureAccount

Se le pedirá el nombre de usuario y la contraseña de Azure. Una vez iniciado sesión, se efectuarán toorun capaz de cmdlets de Azure RemoteApp en las suscripciones de Azure.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>¿Cómo toocheck de modo que una colección está en
Ejecute hello siguiente cmdlet:

        Get-AzureRemoteAppCollection <collectionName>

![Modo de recopilación de Hola de comprobación](./media/remoteapp-perapp/araacllelvel.png)

Hola AclLevel propiedad puede tener Hola siguientes valores:

* Colección: Hola publicación modo original. Todos los usuarios pueden ver todas las aplicaciones publicadas.
* Aplicación: Hola nuevo modo de publicación. Los usuarios ver solo las aplicaciones de hello directamente publicarán toothem.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Cómo el modo de publicación de tooapplication tooswitch
Ejecute hello siguiente cmdlet:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Se conservará el estado de publicación de aplicación: inicialmente todos los usuarios verán todas las aplicaciones publicadas original Hola.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Cómo los usuarios de toolist que pueden ver una aplicación específica
Ejecute hello siguiente cmdlet:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Esta acción muestra todos los usuarios que pueden ver la aplicación hello.

Nota: Puede ver el alias de la aplicación de hello (denominados "alias de la aplicación" en la sintaxis de hello anterior) mediante la ejecución de Get-AzureRemoteAppProgram - nombreDeColección <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>¿Cómo tooassign un usuario de tooa la aplicación
Ejecute hello siguiente cmdlet:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

usuario de Hello ahora podrán disfrutar aplicación hello en el cliente de Azure RemoteApp hello y será capaz de tooconnect tooit.

## <a name="how-tooremove-an-application-from-a-user"></a>¿Cómo tooremove una aplicación de un usuario
Ejecute hello siguiente cmdlet:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Envío de comentarios
Agradecemos sus comentarios y sugerencias sobre esta característica de la versión preliminar. Rellene hello [encuesta](http://www.instant.ly/s/FDdrb) toolet nos conocer su opinión.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>¿No he tenido una característica de vista previa de oportunidad tootry Hola?
Si no ha participado en vista previa de hello todavía, use este [encuesta](http://www.instant.ly/s/AY83p) toorequest acceso.

