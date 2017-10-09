---
title: "aaaAuthenticate con API de REST de Mobile Engagement - configuración manual"
description: "Describe cómo toomanually configurar la autenticación para las API de REST de Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Autenticación con las API de REST de Mobile Engagement: configuración manual
Se trata de una documentación de apéndice demasiado[autenticar con las API de REST de Mobile Engagement](mobile-engagement-api-authentication.md). Asegúrese de que pueda leerse primer contexto de hello tooget. Describe una instalación única de forma alternativa toodo Hola sobre cómo configurar la autenticación para el uso de las API de REST de Mobile Engagement Hola Hola Portal de Azure. 

> [!NOTE]
> instrucciones de Hello siguientes se basan en el objeto [Guía de Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) y personalizar para lo que se requiere para la autenticación de las API de Mobile Engagement. Así que haga referencia tooit si desea toounderstand Hola pasos detalladamente. 
> 
> 

1. Inicio de sesión tooyour cuenta de Azure a través de hello [portal clásico](https://manage.windowsazure.com/).
2. Seleccione **Active Directory** en el panel izquierdo de Hola.
   
     ![seleccionar Active Directory][1]
3. Elija hello **predeterminada Active Directory** en el portal de Azure. 
   
     ![elegir directorio][2]
   
   > [!IMPORTANT]
   > Este enfoque funciona sólo cuando está trabajando en su cuenta de Active Directory de forma predeterminada Hola y no funcionará si está realizando en Active Directory que haya creado en su cuenta. 
   > 
   > 
4. las aplicaciones de hello tooview en el directorio, haga clic en **aplicaciones**.
   
     ![ver aplicaciones][3]
5. Haga clic en **AGREGAR**. 
   
     ![agregar aplicación][4]
6. Haga clic en **Agregar una aplicación que mi organización está desarrollando**
   
     ![nueva aplicación][5]
7. Rellene el nombre de aplicación hello y tipo de select Hola de aplicación como **aplicación WEB Y/O API de WEB** y haga clic en el botón siguiente Hola.
   
     ![aplicación de nombre][6]
8. Puede especificar direcciones URL ficticias en **URL DE INICIO DE SESIÓN** y **URI DE ID. DE APLICACIÓN**. No se usan en nuestro caso y no se validan las direcciones URL de Hola por sí mismos.  
   
     ![propiedades de la aplicación][7]
9. Al final de Hola de esto, tendrá una aplicación AAD con el nombre de hello indicadas anteriormente como Hola siguiente. Este es el **AD\_APP\_NAME** (anótelo).  
   
     ![nombre de la aplicación][8]
10. Haga clic en el nombre de la aplicación hello y haga clic en **configurar**.
    
      ![configurar aplicación ][9]
11. Tome nota de hello Id. de cliente que se usará como **cliente\_ID** de la API llama. 
    
     ![configurar aplicación ][10]
12. Desplácese hacia abajo toohello **claves** sección, agregue una clave con preferiblemente una duración de 2 años (caducidad) y haga clic en **guardar**. 
    
     ![configurar aplicación ][11]
13. Copiar inmediatamente valor Hola que se muestra para la clave de hello, ya que solo se muestra ahora y no se almacena por lo que no se mostrarán nunca más. Si se pierde, tendrá toogenerate una nueva clave. Se trata de hello **CLIENT_SECRET** de la API llama. 
    
     ![configurar aplicación ][12]
    
    > [!IMPORTANT]
    > Esta clave expirará final Hola de duración de Hola que especificó así toorenew seguro de Asegúrese de que cuanto tiempo hello en caso contrario, la autenticación de API dejará de funcionar. También puede eliminar y volver a crear esta clave si cree que se ha visto comprometida.
    > 
    > 
14. Haga clic en **ver EXTREMOS** botón ahora que abrirían hello **extremos de la aplicación** cuadro de diálogo. 
    
    ![][13]
15. Desde el cuadro de diálogo de extremos de la aplicación hello, copie hello **extremo de TOKEN de OAUTH 2.0**. 
    
    ![][14]
16. Este punto de conexión será en hello siguiente formulario donde hello GUID en la dirección URL de hello es su **TENANT_ID** por lo que tome nota del mismo: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Ahora se continuará tooconfigure permisos de hello en esta aplicación. Para que esto tendrá tooopen seguridad hello [portal de Azure](https://portal.azure.com). 
18. Haga clic en **grupos de recursos** y buscar hello **Mobile Engagement** grupo de recursos.  
    
    ![][15]
19. Haga clic en hello **Mobile Engagement** recurso de grupo del sistema y desplácese toohello **configuración** hoja aquí. 
    
    ![][16]
20. Haga clic en **usuarios** en Hola hoja de configuración y, a continuación, haga clic en **agregar** tooadd un usuario. 
    
    ![][17]
21. Haga clic en **Seleccionar un rol**
    
    ![][18]
22. Haga clic en **Propietario**
    
    ![][19]
23. Búsqueda de nombre de saludo de la aplicación **AD\_aplicación\_nombre** en el cuadro de búsqueda de Hola. No verá esto de forma predeterminada aquí. Una vez que encuentra, selecciónelo y haga clic en **seleccione** final Hola de hoja de Hola. 
    
    ![][20]
24. En hello **agregar acceso** hoja, se mostrará como **1 usuario, 0 grupos**. Haga clic en **Aceptar** acerca de este cambio de hello tooconfirm de hoja. 
    
    ![][21]

Ahora ha completado la configuración de AAD de hello necesario y son Hola de toocall conjunto de todas las API. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



