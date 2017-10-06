---
title: "aaaIntro tooauthentication en automatización de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información general de seguridad de automatización y Hola distintos métodos de autenticación disponibles para las cuentas de automatización en automatización de Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "seguridad de automatización, automatización segura; autenticación de automatización"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Introducción tooauthentication en automatización de Azure  
Automatización de Azure permite tooautomate tareas con los recursos en Azure, de forma local y con otros proveedores de nube, como Amazon Web Services (AWS).  En orden para un runbook tooperform las acciones necesarias, deben tener permisos toosecurely acceso Hola recursos tenga derechos mínimos Hola requeridos dentro de la suscripción de Hola.

En este artículo se tratan Hola admiten diversos escenarios de autenticación mediante la automatización de Azure y deberá mostrar cómo comenzar tooget basándose en el entorno de Hola o en entornos que se haya toomanage.  

## <a name="automation-account-overview"></a>Información general sobre las cuentas de Automatización
Al iniciar automatización de Azure por hello primera vez, debe crear al menos una cuenta de automatización. Las cuentas de automatización permiten tooisolate Hola a los recursos de automatización (runbooks, activos, las configuraciones) de recursos que contiene otras cuentas de automatización. Puede usar recursos de tooseparate de cuentas de automatización en entornos lógicos independientes. Por ejemplo, puede usar una cuenta para desarrollo, otra para producción y otra para su entorno local.  Una cuenta de Automatización de Azure es diferente de su cuenta Microsoft o de las cuentas creadas en su suscripción de Azure.

recursos de automatización de Hola para cada cuenta de automatización están asociados con una sola región de Azure, pero las cuentas de automatización pueden administrar todos los recursos de hello en su suscripción. cuentas de automatización de Hello motivo principal toocreate en diferentes regiones sería si tiene directivas que requieran datos y recursos toobe tooa aislado específico la región.

> [!NOTE]
> Cuentas de automatización y recursos Hola contienen que se crean en hello portal de Azure, no son accesibles en hello portal de Azure clásico. Si desea que toomanage estas cuentas o sus recursos con Windows PowerShell, debe usar módulos de hello Azure Resource Manager.
>

Todas las tareas de Hola que llevar a cabo con los recursos en la automatización de Azure de hello cmdlets de Azure y Azure Resource Manager deben autenticarse tooAzure con autenticación de basada en credenciales de identidad organizativa de Azure Active Directory.  Autenticación basada en certificado era Hola de método de autenticación original con el modo de administración de servicios de Azure, pero fue toosetup complicada.  Autenticar tooAzure con el usuario de Azure AD se copia se ha introducido en 2014 toonot solo simplificar Hola proceso tooconfigure una cuenta de autenticación, sino que también compatibilidad Hola capacidad toonon interactivamente autenticar tooAzure con una única cuenta de usuario que ha trabajado con el Administrador de recursos de Azure y los recursos clásicos.   

Actualmente cuando se crea una nueva cuenta de automatización en hello portal de Azure, se crean automáticamente:

* Cuenta de ejecución que se crea una nueva entidad de servicio en Azure Active Directory, un certificado y asigna el control de acceso basado en roles de colaborador de hello (RBAC), que será recursos del Administrador de recursos de toomanage uso de runbooks que se utilizan.
* Clásico cuenta de ejecución mediante la carga de un certificado de administración, que serán utilizado toomanage administración de servicios de Azure o los recursos clásicos mediante runbooks.  

Control de acceso basado en roles está disponible con toogrant de Azure Resource Manager permite la cuenta de usuario de Azure AD de acciones tooan y cuenta de ejecución y autenticar esa entidad de seguridad de servicio.  Lea [el control de acceso basado en roles en el artículo de automatización de Azure](automation-role-based-access-control.md) para obtener más información toohelp desarrolle su modelo para administrar permisos de automatización.  

Runbooks que se ejecutan en un Hybrid Runbook Worker en su centro de datos o en servicios de AWS informáticos no puede usar Hola mismo método que se utiliza normalmente para runbooks autenticar tooAzure recursos.  Esto es porque esos recursos se ejecutan fuera de Azure y por lo tanto, será necesario sus propias credenciales de seguridad definidas en tooresources tooauthenticate de automatización que tendrá acceso localmente.  

## <a name="authentication-methods"></a>Métodos de autenticación
Hello tabla siguiente resumen Hola distintos métodos de autenticación para cada entorno compatible con automatización de Azure y Hola artículo que describe cómo toosetup la autenticación para los runbooks.

| Método | Environment | Artículo |
| --- | --- | --- |
| Cuenta de usuario de Azure AD |Administración de recursos de Azure y Administrador de servicios de Azure |[Autenticación de Runbooks con una cuenta de usuario de Azure AD](automation-create-aduser-account.md) |
| Cuenta de ejecución de Azure |Administrador de recursos de Azure |[Autenticación de Runbooks con una cuenta de ejecución de Azure](automation-sec-configure-azure-runas-account.md) |
| Cuenta de ejecución de Azure clásico |Azure Service Management |[Autenticación de Runbooks con una cuenta de ejecución de Azure](automation-sec-configure-azure-runas-account.md) |
| Autenticación de Windows |Centro de datos local |[Autenticación de Runbooks para Hybrid Runbook Worker](automation-hybrid-runbook-worker.md) |
| Credenciales de AWS |Amazon Web Services |[Autenticación de Runbooks con Amazon Web Services (AWS)](automation-config-aws-account.md) |
