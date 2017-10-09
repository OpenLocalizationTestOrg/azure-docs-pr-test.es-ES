---
title: "puertos del firewall aaaHow tooopen Hola necesarios para una aplicación de Proxy de aplicación | Documentos de Microsoft"
description: "Averiguar qué tooopen puertos para toowork de Proxy de aplicación de Azure AD Hola correctamente"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>¿Cómo tooopen Hola puertos de firewall necesarios para una aplicación de Proxy de aplicación

toosee una lista completa de los puertos de hello necesario y la función de Hola de cada puerto, consulte la sección de requisitos previos de Hola de hello [documentación del Proxy de aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). Tenga en cuenta que el proxy de aplicación solo usa puertos de salida.

También puede comprobar si tiene todos los puertos abiertos de hello necesario abrir hello [herramienta de prueba de puertos de conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) desde la red local. Cuanto mayor sea el número de marcas de verificación verdes, mayor será la resistencia. 

## <a name="app-proxy-regions"></a>Regiones de proxy de aplicación

Estamos trabajando en una forma toolet ya sabe cuáles de estas regiones necesita toobe verde para usted. Por ahora, asegúrese de que todas ellas lo estén. También se necesita Centro de EE. UU., independientemente de en qué región se encuentre.

toomake seguro Hola herramienta proporciona Hola resultados correctos, no olvide:

-   Abra la herramienta de hello en un explorador desde servidor hello donde esté instalado Hola conector.

-   Asegúrese de que cualquier tooyour aplicable de firewalls o servidores proxy conector también son aplicado toothis página. Esto puede hacerse en Internet Explorer, vaya demasiado**configuración**  - &gt; **opciones de Internet**  - &gt; **conexiones**  - &gt; **Configuración de Lan**. En esta página, verá el campo Hola "Use a Proxy Server para su LAN". Active esta casilla y coloca la dirección de proxy de hello en el campo de "Dirección" Hola.

## <a name="next-steps"></a>Pasos siguientes
[Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
