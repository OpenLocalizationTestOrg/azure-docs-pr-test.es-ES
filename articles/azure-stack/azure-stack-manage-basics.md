---
title: "Aspectos básicos de administración de Azure Stack | Microsoft Docs"
description: Aprenda lo necesario para administrar Azure Stack.
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 856738a7-1510-442a-88a8-d316c67c757c
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: twooley
ms.openlocfilehash: 73f2c739a792825ccccda39ca76abef2dd490808
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stack-administration-basics"></a>Aspectos básicos de administración de Azure Stack

Hay varias cosas que debe saber si no está familiarizado con la administración de Azure Stack. Esta guía proporciona información general sobre el rol como operador de nube, y lo que debe decir a los usuarios para que aumenten su productividad rápidamente.

## <a name="understand-development-kit-builds"></a>Comprender las compilaciones del kit de desarrollo

Revise el artículo [What is Azure Stack?](azure-stack-poc.md) (¿Qué es Azure Stack?) para asegurarse de comprender el propósito de Azure Stack Development Kit y sus limitaciones. Debe usar el kit de desarrollo como un “espacio aislado” donde puede evaluar Azure Stack, y desarrollar y probar sus aplicaciones en un entorno que no es de producción. Para obtener información de implementación, consulte [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md) (Guía de inicio rápido de implementación de Azure Stack Development Kit).

Como Azure, innovamos con rapidez. Publicaremos nuevas compilaciones con asiduidad. Cuando quiera pasar a la compilación más reciente, debe [volver a implementar Azure Stack](azure-stack-redeploy.md). Este proceso lleva tiempo, pero la ventaja es que puede probar las características más recientes. La documentación de nuestro sitio web hace referencia a la versión de compilación más reciente.

## <a name="learn-about-available-services"></a>Información sobre los servicios disponibles

Deberá saber qué servicios puede poner a disposición de los usuarios. Azure Stack admite un subconjunto de servicios de Azure. La lista de servicios admitidos continuará evolucionando.

**Servicios fundamentales**

De forma predeterminada, Azure Stack incluye los siguientes “servicios fundamentales” cuando se implementa Azure Stack:

- Proceso
- Storage
- Redes
- Key Vault

Con estos servicios fundamentales, puede ofrecer la infraestructura como servicio (IaaS) a los usuarios con una configuración mínima.

**Servicios adicionales**

Actualmente, se admiten los siguientes servicios de plataforma como servicio (PaaS) adicionales:

- App Service
- Funciones de Azure
- Bases de datos SQL y MySQL

Estos servicios requieren una configuración adicional para que pueda ponerlos a disposición de los usuarios. Para obtener más información, consulte las secciones “Tutoriales” y “Guías de procedimientos\Oferta de servicios” de la documentación.

**Mapa de ruta de los servicios**

Azure Stack continuará agregando compatibilidad con los servicios de Azure. Para obtener el mapa de ruta previsto, consulte las notas del producto [Hybrid Application Innovation with Azure and Azure Stack](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) (Innovación de aplicaciones híbridas con Azure y Azure Stack). También puede supervisar las [publicaciones de blog de Azure Stack](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) para conocer los nuevos anuncios.

## <a name="what-tools-do-i-use-to-manage"></a>¿Qué herramientas debo usar para la administración?
 
Puede usar el [portal de administración](azure-stack-manage-portals.md) o PowerShell para administrar Azure Stack. La manera más fácil de aprender los conceptos básicos es a través del portal. Si quiere usar PowerShell, existen algunos pasos preparatorios. Debe [instalar](azure-stack-powershell-install.md) PowerShell, [descargar](azure-stack-powershell-download.md) módulos adicionales y [configurar](azure-stack-powershell-configure-admin.md) PowerShell.

Azure Stack usa Azure Resource Manager como mecanismo subyacente de implementación, administración y organización. Si va a administrar Azure Stack y ayudar en el soporte técnico a los usuarios, debe obtener información sobre Resource Manager. Consulte las notas del producto [Getting Started with Azure Resource Manager](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) (Introducción a Azure Resource Manager).

## <a name="your-typical-responsibilities"></a>Sus responsabilidades típicas

Los usuarios quieren usar los servicios. Desde la perspectiva de estos, su rol principal es poner estos servicios a su disposición. Debe decidir qué servicios se deben ofrecer y poner dichos servicios a su disposición mediante la creación de [cuotas](azure-stack-setting-quotas.md), [planes](azure-stack-create-plan.md) y [ofertas](azure-stack-create-offer.md). 

También deberá agregar elementos al Marketplace, como imágenes de máquinas virtuales. La manera más fácil es [descargar elementos de Marketplace de Azure a Azure Stack](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> Si quiere probar los planes, las ofertas y los servicios, debe utilizar el [portal de usuarios](azure-stack-manage-portals.md), no el portal de administración.

Además de ofrecer servicios, debe realizar todas las tareas habituales de un operador de nube para mantener Azure Stack en funcionamiento. Estas tareas incluyen las siguientes:

- Agregar cuentas de usuario (para la implementación de [Azure Active Directory](azure-stack-add-new-user-aad.md) o de [Servicios de federación de Active Directory](azure-stack-add-users-adfs.md))
- [Asignar roles de control de acceso basado en roles (RBAC)](azure-stack-manage-permissions.md) (esto no se restringe a los administradores).
- [Supervisar el estado de la infraestructura](azure-stack-monitor-health.md)
- Administrar los recursos de [red](azure-stack-viewing-public-ip-address-consumption.md) y [almacenamiento](azure-stack-manage-storage-accounts.md)
- Reemplazar el hardware defectuoso

## <a name="what-to-tell-your-users"></a>Qué decirles a los usuarios

Deberá informar a los usuarios cómo trabajar con los servicios en Azure Stack, cómo conectarse con el entorno del kit de desarrollo y cómo suscribirse a las ofertas.

**Información sobre cómo trabajar con servicios en Azure Stack**

Hay información que los usuarios deben comprender antes de usar los servicios y compilar aplicaciones en Azure Stack. Por ejemplo, existen requisitos específicos para las versiones de PowerShell y API. Además, existen algunas diferencias de características entre un servicio en Azure y el servicio equivalente en Azure Stack. Asegúrese de que los usuarios consulten los siguientes artículos:

- [Key considerations: Using services or building apps for Azure Stack](azure-stack-considerations.md) (Consideraciones clave: uso de servicios o compilación de aplicaciones para Azure Stack)
- [Consideraciones sobre máquinas virtuales en Azure Stack](azure-stack-vm-considerations.md)
- [Storage: differences and considerations](azure-stack-acs-differences-tp2.md) (Storage: diferencias y consideraciones)

La información de estos artículos resume las diferencias entre un servicio en Azure y Azure Stack. Complementa la información disponible para un servicio de Azure en la documentación global de Azure. 

**Conexión a Azure Stack como usuario**

En un entorno del kit de desarrollo, si un usuario no tiene acceso del Escritorio remoto al host del kit de desarrollo, debe configurar una conexión de red privada virtual (VPN) para poder obtener acceso a Azure Stack. Consulte [Conexión a Azure Stack](azure-stack-connect-azure-stack.md). 

Los usuarios querrán saber cómo [acceder al portal de usuarios](azure-stack-manage-portals.md) o cómo conectarse a través de PowerShell. Si usa PowerShell, puede que los usuarios deban registrar proveedores de recursos para poder usar los servicios. (Un proveedor de recursos administra un servicio. Por ejemplo, el proveedor de recursos de red administra recursos, como redes virtuales, interfaces de red y equilibradores de carga). Debe [instalar](azure-stack-powershell-install.md) PowerShell, [descargar](azure-stack-powershell-download.md) módulos adicionales y [configurar](azure-stack-powershell-configure-user.md) PowerShell (que incluye el registro de proveedores de recursos).

**Suscripción a una oferta**

Para que un usuario puede tener acceso a los servicios, debe [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que usted haya creado como operador de nube.

## <a name="where-to-get-support"></a>Dónde obtener soporte técnico

Para Azure Stack Development Kit, puede dirigir las preguntas relacionadas con el soporte técnico a los [foros de Microsoft](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). Si hace clic el icono de ayuda y soporte técnico (signo de interrogación) en la esquina superior derecha del portal de administración y, a continuación, hace clic en **Nueva solicitud de soporte técnico**, se abrirá el sitio de foros directamente. Estos foros se supervisan periódicamente. Dado que el kit de desarrollo es un entorno de evaluación, no se ofrece ningún soporte técnico oficial a través de los servicios de soporte técnico al cliente (CSS) de Microsoft.

## <a name="next-steps"></a>Pasos siguientes

- [Administración de regiones en Azure Stack](azure-stack-region-management.md)


