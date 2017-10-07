---
title: "Active Directory Reporting preguntas más frecuentes sobre aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre informes de Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Preguntas más frecuentes sobre informes de Azure Active Directory

Este artículo incluye toofrequently respuestas preguntas frecuentes (P+f) sobre los informes de Azure Active Directory.  
Para más información, vea [Informes de Azure Active Directory](active-directory-reporting-azure-portal.md). 

**P: ¿cuál es la retención de datos de Hola para los registros de actividad (auditoría y los inicios de sesión) en hello portal de Azure?** 

**R:** proporcionamos 7 días de datos para nuestros clientes libres y cambiando tooan Azure AD Premium 1 o 2 Premium licencia, puede tener acceso a datos para los días de too30. Para obtener más información sobre la retención, vea [Directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md).

--- 

**P: ¿cuánto tiempo tarda hasta que ven los datos de actividad de hello después de que se ha completado una tarea?**

**R:** registros de auditoría de actividad con una latencia comprendido entre 15 minutos tooan hora. Registros de actividad de inicio de sesión con una latencia comprendido entre 15 minutos para la mayoría de los registros y too2 horas para una serie de registros.

---

**P: ¿necesito toobe que una actividad de administrador global toosee hello inicia una sesión Hola Portal de Azure o tooget datos a través de hello API?**

**R**: No. Puede ser un **lector de seguridad**, un **Administrador de seguridad** o un **administrador Global** toosee datos en el Portal de Azure o accediendo a través de hello API de informes.

---

**P: ¿puedo obtener información de registro de actividad de Office 365 a través de hello portal de Azure?**

**R:** aunque actividad de Office 365 y recurso compartido de registros de actividad de Azure AD muchos recursos de directorio de hello, si desea que una vista completa de Hola registros de actividad de Office 365, debe pasar la información de registro de actividad de Office 365 tooget de toohello centro de administración de Office 365.

---


**P: ¿qué es la API utilizo tooget información acerca de los registros de actividad de Office 365?**

**R:** uso Hola API de administración de Office 365 tooaccess Hola [registros de actividad de Office 365 a través de una API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**P: ¿Cuántos registros puedo descargar de Azure Portal?**

**R:** puede descargar los registros de too120K de hello portal de Azure. Hola registros se ordenan por *más reciente* y de forma predeterminada, se obtienen los registros de hello K más reciente de 120. 

---

**P: ¿cuántos registros se pueden consultar a través de las actividades de hello API?**

**R:** puede consultar los registros de millones de too1 (si no utiliza el operador top de hello, que ordena el registro de hello más reciente). Si usa el operador de "top" Hola, puede consultar los registros de too500K. Puede encontrar las consultas de ejemplo de cómo toouse Hola API aquí [aquí](active-directory-reporting-api-getting-started.md).

---

**P: ¿Cómo puedo obtener una licencia Premium?**

**R:** vea [Introducción a Azure Active Directory Premium](active-directory-get-started-premium.md) para una pregunta de toothis de respuesta.

---

**P: ¿Cuándo se deberían ver los datos de actividades después de obtener una licencia Premium?**

**R:** si ya tiene datos de las actividades como una licencia gratuita, a continuación, puede ver Hola los mismos datos. Si no tiene ningún dato, tardará uno o dos días.

---

**P: ¿Puedo ver los datos del último mes después de obtener una licencia de Azure AD Premium?**

**R:** si ha cambiado recientemente tooa Premium versión (incluida una versión de prueba), puede ver los datos de too7 días inicialmente. Cuando se acumulan datos, verá los too30 días.

---

**P: ¿hay un evento de riesgo en la protección de identidad pero no veo un inicio de sesión correspondiente en hello todos los inicios de sesión. ¿Es normal?**

**R:** Sí, Identity Protection evalúa el riesgo de todos los flujos de autenticación si es interactivo o no interactivo. Sin embargo, el único informe de todos los inicios de sesión muestra hello solo inicios de sesión interactivos.

---

**P: ¿Cómo puedo descargar informes de "Usuarios marcan para su riesgo" hello en el portal de Azure?**

**R:** toodownload de opción de hello *usuarios marcan para su riesgo* pronto se agregará el informe.

---

**P: ¿cómo saber por qué un inicio de sesión o un usuario se marcó arriesgado Hola portal de Azure?**

**R:** clientes de edición Premium pueden obtener más información sobre Hola subyacente eventos de riesgo, haga clic en usuario de hello en "Usuarios marcan para su riesgo" o haciendo clic en "Arriesgados inicios de sesión de" Hola. Los clientes de edición gratuita y básica obtener usuarios en riesgo de toosee hello e inicios de sesión sin Hola subyacente información sobre eventos de riesgo.

---

**P: ¿cómo se calculan las direcciones IP en inicios de sesión de Hola y el informe de inicios de sesión riesgo?**

**R:** direcciones IP se emiten de forma que no hay ninguna conexión definitiva entre una dirección IP y dónde se encuentran físicamente equipo del Hola con esa dirección. Esto se complica por factores como proveedores de dispositivos móviles y las redes privadas virtuales emitir las direcciones IP de grupos centrales a menudo muy lejos de donde se usa realmente el dispositivo de cliente de Hola. Dados Hola anterior, la conversión de ubicación física del tooa de dirección IP es un esfuerzo en función de seguimientos, datos del registro, busque inversa SAI (UPS) y otra información. 

---
