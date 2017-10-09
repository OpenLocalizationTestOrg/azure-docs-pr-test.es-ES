---
title: "aplicaciones de Proxy de aplicación de Azure AD en los equipos de aaaAccess | Documentos de Microsoft"
description: "Utilice el Proxy de aplicación de Azure AD tooaccess la aplicación local a través de Microsoft Teams."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Acceso a aplicaciones locales a través de Microsoft Teams

Azure Proxy de aplicación de Active Directory proporciona un único inicio de sesión tooon aplicaciones locales con independencia de dónde se encuentre y Microsoft Teams optimiza sus esfuerzos de colaboración en un solo lugar. Integración de hello dos juntos significa que los usuarios puedan ser más productivos con sus compañeros de equipo en cualquier situación. 

Los usuarios pueden agregar canales de los equipos de nube aplicaciones tootheir [con pestañas](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), pero ¿qué ocurre si ese sitio de SharePoint o la herramienta de planeación todas utilizan está hospedado en local? Proxy de aplicación es la solución de Hola. Puede agregar las aplicaciones publicadas a través de Proxy de aplicación tootheir canales con Hola mismo direcciones URL externas siempre usan tooaccess sus aplicaciones de forma remota. Y como Proxy de aplicación autentica a través de Azure Active Directory, Hola misma experiencia de inicio de sesión único lleva a través de.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Instalar el conector del Proxy de aplicación de Hola y publicar la aplicación

Si no lo ha hecho ya, [configurar el Proxy de aplicación para el inquilino e instalar el conector de hello](active-directory-application-proxy-enable.md). A continuación, [publique la aplicación local](application-proxy-publish-azure-portal.md) para acceso remoto. Cuando publica la aplicación hello, tome nota de la dirección URL externa de hello porque los usuarios finales necesitan esa información cuando se agregan tooTeams de aplicación Hola.

Si ya tiene sus aplicaciones publicadas pero no recuerda sus direcciones URL externas, buscarlos en hello [portal de Azure](https://portal.azure.com). Inicie sesión en, a continuación, desplácese demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones** > Seleccionar la aplicación > **Proxy de aplicación**.

## <a name="add-your-app-tooteams"></a>Agregar la aplicación tooTeams

Una vez que publica la aplicación hello a través de Proxy de aplicación, que los usuarios sepan que puede agregar como una pestaña directamente en sus canales de los equipos. Haga que sigan estos tres pasos:

1. Navegue toohello los equipos de canal en el que desea tooadd esta aplicación y seleccionen  **+**  tooadd una pestaña.

   ![Seleccione Agregar una pestaña](./media/application-proxy-teams/add-tab.png)

2. Seleccione **sitio Web** de opciones de la pestaña de Hola.

   ![Incorporación de un sitio web](./media/application-proxy-teams/website.png)

3. Asigne un nombre de pestaña de Hola y establecer la dirección externa del Proxy de aplicación Hola URL toohello. 

   ![Configuración de la dirección URL y el nombre de la pestaña](./media/application-proxy-teams/tab-name-url.png)

Una vez que un miembro de un equipo agrega pestaña hello, muestra para todos los usuarios en el canal de Hola. Los usuarios que dispongan de acceso toohello aplicación obtendrán acceso de inicio de sesión único con credenciales de Hola que usan para Teams de Microsoft. Los usuarios que no dispongan de acceso toohello aplicación verán la pestaña de hello en los equipos, pero se bloquean hasta que otorgarles permisos toohello local aplicación y hello Azure versión publicada del portal de la aplicación hello. 

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo demasiado[publicar sitios de SharePoint locales](application-proxy-enable-remote-access-sharepoint.md) con Proxy de aplicación.
- Configurar la toouse aplicaciones [dominios personalizados](active-directory-application-proxy-custom-domains.md) para su dirección URL externa. 
