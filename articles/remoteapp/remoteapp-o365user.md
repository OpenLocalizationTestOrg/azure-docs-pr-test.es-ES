---
title: aaaHow toouse Azure RemoteApp con cuentas de usuario de Office 365 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure RemoteApp con las cuentas de usuario de Office 365"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>¿Cómo toouse Azure RemoteApp con cuentas de usuario de Office 365
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Si tiene una suscripción a Office 365 tiene un Azure Active Directory que almacena los nombres de usuario y contraseñas usan tooaccess servicios de Office 365. Por ejemplo, cuando los usuarios activan Office 365 ProPlus autentican contra toocheck de Azure AD para licencias. Mayoría de los clientes se como toouse Hola mismo directorio con Azure RemoteApp.

Si está implementando Azure RemoteApp, lo más probable es que esté usando una suscripción de Azure asociada a un Azure AD diferente. En Ordenar toouse el directorio de Office 365, necesitará toomove Hola suscripción de Azure en el directorio.

Para obtener información sobre cómo las aplicaciones de cliente de toodeploy Office 365, vea [cómo toouse la suscripción a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Fase 1: Registro de su suscripción gratuita de Office 365 Azure Active Directory
Si usas Hola portal de Azure clásico, siga los pasos de hello en [registrar la suscripción gratuita a Azure Active Directory](https://technet.microsoft.com/library/dn832618.aspx) tooget acceso administrativo tooyour Azure AD a través de hello Portal de administración de Azure. Como resultado de hello de este proceso debe ser capaz de toolog en hello portal de Azure y vea su directorio no existe: en este momento no verá mucho más porque hello suscripción de Azure completo que usa con Azure RemoteApp está en un directorio diferente.

Recuerde Hola nombre y la contraseña de cuenta de administrador de hello creada en este paso, se necesitarán en la fase 2.

Si usas Hola portal de Azure, visite [cómo tooregister y activar una gratuita de Azure Active Directory mediante el portal de Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Fase 2: Hello Azure AD de cambio asociada a su suscripción de Azure.
Vamos toochange su suscripción de Azure desde su directorio actual al directorio de Office 365 Hola que trabajamos en la fase 1.

Siga las instrucciones de hello descritas en [inquilino de Azure Active Directory de cambio hello en Azure RemoteApp](remoteapp-changetenant.md). Pagar toohello especial atención pasos:

* Paso n.º 1: si ha implementado Azure RemoteApp (ARA) en esta suscripción, asegúrese de quitar todas las cuentas de usuario de Azure AD de cualquier colección ARA en primer lugar antes de intentar nada más. También puede eliminar las colecciones existentes.
* Paso n.º 2: este es un paso crítico. Necesita una cuenta de Microsoft toouse (p. ej. @outlook.com) como administrador de servicios de suscripción de hello; esto es porque no podemos tenemos las cuentas de usuario de hello existente vinculada a Azure AD toohello suscripción – si se hace, se no será capaz de toomove se tooa Azure AD diferentes.
* Paso &#4;: Al agregar un directorio existente, Hola sistema le preguntará toosign con cuenta de administrador de Hola para ese directorio. Asegúrese de cuenta de administrador de hello toouse seguro desde la fase 1.
* Paso &#5;: Cambiar el directorio principal de Hola Hola tooyour Office 365 del directorio de suscripción. resultado de Hello final debe ser que en Configuración -> suscripciones la suscripción indica el directorio de hello Office 365. 
  ![Cambie el directorio primario Hola de suscripción de Hola](./media/remoteapp-o365user/settings.png)

En este momento se asocia con su Office 365 Azure AD; la suscripción de Azure RemoteApp Puede utilizar cuentas de usuario de Office 365 existentes Hola con Azure RemoteApp.

