---
title: "Configuraciones de registro de detección de aplicación para los servicios de Proxy aaaCloud | Documentos de Microsoft"
description: objetivo de Hola de este tema es tooprovide a Hola lo necesita puerto tooperform tooset Hola necesario Hola ejecutan el agente de Cloud App Discovery de Hola.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Configuración del registro de Cloud App Discovery para los servicios de proxy
De forma predeterminada, el agente de Cloud App Discovery de hello es toouse configurado solo Hola puertos 80 o 443. Si piensa instalar Cloud App Discovery en un entorno con un servidor proxy que usa un puerto personalizado (ni 80 ni el 443), necesita tooconfigure su toouse agentes este puerto. configuración de Hola se basa en una clave del registro.

objetivo de Hola de este tema es tooprovide a Hola lo necesita puerto tooperform tooset Hola necesario Hola ejecutan el agente de Cloud App Discovery de Hola.

**puerto de hello toomodify usado por equipo de Hola que se ejecuta el agente de Cloud App Discovery de hello, lleve a cabo Hola pasos:**

1. Inicie el editor del registro de hello. <br> ![Ejecute](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Navegue tooor crear Hola después de la clave del registro: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Cree un nuevo valor de **cadenas múltiples** denominado **Puertos**. ![Nuevo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Hola tooopen **modificar cadenas múltiples** cuadro de diálogo, haga doble clic en el valor de puertos de Hola.
5. En el cuadro de texto de datos de valor de hello, escriba Hola después de valores y agregue todos los puertos personalizados que se usan en su organización: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Modificar cadenas múltiples](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Haga clic en **Aceptar** tooclose hello **modificar cadenas múltiples** cuadro de diálogo.

**Recursos adicionales**

* [¿Cómo puedo detectar aplicaciones en la nube no sancionadas que se usan dentro de mi organización?](active-directory-cloudappdiscovery-whatis.md) 

