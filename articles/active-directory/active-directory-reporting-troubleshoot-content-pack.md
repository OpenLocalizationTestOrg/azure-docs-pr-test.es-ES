---
title: "Solución de errores de los paquetes de contenido de los registros de actividad de Azure Active Directory | Microsoft Docs"
description: Proporciona una lista de mensajes de error de hello actividad de Azure Active Directory content pack y pasos toofix ellos.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Solución de errores de los paquetes de contenido de los registros de actividad de Azure Active Directory 


Cuando se trabaja con hello paquete de contenido de Power BI para Azure Active Directory Preview, es posible que ejecute en hello siguientes errores: 

- [Error al actualizar](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Credenciales del origen de datos de errores tooupdate](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [La importación de datos tarda demasiado](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Este tema proporciona información acerca de posibles causas de Hola y cómo toofix estos errores.
 
## <a name="refresh-failed"></a>Error al actualizar 
 
**¿Cómo aparece este error**: correo electrónico desde Power BI o estado de error en el historial de actualización de Hola. 


| Causa | Cómo toofix |
| ---   | ---        |
| Actualizar errores pueden deberse al credenciales de Hola de los usuarios de hello conectar el paquete de contenido de toohello restablecer aún no se actualizan en configuración de conexión de Hola Hola de paquete de contenido de Hola de error. | En Power BI, busque Hola de conjunto de datos correspondiente toohello panel de registros de actividad de Azure Active Directory (registros de actividad de Azure Active Directory), elegir programar la actualización y, a continuación, escriba sus credenciales de Azure AD. |
| Una actualización puede producir un error debido a problemas de toodata Hola subyacente paquete de contenido. | Abra una incidencia de soporte técnico. Para obtener más información, consulte [cómo son compatibles con tooget para Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Credenciales del origen de datos de errores tooupdate 
 
**¿Cómo aparece este error**: en Power BI, cuando se conectan toohello paquete de contenido de registros (vista previa) de actividad de Azure Active Directory. 

| Causa | Cómo toofix |
| ---   | ---        |
| usuario que se conecta Hello es ni un administrador global ni un lector de seguridad o un administrador de seguridad. | Utilice una cuenta que sea un administrador global o un lector de seguridad o una seguridad admin tooaccess Hola los paquetes de contenido. |
| El inquilino no es Premium o no tiene al menos un usuario con un archivo de licencia Premium. | Abra una incidencia de soporte técnico. Para obtener más información, consulte [cómo son compatibles con tooget para Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>La importación de datos tarda demasiado 
 
**¿Cómo aparece este error**: en Power BI, una vez que se ha conectado el paquete de contenido, proceso de importación de datos de hello inicia tooprepare el panel de registro de actividad de Azure Active Directory. Verá un mensaje de bienvenida: "*importar datos...* "  

| Causa | Cómo toofix |
| ---   | ---        |
| Función tamaño Hola de su inquilino, este paso podría tardar entre unos minutos too30 minutos. | Tenga paciencia. Si mensaje hello no cambia tooshowing panel dentro de una hora, registre una incidencia de soporte técnico. Para obtener más información, consulte [cómo son compatibles con tooget para Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Pasos siguientes

Hola tooinstall paquete de contenido de Power BI para Azure Active Directory vista previa, haga clic en [aquí](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


