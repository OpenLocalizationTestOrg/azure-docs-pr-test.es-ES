---
title: "una aplicación de Proxy de aplicación del aaaHow tooconfigure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un configurar una aplicación de Proxy de aplicación en unos pocos pasos sencillos"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>¿Cómo tooconfigure una aplicación de Proxy de aplicación

En este artículo le ayudarán a toounderstand cómo tooconfigure una aplicación de Proxy de aplicación en Azure AD tooexpose su toohello de aplicaciones local en la nube.

## <a name="recommended-documents"></a>Documentos recomendados 

toolearn sobre configuraciones iniciales de Hola y la creación de una aplicación de Proxy de aplicación a través de hello Portal de administración, siga hello [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Para obtener más información sobre la configuración de conectores, consulte [habilitar Proxy de aplicación en el portal de Azure hello](active-directory-application-proxy-enable.md).

Para información sobre cómo cargar certificados y usar dominios personalizados, consulte [Uso de dominios personalizados en el proxy de la aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Crear hello las direcciones URL de configuración de la aplicación/hello

Si está siguiendo los pasos Hola Hola [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentación y se recibe un error al crear la aplicación hello, ver detalles de error de Hola para obtener información y sugerencias sobre cómo aplicación de hello toofix. La mayoría de los mensajes de error incluyen una sugerencia de corrección. tooavoid los errores comunes, compruebe que:

-   Es un administrador con permiso toocreate una aplicación de Proxy de aplicación

-   dirección URL interna de Hello es único

-   dirección URL externa de Hello es única

-   Hola direcciones URL de inicio con http o https y terminar con un "/"

-   dirección URL de Hello debe ser un nombre de dominio, no una dirección IP

mensaje de error de Hello debe aparecer en la esquina superior derecha de hello cuando se crea la aplicación hello. También puede seleccionar los mensajes de error de hello notificación icono toosee Hola.

   ![Mensaje de notificación](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Configuración de conectores y grupos de conectores

Si tiene dificultades para la configuración de la aplicación debido a la advertencia sobre los conectores de Hola y grupos de conectores, consulte las instrucciones sobre cómo habilitar el Proxy de aplicación para obtener más información acerca de cómo los conectores de toodownload. Si desea más información acerca de los conectores de toolearn, vea hello [documentación conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Si los conectores están inactivos, esto significa que son servicios de hello tooreach no se puede. Esto suele ocurrir porque todos los puertos de hello necesario no están abiertos. toosee una lista de los puertos necesarios, vea la sección de requisitos previos de Hola de hello habilitar la documentación de Proxy de aplicación.

## <a name="upload-certificates-for-custom-domains"></a>Carga de certificados para dominios personalizados

Dominios personalizados permiten dominio de hello toospecify de las direcciones URL externas. toouse dominios personalizados, necesita tooupload Hola certificado para ese dominio. Para información sobre cómo usar certificados y dominios personalizados, consulte [Uso de dominios personalizados en el proxy de la aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Si se están produciendo problemas al cargar el certificado, busque mensajes de error de hello en el portal de Hola para obtener información adicional sobre el problema de hello con el certificado de Hola. Algunos problemas habituales con los certificados son:

-   Certificado expirado

-   Certificado autofirmado

-   El certificado no tiene clave privada de Hola

presentación de mensajes de error de Hello en hello esquina superior derecha cuando intente certificado de hello tooupload. También puede seleccionar los mensajes de error de hello notificación icono toosee Hola.

   ![Mensaje de notificación](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Pasos siguientes
[Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md)
