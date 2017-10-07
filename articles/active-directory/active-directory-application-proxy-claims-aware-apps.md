---
title: "aplicaciones con reconocimiento de aaaClaims - Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "¿Cómo toopublish local de las aplicaciones de ASP.NET que aceptan notificaciones ADFS para proteger el acceso remoto por los usuarios."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Trabajo con aplicaciones para notificaciones en Proxy de aplicación
[Aplicaciones para notificaciones](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) realizar un servicio de Token de seguridad (STS) de toohello de redirección. Hola STS solicita las credenciales de usuario de Hola a cambio de un token y, a continuación, redirige aplicación toohello de hello usuario. Hay algunas maneras tooenable Proxy de aplicación toowork con estas redirecciones. Use este artículo tooconfigure la implementación para las aplicaciones para notificaciones. 

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que ese Hola STS que Hola aplicación para notificaciones redirige toois disponible fuera de la red local. Puede hacer Hola STS disponibles mediante la exposición a través de un proxy o puede permitir que fuera de las conexiones. 

## <a name="publish-your-application"></a>Publicación de la aplicación

1. Publicar su aplicación según las instrucciones de toohello descritas en [publicar aplicaciones con Proxy de aplicación](application-proxy-publish-azure-portal.md).
2. Navegar por la página de aplicación toohello Hola portal y seleccione **inicio de sesión único**.
3. Si elige **Azure Active Directory** como **Método de autenticación previa**, seleccione **Se desactivó el inicio de sesión único de Azure AD** como **Método de autenticación interno**. Si ha elegido **Passthrough** como su **método de autenticación previa**, no es necesario toochange nada.

## <a name="configure-adfs"></a>Configuración de AD FS

Puede configurar AD FS en aplicaciones para notificaciones de alguna de estas dos formas. Hola en primer lugar es mediante el uso de dominios personalizados. en segundo lugar es Hola con WS-Federation. 

### <a name="option-1-custom-domains"></a>Opción 1: dominios personalizados

Si todas las direcciones URL internas de Hola para las aplicaciones son nombres completos (FQDN) de nombres de dominio, puede configurar [dominios personalizados](active-directory-application-proxy-custom-domains.md) para sus aplicaciones. Use Hola dominios personalizados toocreate direcciones URL externas que son Hola igual Hola direcciones URL internas. Cuando las direcciones URL externas coincide con las direcciones URL internas, las redirecciones de STS de hello funcionar independientemente de los usuarios estén local o remoto. 

### <a name="option-2-ws-federation"></a>Opción 2: WS-Federation

1. Abra Administración de AD FS.
2. Vaya demasiado**Veracidades**, haga doble clic en la aplicación hello se publica con el Proxy de aplicación y elija **propiedades**.  

   ![Relaciones de confianza para usuario autenticado: haga clic con el botón derecho en el nombre de la aplicación (captura de pantalla)](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. En hello **extremos** ficha **tipo de extremo**, seleccione **WS-Federation**.
4. En **dirección URL de confianza**, escriba dirección URL de Hola que escribió en hello Proxy de aplicación en **dirección URL externa** y haga clic en **Aceptar**.  

   ![Agregar un extremo: establezca el valor de Dirección URL de confianza - captura de pantalla](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Pasos siguientes
* [Habilitar el inicio de sesión único](application-proxy-sso-overview.md) para las aplicaciones que no son compatibles con notificaciones
* [Habilitar toointeract de aplicaciones de cliente nativo con aplicaciones de servidor proxy](active-directory-application-proxy-native-client.md)


