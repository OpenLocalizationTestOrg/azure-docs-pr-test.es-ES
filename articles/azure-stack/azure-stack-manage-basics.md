---
title: "conceptos básicos de administración de pila aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de lo que necesita tooknow tooadminister pila de Azure."
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
ms.openlocfilehash: cdf2818e9fc819b448508ca52bbdbec259890265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-administration-basics"></a>Aspectos básicos de administración de Azure Stack

Hay varias cosas que debe tooknow Soy nuevo tooAzure administración de la pila. Esta guía proporciona información general de la función como un operador en la nube y lo que necesita tootell a los usuarios les toobecome productivo rápidamente.

## <a name="understand-development-kit-builds"></a>Comprender las compilaciones del kit de desarrollo

Hola de revisión [¿qué es Azure pila?](azure-stack-poc.md) toomake artículo debe comprender el propósito de Hola de hello Kit de desarrollo de pila de Azure y sus limitaciones. Debe usar el kit de desarrollo de Hola como un "recinto", donde puede evaluar la pila de Azure y desarrollar y probar sus aplicaciones en un entorno no productivo. (Para obtener información de implementación, vea hello [implementación del Kit de desarrollo de Azure pila](azure-stack-deploy-overview.md) inicio rápido.)

Como Azure, innovamos con rapidez. Publicaremos nuevas compilaciones con asiduidad. Cuando quiera toomove toohello última compilación, debe [volver a implementar Azure pila](azure-stack-redeploy.md). Este proceso lleva tiempo, pero ventaja de hello es que puede probar características más recientes de Hola. documentación de Hello en nuestro sitio Web refleja la compilación de versión más reciente de Hola.

## <a name="learn-about-available-services"></a>Información sobre los servicios disponibles

Necesitará un reconocimiento de los servicios que puede hacer que los usuarios de tooyour disponible. Azure Stack admite un subconjunto de servicios de Azure. lista de Hello de servicios compatibles seguirán tooevolve.

**Servicios fundamentales**

De forma predeterminada, la pila de Azure incluye Hola después de "servicios fundamentales" cuando se implementa la pila de Azure:

- Proceso
- Storage
- Redes
- Key Vault

Con estos servicios fundamentales, puede ofrecer a los usuarios de infraestructura como-servicio (IaaS) tooyour con una configuración mínima.

**Servicios adicionales**

Actualmente, se admite Hola después de los servicios de plataforma como-servicio (PaaS) adicionales:

- App Service
- Funciones de Azure
- Bases de datos SQL y MySQL

Estos servicios requieren configuración adicional para poder realizar los usuarios de tooyour disponible. Para obtener más información, consulte las secciones de "cómo tooguides\Offer servicios" de Hola de nuestra documentación y tutoriales"Hola".

**Mapa de ruta de los servicios**

Pila Azure seguirá tooadd compatibilidad con los servicios de Azure. Para esquema de hello proyectado, vea hello [innovación de aplicaciones híbridas con Azure y Azure pila](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) notas del producto. También puede supervisar hello [entradas de blog de Azure pila](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) para anuncios de nuevo.

## <a name="what-tools-do-i-use-toomanage"></a>¿Qué herramientas usar toomanage?
 
Puede usar hello [portal del administrador](azure-stack-manage-portals.md) o PowerShell toomanage pila de Azure. conceptos básicos de Hello más fáciles manera toolearn hello es a través del portal de Hola. Si desea toouse PowerShell, hay pasos de preparación. Debe [instalar](azure-stack-powershell-install.md) PowerShell, [descargar](azure-stack-powershell-download.md) módulos adicionales y [configurar](azure-stack-powershell-configure-admin.md) PowerShell.

Azure Stack usa Azure Resource Manager como mecanismo subyacente de implementación, administración y organización. Si se va a toomanage pila de Azure y ayudan a los usuarios de soporte técnico, debe obtener información sobre el Administrador de recursos. Vea hello [introducción con el Administrador de recursos de Azure](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) notas del producto.

## <a name="your-typical-responsibilities"></a>Sus responsabilidades típicas

Los usuarios desean toouse servicios. Desde su perspectiva, su función principal es toomake estos servicios toothem disponible. Debe decidir qué toooffer de servicios y hacer que dichos servicios disponibles mediante la creación de [cuotas](azure-stack-setting-quotas.md), [planes](azure-stack-create-plan.md), y [ofrece](azure-stack-create-offer.md). 

También necesitará tooadd elementos toohello marketplace, como las imágenes de máquina virtual. Hello más sencillo es demasiado[descargar elementos de marketplace de Azure tooAzure pila](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> Si desea tootest los planes, ofertas y servicios, debe usar hello [portal de usuarios](azure-stack-manage-portals.md); no portal del Administrador de Hola.

En los servicios de tooproviding adición, debe realizar todas las tareas normales de Hola de un tookeep de operador en la nube Azure pila activados y ejecutándose. Estas tareas Hola siguientes:

- Agregar cuentas de usuario (para la implementación de [Azure Active Directory](azure-stack-add-new-user-aad.md) o de [Servicios de federación de Active Directory](azure-stack-add-users-adfs.md))
- [Asignar roles (RBAC) de control de acceso basado en roles](azure-stack-manage-permissions.md) (Esto no está restringido tooadministrators.)
- [Supervisar el estado de la infraestructura](azure-stack-monitor-health.md)
- Administrar los recursos de [red](azure-stack-viewing-public-ip-address-consumption.md) y [almacenamiento](azure-stack-manage-storage-accounts.md)
- Reemplazar el hardware defectuoso

## <a name="what-tootell-your-users"></a>¿Qué tootell los usuarios

Necesitará toolet que los usuarios sepan cómo toowork con servicios en la pila de Azure, entorno del kit de desarrollo de toohello tooconnect y cómo toosubscribe toooffers.

**Comprender cómo toowork con servicios en la pila de Azure**

Hay información que los usuarios deben comprender antes de usar los servicios y compilar aplicaciones en Azure Stack. Por ejemplo, existen requisitos específicos para las versiones de PowerShell y API. Además, existen algunas diferencias de características entre un servicio de Azure y el servicio equivalente de hello en la pila de Azure. Asegúrese de que los usuarios revisión Hola siguientes artículos:

- [Key considerations: Using services or building apps for Azure Stack](azure-stack-considerations.md) (Consideraciones clave: uso de servicios o compilación de aplicaciones para Azure Stack)
- [Consideraciones sobre máquinas virtuales en Azure Stack](azure-stack-vm-considerations.md)
- [Storage: differences and considerations](azure-stack-acs-differences-tp2.md) (Storage: diferencias y consideraciones)

información de Hello en estos artículos resume las diferencias de hello entre un servicio en Azure y la pila de Azure. Complementa la información de Hola que está disponible para un servicio de Azure en la documentación de Azure global Hola. 

**Conectar tooAzure pila como un usuario**

En un entorno de kit de desarrollo, si un usuario no tiene el host del kit de desarrollo de escritorio remoto acceso toohello, debe configurar una conexión de red privada virtual (VPN) antes de que puede obtener acceso a la pila de Azure. Vea [conectar tooAzure pila](azure-stack-connect-azure-stack.md). 

Los usuarios desearán tooknow cómo demasiado[portal de usuarios de acceso hello ](azure-stack-manage-portals.md) o cómo tooconnect a través de PowerShell. Si usa PowerShell, los usuarios pueden tener tooregister proveedores de recursos para poder usar los servicios. (Un proveedor de recursos administra un servicio. Por ejemplo, hello proveedor de recursos de red administra los recursos tales como redes virtuales, interfaces de red y los equilibradores de carga.) Debe [instalar](azure-stack-powershell-install.md) PowerShell, [descargar](azure-stack-powershell-download.md) módulos adicionales y [configurar](azure-stack-powershell-configure-user.md) PowerShell (que incluye el registro de proveedores de recursos).

**Suscribirse tooan oferta**

Antes de que un usuario puede tener acceso a servicios, pero deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que ha creado como un operador en la nube.

## <a name="where-tooget-support"></a>Donde se admite tooget

Para hello Kit de desarrollo de pila de Azure, puede hacer preguntas relacionadas con el soporte de hello [foros de Microsoft](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). Si hace clic Hola ayuda y soporte técnico de icono (signo de interrogación) en la esquina superior derecha de hello del portal de administrador de hello y, a continuación, haga clic en **nueva solicitud de soporte técnico**, esto abre el sitio de foros de hello directamente. Estos foros se supervisan periódicamente. Dado que el kit de desarrollo de hello es un entorno de evaluación, no hay ningún oficial de soporte técnico que ofrecen a través de servicios de admitir de cliente de Microsoft (CSS).

## <a name="next-steps"></a>Pasos siguientes

- [Administración de regiones en Azure Stack](azure-stack-region-management.md)


