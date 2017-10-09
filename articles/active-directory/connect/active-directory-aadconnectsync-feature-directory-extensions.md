---
title: "Sincronización de Azure AD Connect: Extensiones de directorio | Microsoft Docs"
description: "Este tema describe la característica de extensiones de directorio de hello en Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Sincronización de Azure AD Connect: Extensiones de directorio
Extensiones de directorio permite esquemas de hello tooextend en Azure AD con sus propios atributos de la instancia local de Active Directory. Esta característica le permite consumir atributos continuar toomanage local toobuild las aplicaciones LOB. Estos atributos se pueden consumir mediante [extensiones de directorio de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/). Puede ver Hola atributos disponible mediante [explorer de Azure AD Graph](https://graphexplorer.cloudapp.net) y [el Explorador de Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivamente.

En la actualidad, ninguna carga de trabajo de Office 365 consume estos atributos.

Configurar los atributos adicionales que desee toosynchronize en la ruta de acceso de configuración personalizada de hello en el Asistente para la instalación de Hola.
![Asistente para la extensión de esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
instalación de Hello muestra hello siguientes atributos, que son candidatas válidas:

* Tipos de objetos de usuario y de grupo
* Atributos de valor único: cadena, booleano, entero y binario
* Atributos multivalor: cadena y binario

lista de Hola de atributos es de lectura de caché de esquema de hello creado durante la instalación de Azure AD Connect. Si se ha ampliado el esquema de Active Directory de hello con atributos adicionales, Hola [se debe actualizar el esquema](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) antes de que estos nuevos atributos están visibles.

Un objeto en Azure AD puede tener los atributos de las extensiones de directorio too100. longitud máxima de Hello es 250 caracteres. Si un valor de atributo es más largo, se trunca el motor de sincronización Hola.

Durante la instalación de Azure AD Connect, se registra una aplicación donde estos atributos estén disponibles. Puede ver esta aplicación Hola portal de Azure.  
![Aplicación de extensión de esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Estos atributos están ahora disponibles en Graph:   
![Grafo](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

atributos de Hello tienen el prefijo con la extensión\_{AppClientId}\_. Hola AppClientId tiene Hola mismo valor para todos los atributos en el inquilino de Azure AD.

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
