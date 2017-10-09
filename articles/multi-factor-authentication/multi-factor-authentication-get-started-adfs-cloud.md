---
title: recursos de nube aaaSecure con MFA de Azure y AD FS | Documentos de Microsoft
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo se inicia tooget con MFA de Azure y AD FS en la nube de Hola."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Protección de recursos en la nube con Azure Multi-Factor Authentication y AD FS
Si su organización está federada con Azure Active Directory, utilice la autenticación multifactor Azure o recursos de toosecure de servicios de federación de Active Directory (AD FS) que se obtiene acceso a Azure AD. Usar hello después de recursos de Active Directory de toosecure procedimientos con la autenticación multifactor Azure o los servicios de federación de Active Directory.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Protección de los recursos de Azure AD mediante AD FS
toosecure el recurso en la nube, configure una regla de notificaciones para que los servicios de federación de Active Directory emite hello multipleauthn notificación cuando un usuario realiza la verificación en dos pasos correctamente. Esta notificación se pasa en tooAzure AD. Siga este toowalk procedimiento a través de los pasos de hello:


1. Abra Administración de AD FS.
2. Hola izquierda, seleccione **Veracidades**.
3. Haga clic con el botón derecho en **Plataforma de identidad de Microsoft Office 365** y seleccione **Editar reglas de notificaciones**.

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. En Reglas de transformación de emisión, haga clic en **Agregar regla**.

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. En Hola transformar notificaciones Asistente para agregar reglas, seleccione **paso a través o filtrar una notificación entrante** de Hola lista desplegable y haga clic en **siguiente**.

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Asigne un nombre a la regla. 
7. Seleccione **referencias de métodos de autenticación** tipo de notificación de Hola entrantes.
8. Seleccione **Pasar a través todos los valores de notificaciones**.
    ![Asistente para agregar regla de notificación de transformación](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Haga clic en **Finalizar** Cierre la consola de administración FS Hola AD.

## <a name="trusted-ips-for-federated-users"></a>Direcciones IP de confianza para usuarios federados
IP de confianza permiten a los administradores verificacion de paso de tooby para direcciones IP concretas o para usuarios federados que tienen las solicitudes que se originan dentro de su propia intranet. Hello las secciones siguientes describen cómo tooconfigure la autenticación multifactor Azure confianza direcciones IP con los usuarios federados y verificacion de eludir cuando una solicitud se origina desde dentro de una intranet de los usuarios federados. Esto se logra mediante la configuración de AD FS toouse un acceso directo o filtrar una plantilla de notificación entrante con hello el tipo de notificación dentro de la red corporativa.

En este ejemplo se utiliza Office 365 para las relaciones de confianza para usuario autenticado .

### <a name="configure-hello-ad-fs-claims-rules"></a>Configurar reglas de notificaciones de AD FS Hola
Hola primera cosa que necesitamos toodo es tooconfigure Hola AD FS notificaciones. Creará dos reglas de notificaciones, uno para hello dentro de la red corporativa de notificación de tipo y otra adicional para mantener a nuestros usuarios que han iniciado.

1. Abra Administración de AD FS.
2. Hola izquierda, seleccione **Veracidades**.
3. Haga clic con el botón derecho en **Plataforma de identidad de Microsoft Office 365** y seleccione **Editar reglas de notificaciones…**
   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. En Reglas de transformación de emisión, haga clic en **Agregar regla**.
   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. En Hola transformar notificaciones Asistente para agregar reglas, seleccione **paso a través o filtrar una notificación entrante** de Hola lista desplegable y haga clic en **siguiente**.
   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. En nombre de regla de tooClaim siguiente de hello cuadro, asigne la regla un nombre. Por ejemplo: InsideCorpNet.
7. Desde la lista desplegable de hello, tooIncoming siguiente tipo de notificación, seleccione **dentro de la red corporativa**.
   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Haga clic en **Finalizar**
9. En Reglas de transformación de emisión, haga clic en **Agregar regla**.
10. En Hola transformar notificaciones Asistente para agregar reglas, seleccione **enviar notificaciones mediante una regla personalizada** de Hola lista desplegable y haga clic en **siguiente**.
11. En el cuadro de hello en nombre de la regla de notificación: escriba *mantener a los usuarios firmado en*.
12. En el cuadro de regla personalizada de hello, escriba:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Haga clic en **Finalizar**
14. Haga clic en **Apply**.
15. Haga clic en **Aceptar**.
16. Cierre Administración de AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Configuración de las IP de confianza de Azure Multi-Factor Authentication con usuarios federados
Ahora que las notificaciones de hello están en su lugar, podemos configurar IP de confianza.

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Hola izquierda, haga clic en **Active Directory**.
3. En el directorio, seleccione el directorio de Hola donde desea tooset una IP de confianza.
4. En hello directorio que ha seleccionado, haga clic en **configurar**.
5. En la sección de la autenticación multifactor de hello, haga clic en **administrar la configuración del servicio**.
6. En la página de configuración del servicio de hello en IP de confianza, seleccione **omitir varios-factor de autenticación para solicitudes de usuarios federados en mi intranet**.  

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Haga clic en **guardar**.
8. Una vez que se han aplicado las actualizaciones de hello, haga clic en **cerrar**.

¡Ya está! En este momento, los usuarios federados de Office 365 solamente deben tener toouse MFA cuando una notificación se origina en la intranet corporativa de hello exterior.
