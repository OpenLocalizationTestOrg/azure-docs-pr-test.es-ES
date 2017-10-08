---
title: "aaaProblems iniciar sesión en aplicaciones personalizadas de tooan | Documentos de Microsoft"
description: "Errores comunes que pudieron estar causando toonot ser capaz de toosign en una aplicación que haya desarrollado con Azure AD"
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
ms.openlocfilehash: cc302e68ae6c129b74387c6fc5ba4fb45ccb8fb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-custom-developed-application"></a>Problemas para iniciar sesión en aplicaciones personalizadas de tooan

Existen varios errores que podrían provocar toonot ser capaz de toosign en una aplicación. motivo mayor Hola personas produce este problema es mala configuración de aplicaciones.

## <a name="errors-related-too-misconfigured-apps"></a>Errores relacionados con aplicaciones demasiado mal configuradas

* Compruebe las configuraciones de hello en el portal de hello coincide con lo que tiene en su aplicación. En concreto, compare el identificador del cliente o aplicación, las direcciones URL de respuesta, las claves y secretos de cliente, y el URI del identificador de la aplicación.

* Comparar recursos Hola están solicitando acceso tooin código con permisos de hello configurado en hello **recursos necesarios** toomake ficha seguro solo solicitar recursos que haya configurado.

* Busque en [Azure AD en StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) errores o problemas similares.

## <a name="next-steps"></a>Pasos siguientes

[Guía del desarrollador de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[Integración de aplicaciones y consentimiento tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azure AD en StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory>)
