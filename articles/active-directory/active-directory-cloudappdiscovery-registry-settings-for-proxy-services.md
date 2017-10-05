---
title: "Configuración del Registro de Cloud App Discovery para servicios de proxy | Microsoft Docs"
description: El objetivo de este tema es proporcionarle los pasos que debe llevar a cabo para establecer el puerto requerido en los equipos que ejecutan el agente de Cloud App Discovery.
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Configuración del registro de Cloud App Discovery para los servicios de proxy
De forma predeterminada, el agente de Cloud App Discovery está configurado para usar solo los puertos 80 o 443. Si piensa instalar Cloud App Discovery en un entorno con un servidor proxy que usa un puerto personalizado (que no sea el 80 ni el 443), deberá configurar los agentes para usar dicho puerto. La configuración se basa en una clave del registro.

El objetivo de este tema es proporcionarle los pasos que debe llevar a cabo para establecer el puerto requerido en los equipos que ejecutan el agente de Cloud App Discovery.

**Para modificar el puerto que usa el equipo que ejecuta el agente de Cloud App Discovery, lleve a cabo los pasos siguientes:**

1. Inicie el editor del Registro. <br> ![Ejecute](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Vaya a o cree la siguiente clave del registro: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Cree un nuevo valor de **cadenas múltiples** denominado **Puertos**. ![Nuevo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Para abrir el cuadro de diálogo **Modificar cadenas múltiples** , haga doble clic en el valor Puertos.
5. En el cuadro de texto Datos de valor, escriba los siguientes valores y agregue todos los puertos personalizados que se usan en su organización:  <br><br>
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
6. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Modificar cadenas múltiples**.

**Recursos adicionales**

* [¿Cómo puedo detectar aplicaciones en la nube no sancionadas que se usan dentro de mi organización?](active-directory-cloudappdiscovery-whatis.md) 

