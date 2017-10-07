---
title: "Integración de registro con los registros de auditoría de Azure Active Directory aaaAzure | Documentos de Microsoft"
description: "Saber cómo tooinstall Hola servicio de integración de registro de Azure e integrar los registros de registros de auditoría de Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Integración de los registros de auditoría de Azure Active Directory

Los eventos de auditoría de Azure Active Directory (Azure AD) le ayudan a identificar las acciones con privilegios que se produjeron en Azure Active Directory. Puede ver Hola tipos de eventos que puede realizar un seguimiento mediante la revisión [eventos de informe de auditoría de Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Antes de intentar pasos hello en este artículo, debe revisar hello [Introducción](security-azure-log-integration-get-started.md) artículo y complete los pasos de Hola allí.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Registros de auditoría de Azure Active directory de pasos toointegrate

1. Abra el símbolo del sistema de Hola y ejecute este comando:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Ejecute este comando: 
 
   ``azlog createazureid``

   Este comando solicita el inicio de sesión de Azure. Hello comando, a continuación, crea un Azure Active Directory entidad de servicio en los inquilinos de hello Azure AD que hospedan Hola suscripciones de Azure en qué Hola ha iniciado la sesión de usuario es un administrador, un administrador o un propietario. comando Hola se producirá un error si usuario registrado hello es solo un usuario invitado en el inquilino de Azure AD Hola. TooAzure de autenticación se realiza a través de Azure AD. Crear a una entidad de servicio para la integración de registro de Azure crea Hola identidad de Azure AD que se da acceso tooread de las suscripciones de Azure.

3. Comando de ejecución Hola siguiente tooprovide el identificador del inquilino. Necesita a miembro de toobe del comando de hello inquilino admin rol toorun Hola.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Ejemplo:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Comprobar Hola después tooconfirm de carpetas que Hola archivos de JSON de registro de auditoría de Azure Active Directory se crea en ellas:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Hello vídeo siguiente muestra los pasos de hello tratados en este artículo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Para obtener instrucciones específicas para incluir información de hello en archivos JSON de hello en el sistema de administración (SIEM) de eventos e información de seguridad, póngase en contacto con su proveedor SIEM.

Ayuda de la Comunidad está disponible a través de hello [foro de MSDN de integración de Azure registro](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Este foro permite a los usuarios en hello Azure registro integración Comunidad toosupport entre sí con preguntas, respuestas, sugerencias y trucos. Además, equipo de integración de Azure registro de hello supervisa este foro y ayuda a siempre que sea posible.

También puede abrir una [solicitud de soporte técnico](../azure-supportability/how-to-create-azure-support-request.md). Seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la integración de registro de Azure, vea:

* [Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) (Microsoft Azure Log Integration para registros de Azure): Esta página del Centro de descarga proporciona información, los requisitos del sistema y las instrucciones de instalación de Azure Log Integration.
* [Introducción tooAzure registro integración](security-azure-log-integration-overview.md): este artículo explica tooAzure integración de registro, sus capacidades claves y su funcionamiento.
* [Pasos de configuración de socios comerciales](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): esta entrada de blog muestra cómo tooconfigure toowork de integración de registro de Azure con socios comerciales soluciones Splunk, HP ArcSight y IBM QRadar.
* [Preguntas más frecuentes sobre Azure Log Integration](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre Azure Log Integration.
* [Integración de las alertas del centro de seguridad con la integración de Azure registro](../security-center/security-center-integrating-alerts-with-log-integration.md): este artículo muestra cómo las alertas toosync centro de seguridad, junto con los eventos de seguridad de máquina virtual recopilados por diagnósticos de Azure y los registros de auditoría de Azure, con los análisis de registros o Solución SIEM.
* [Registros de auditoría de nuevas características para diagnósticos de Azure y Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta entrada de blog presenta tooAzure los registros de auditoría y otras características que le ayudarán a obtienen información sobre las operaciones de Hola de los recursos de Azure.
