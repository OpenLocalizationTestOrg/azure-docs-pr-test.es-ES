---
title: "crear una aplicación de Proxy de aplicación de aaaProblem | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot problemas de creación de aplicaciones de Proxy de aplicación de portal de administración de AD de Azure de Hola"
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>Problema al crear una aplicación de proxy de aplicación 

A continuación son algunos de los problemas comunes de Hola se enfrentan los usuarios cuando se crea una nueva aplicación de proxy de aplicación.

## <a name="recommended-documents"></a>Documentos recomendados 

toolearn más acerca de cómo crear una aplicación de Proxy de aplicación a través de hello Portal de administración, consulte [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Si está siguiendo los pasos de hello en ese documento y obtiene un error al crear la aplicación hello, vea los detalles del error Hola para obtener información y sugerencias sobre cómo toofix Hola aplicación. La mayoría de los mensajes de error incluyen una sugerencia de corrección. 

## <a name="specific-things-toocheck"></a>Toocheck acciones específicas

tooavoid los errores comunes, compruebe que:

-   Es un administrador con permiso toocreate una aplicación de Proxy de aplicación

-   dirección URL interna de Hello es único

-   dirección URL externa de Hello es única

-   Hola direcciones URL de inicio con http o https y terminar con un "/"

-   dirección URL de Hello debe ser un nombre de dominio y no una dirección IP

mensaje de error de Hello debe aparecer en la esquina superior derecha de hello cuando se crea la aplicación hello. También puede seleccionar los mensajes de error de hello notificación icono toosee Hola.

   ![Mensaje de notificación](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Pasos siguientes
[Habilita el Proxy de aplicación en hello portal de Azure](active-directory-application-proxy-enable.md)
