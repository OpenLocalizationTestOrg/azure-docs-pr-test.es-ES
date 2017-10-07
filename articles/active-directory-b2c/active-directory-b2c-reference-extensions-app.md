---
title: "Aplicación de extensiones: Azure AD B2C | Microsoft Docs"
description: "Restaurar Hola b2c extensiones de aplicación"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: aplicación de extensiones

Cuando se crea un directorio de Azure AD B2C, llama a una aplicación `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` automáticamente se crea dentro de hello nuevo directorio. Esta aplicación, que se hace referencia tooas Hola **b2c-extensiones-app**, está visible en *registros de aplicación*. Se utiliza por hello Azure AD B2C toostore información sobre los usuarios y los atributos personalizados. Si se elimina la aplicación hello, Azure AD B2C no funcionará correctamente y el entorno de producción se verán afectado.

> [!IMPORTANT]
> No elimine Hola b2c extensiones de aplicación, a menos que piensa eliminar tooimmediately el inquilino. Si la aplicación hello permanece eliminado durante más de 30 días, información de usuario se perderá permanentemente.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Comprobar que las extensiones de la aplicación hello está presente

tooverify que Hola b2c-extensiones-app está presente:

1. Dentro de su inquilino de Azure AD B2C, haga clic en **más servicios** en el menú de navegación izquierdo de Hola.
1. Busque y abra **Registros de aplicaciones**.
1. Busque una aplicación que empiece por **b2c-extensions-app**.

## <a name="recover-hello-extensions-app"></a>Recuperar la aplicación de las extensiones de hello

Si elimina accidentalmente Hola b2c extensiones de aplicación, tendrá que toorecover de 30 días se. Puede restaurar la aplicación hello mediante Hola API Graph:

1. Examinar demasiado[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Inicie sesión en el sitio de toohello como administrador global para el directorio de Azure AD B2C Hola que desee toorestore Hola Eliminar aplicación para.
1. Emitir una solicitud HTTP GET en la dirección URL de hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` con api-version = 1.6. Asegúrese de que tooreplace `{tenantName}` con el nombre del inquilino. Esta operación enumera todas las aplicaciones de Hola que se han eliminado en hello últimos 30 días.
1. Busque aplicación hello en lista de Hola donde nombre de hello comienza con 'aplicación de extensión b2c' y copie su `objectid` valor de propiedad.
1. Emitir una solicitud HTTP POST con la dirección URL de hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Reemplace hello `{OBJECTID}` parte de la dirección URL de hello con hello `objectid` del paso anterior Hola. 

Ahora debe poder demasiado[vea aplicación hello restaurar](#verifying-that-the-extensions-app-is-present) Hola portal de Azure.

> [!NOTE]
> Una aplicación sólo puede restaurarse si se ha eliminado en hello últimos 30 días. Si han pasado más de 30 días, los datos se perderán permanentemente. Para obtener más ayuda, abra una incidencia de soporte técnico.
