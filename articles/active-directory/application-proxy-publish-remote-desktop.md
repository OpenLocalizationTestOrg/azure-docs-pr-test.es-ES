---
title: "aaaPublish escritorio remoto con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Abarca conceptos básicos de hello acerca de los conectores de Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Publicación de Escritorio Remoto con el Proxy de aplicación de Azure AD

Este artículo se trata cómo toodeploy servicios de escritorio remoto (RDS) con el Proxy de aplicación para que los usuarios remotos pueden ser más productivos.

Hola dirigida está dirigido a este artículo:
- Clientes de Proxy de aplicación de Azure AD actuales que desean toooffer los usuarios finales de tootheir de más aplicaciones mediante la publicación de aplicaciones locales a través de servicios de escritorio remoto.
- Clientes de servicios de escritorio remoto actuales que deseen superficie expuesta a ataques tooreduce Hola de su implementación mediante el uso de Proxy de aplicación de Azure AD. Este escenario le ofrece un conjunto limitado de verificación en dos pasos y tooRDS de controles de acceso condicional.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Cómo encaja el Proxy de aplicación en la implementación de RDS estándar Hola

Una implementación de RDS estándar incluye diversos servicios de rol de Escritorio remoto que se ejecutan en Windows Server. Examinando hello [arquitectura de servicios de escritorio remoto](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), existen varias opciones de implementación. Hola diferencia más notable entre hello [implementación de RDS con el Proxy de aplicación de Azure AD](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (que se muestra en hello siguiente diagrama) y hello otras opciones de implementación es ese escenario de Proxy de aplicación hello tiene una salida permanente conexión desde el servidor de hello ejecutando el servicio de conector de Hola. Otras implementaciones dejan conexiones entrantes abiertas a través de un equilibrador de carga.

![Aplicación sigue Proxy entre Hola RDS VM y Hola internet pública](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

En una implementación de RDS, rol Web de escritorio remoto de Hola y rol de puerta de enlace de escritorio remoto de Hola se ejecutan en máquinas con conexión a Internet. Estos puntos de conexión se exponen para hello siguientes motivos:
- Web de escritorio remoto proporciona a usuario Hola un toosign de punto de conexión público en y vista Hola diversas aplicaciones locales y escritorio pueden tener acceso. Al seleccionar un recurso, una conexión RDP se crea mediante la aplicación nativa de hello en hello SO.
- Puerta de enlace de escritorio remoto entra en la imagen de hello una vez que un usuario inicia la conexión RDP de Hola. Hola puerta de enlace de escritorio remoto controla el tráfico RDP Hola cifrado transmite a través de Internet de Hola y lo traduce toohello servidor local que Hola usuario se conecta a. En este escenario, Hola Hola de tráfico que puerta de enlace de escritorio remoto está recibiendo procede de hello Proxy de aplicación de Azure AD.

>[!TIP]
>Si aún no ha implementado RDS antes, o desea obtener más información antes de comenzar, obtenga información acerca de cómo demasiado[perfectamente implementar RDS con el Administrador de recursos de Azure y Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Requisitos

- Ambos hello Web de escritorio remoto y puerta de enlace de escritorio remoto deben estar ubicados los puntos de conexión en Hola mismo equipo y con una raíz común. Web de escritorio remoto y puerta de enlace de escritorio remoto se publicará como una única aplicación de forma que pueda tener una experiencia de inicio de sesión única entre aplicaciones de hello dos.

- Ya debe tener [RDS implementados](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) y el [proxy de aplicación habilitado](active-directory-application-proxy-enable.md).

- Este escenario se supone que los usuarios finales se vaya a través de Internet Explorer en los escritorios de Windows 7 o Windows 10 que se conectan a través de la página Web de escritorio remoto de Hola. Si necesita toosupport otros sistemas operativos, consulte [compatibilidad con otras configuraciones de cliente](#support-for-other-client-configurations).

  >[!NOTE]
  >La actualización del creador de Windows 10 no se admite actualmente.

- En Internet Explorer, habilite complementos de ActiveX RDS Hola.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Implementar Hola joint escenario RDS y Proxy de aplicación

Después de configurar el Proxy de aplicación de Azure AD para su entorno y de RDS, siga dos soluciones de hello pasos toocombine Hola. Estos pasos se describe a través de extremos de publicación Hola dos web orientado RDS (Web de escritorio remoto y puerta de enlace de escritorio remoto) como aplicaciones y, a continuación, dirigir el tráfico en su toogo RDS a través de Proxy de aplicación.

### <a name="publish-hello-rd-host-endpoint"></a>Publicar el extremo de host de escritorio remoto de Hola

1. [Publicar una nueva aplicación de Proxy de aplicación](application-proxy-publish-azure-portal.md) con hello siguientes valores:
   - Dirección URL interna: https://\<rdhost\>.com /, donde \<rdhost\> es Hola raíz común que comparten Web de escritorio remoto y puerta de enlace de escritorio remoto.
   - Dirección URL externa: Este campo se rellena automáticamente basándose en nombre hello aplicación hello, pero puede modificarlo. Los usuarios irá toothis URL cuando acceden a RDS.
   - Método de autenticación previa: Azure Active Directory
   - Traducir URL en encabezados: no
2. Asignar usuarios toohello publicó la aplicación de escritorio remoto. Asegúrese de que todos ellos tienen acceso tooRDS, también.
3. Leave Hola único inicio de sesión (método) para la aplicación hello como **Azure AD inicio de sesión único deshabilitado**. Los usuarios son más frecuentes tooauthenticate una vez tooAzure AD y una vez tooRD Web, pero tienen único inicio de sesión tooRD puerta de enlace.
4. Vaya demasiado**Azure Active Directory** > **registros de aplicaciones** > *la aplicación* > **deconfiguración**.
5. Seleccione **propiedades** actualización hello y **dirección URL de la página de inicio** punto de conexión de campo toopoint tooyour Web de escritorio remoto (como https://\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Dirigir el tráfico RDS tooApplication Proxy

Conectar la implementación de RDS toohello como administrador y cambie el nombre del servidor de puerta de enlace de escritorio remoto de hello para la implementación de Hola. Esto garantiza que las conexiones se vayan a través de hello Proxy de aplicación de Azure AD.

1. Conecte toohello RDS servidor ejecutando el rol de agente de conexión a Escritorio remoto de Hola.
2. Inicie **Administrador del servidor**.
3. Seleccione **servicios de escritorio remoto** desde panel Hola Hola izquierda.
4. Seleccione **Información general**.
5. En la sección información general de la implementación de hello, seleccione el menú desplegable de Hola y elija **editar propiedades de implementación**.
6. En la ficha de la puerta de enlace de escritorio remoto de hello, cambie hello **nombre del servidor** campo toohello dirección URL externa que establecen en el extremo de host de escritorio remoto de Hola de Proxy de aplicación.
7. Hola de cambio **método de inicio de sesión** campo demasiado**autenticación de contraseña**.

  ![Pantalla Propiedades de implementación de RDS](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Para cada colección, ejecute el siguiente comando de Hola. Reemplace  *\<yourcollectionname\>*  y  *\<proxyfrontendurl\>*  por su propia información. Este comando habilita el inicio de sesión único entre Acceso web de Escritorio remoto y Puerta de enlace de Escritorio remoto, además de optimizar el rendimiento:

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Por ejemplo:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. modificación de hello tooverify de propiedades personalizadas de RDP de hello, así como ver Hola RDP contenido del archivo que se descargarán desde RDWeb para esta recopilación, ejecute el siguiente comando de hello:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Ahora que ha configurado el escritorio remoto, el Proxy de aplicación de Azure AD ha asumido como componente de conexión a internet de Hola de RDS. Puede quitar Hola otros puntos de conexión a través de internet públicas en los equipos de Web de escritorio remoto y puerta de enlace de escritorio remoto.

## <a name="test-hello-scenario"></a>Escenario de prueba de Hola

Escenario de hello con Internet Explorer en un Windows 7 o 10 equipo de prueba.

1. Vaya a configurar la URL externa toohello o busque su aplicación en hello [panel mis aplicaciones](https://myapps.microsoft.com).
2. Se le preguntará tooauthenticate tooAzure Active Directory. Usar una cuenta que se ha asignado toohello aplicación.
3. Se le preguntará tooauthenticate tooRD Web.
4. Una vez que la autenticación de RDS se realiza correctamente, puede seleccionar Hola escritorio o aplicación que desee y comenzar a trabajar.

## <a name="support-for-other-client-configurations"></a>Compatibilidad con otras configuraciones de cliente

configuración de Hola que se describe en este artículo es para los usuarios en Windows 7 o 10, con Internet Explorer más complementos de ActiveX RDS Hola. No obstante, en caso necesario, también se ofrece compatibilidad con otros sistemas operativos o exploradores. diferencia de Hello es en el método de autenticación de Hola que usar.

| Método de autenticación | Configuración de cliente compatible |
| --------------------- | ------------------------------ |
| Autenticación previa    | Windows 7/10 con Internet Explorer + complemento ActiveX de RDS |
| Acceso directo | Cualquier otro sistema operativo que admita la aplicación de escritorio remoto de Microsoft hello |

flujo de autenticación previa de Hello ofrece más ventajas de seguridad de flujo de paso a través de Hola. Con la autenticación previa puede aprovechar características de autenticación de Azure AD como el inicio de sesión único, el acceso condicional y la verificación en dos pasos para recursos locales. También garantiza que solo el tráfico autenticado alcance la red.

autenticación de paso a través de toouse, existe son solo dos modificaciones toohello pasos enumerados en este artículo:
1. En [publica el punto de conexión de escritorio remoto de hello host](#publish-the-rd-host-endpoint) el paso 1, establecer método de autenticación previa de hello demasiado**Passthrough**.
2. En [RDS directa tráfico tooApplication Proxy](#direct-rds-traffic-to-application-proxy), omita el paso 8 completamente.

## <a name="next-steps"></a>Pasos siguientes

[Habilitar acceso remoto tooSharePoint con el Proxy de aplicación de Azure AD](application-proxy-enable-remote-access-sharepoint.md)  
[Consideraciones de seguridad al obtener acceso a aplicaciones de forma remota con el proxy de aplicación de Azure AD](application-proxy-security-considerations.md)
