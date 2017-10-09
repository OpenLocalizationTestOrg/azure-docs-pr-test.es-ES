---
title: aplicaciones administradas de aaaOverview de Azure | Documentos de Microsoft
description: Describe los conceptos de Hola para Azure aplicaciones administradas
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Introducción a las aplicaciones administradas de Azure

Los proveedores que utilizan Azure pueden ofrecer soluciones toocustomers alrededor de Hola a todos. Azure Marketplace es una galería que consta de cientos de plantillas complejas de múltiples recursos de proveedores propios y de terceros. En minutos, los clientes pueden implementar y empezar a usar aplicaciones de plataforma como servicio (PaaS) y de software como servicio (SaaS). 

Aunque Hola Marketplace proporciona una excelente manera de para los clientes tooquickly implementar una oferta, cliente de hello es responsable de mantener y actualizar soluciones de Hola. Más allá de facturación de imagen de máquina virtual de hello, los proveedores no cobran a los clientes para el uso de Hola de una aplicación. Además, los proveedores no pueden evitar que los clientes modifiquen los recursos de aplicaciones esenciales. Los proveedores también no pueden bloquear la propiedad toointellectual de acceso que componen una aplicación. Las aplicaciones administradas de Azure proporcionan soluciones para estos problemas. 

Una aplicación administrada es la plantilla de solución de tooa similar en hello Marketplace, con una diferencia clave. En una aplicación administrada, recursos de hello son aprovisionados tooa grupo de recursos administrado por el proveedor de Hola. grupo de recursos de Hello está presente en la suscripción del cliente de hello, pero una identidad en el inquilino del proveedor de hello tiene grupo de recursos de toohello de acceso.

## <a name="advantages-of-managed-applications"></a>Ventajas de las aplicaciones administradas

Administrar proveedores de servicios (MSP) de ISV, y los equipos de TI centrales corporativos pueden utilizar aplicaciones administradas toodeliver soluciones a través de Marketplace de Hola u Hola catálogo de servicios. Aunque los clientes implementar estas aplicaciones administradas en sus suscripciones, no tienen toomaintain, actualizar o darles servicio. Dado que los proveedores de administran y admiten aplicaciones de hello, los clientes no tienen toomanage de conocimiento de dominio específico de la aplicación toodevelop estas aplicaciones. Los clientes pueden adquirir automáticamente actualizaciones de la aplicación sin Hola necesidad tooworry sobre solución de problemas y diagnosticar problemas relacionados con las aplicaciones de Hola.

Para los fabricantes y proveedores, las aplicaciones administradas crean una infraestructura de toosell de canal y el software a través de hello Marketplace. Las aplicaciones administradas también proporcionan una manera tooattach servicios y clientes de tooAzure soporte operacional. Los proveedores pueden facturar a los clientes mediante el uso de hello sistema de facturación de Azure. Puede utilizar el ciclo de vida de plantillas toomanage Hola de aplicaciones implementadas. Estas soluciones son independientes y sealed toohello cliente, por lo que los fabricantes pueden proporcionar servicio de alta calidad. Este enfoque beneficia a los proveedores de PaaS y SaaS. También ayuda a los equipos corporativos plataforma central y los integradores de sistemas (SIs) que desee toopackage y revenden sus soluciones.

## <a name="managed-application-types"></a>Tipos de aplicaciones administradas
Las aplicaciones administradas de Azure son de dos tipos: del catálogo de servicios y de Marketplace.
 
### <a name="service-catalog"></a>Catálogo de servicios  

Con hello catálogo de servicios, los clientes pueden crear un catálogo de soluciones aprobadas para Azure toobe utilizados por personal de su organización. Mantener un catálogo de soluciones de ese tipo resulta útil para los equipos centrales de TI en las empresas. Cumplimiento de normas de hello catálogo tooensure con ciertos estándares de la organización pueden usar mientras proporcionan soluciones para sus organizaciones. Pueden controlar, actualizar y mantener estas aplicaciones. Los empleados pueden usar Hola catálogo tooeasily detectar abundancia de Hola de aplicaciones que se recomienda y aprobadas por los departamentos de TI. Los clientes ven aplicaciones del catálogo de servicios administrados de Hola que han creado. También puede ver hello las aplicaciones administradas que otras personas de su recurso compartido de la organización con ellos.
 
Para información sobre cómo publicar una aplicación administrada del catálogo de servicios, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).
 
Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).
 
### <a name="marketplace"></a>Marketplace

Las aplicaciones administradas están disponibles a través de Marketplace de Hola Hola portal de Azure. Después de que el proveedor de hello publica estas aplicaciones, están disponibles para todos los usuarios dentro o fuera de una organización tooconsume. Con este enfoque, MSP, ISV y SIs pueden ofrecer su soluciones tooall los clientes de Azure. Los clientes obtengan los beneficios de Hola de uso de estas soluciones complejas sin hello tooinvest de necesidad de comprender y mantener soluciones de Hola. 

Actualmente, los publicadores pueden hacer que sus ofertas estén disponibles como una aplicación administrada o como una plantilla de solución no administrada. componentes principales de Hello sobre la publicación de una aplicación administrada incluyen el archivo de plantilla de Hola y el archivo de definición de interfaz de usuario de Hola. archivo de plantilla de Hello describe los recursos de Hola que se ha aprovisionado. archivo de definición de interfaz de usuario de Hello describe cómo Hola necesarios entradas para el aprovisionamiento de estos recursos se muestran en el portal de Hola. Hola requiere archivos están empaquetados en un archivo .zip y cargar a través del portal de publicación de Hola.
 
Para obtener información acerca de cómo publicar un toohello de aplicación administrada Marketplace, vea [Azure administra las aplicaciones de hello Marketplace](managed-application-author-marketplace.md).

Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Conceptos clave

### <a name="managed-resource-group"></a>Grupo de recursos administrado
Hola grupo de recursos administrado es donde todo hello Azure se crean recursos que se aprovisionan en plantilla Hola. Por ejemplo, si el dispositivo de hello es toocreate usa una cuenta de almacenamiento, este grupo de recursos contiene recursos de cuenta de almacenamiento de Hola. No contiene recursos de dispositivo de Hola.

### <a name="appliance-package"></a>Paquete de aplicación
publicador de Hello crea un paquete que contiene los archivos de plantilla de Hola y el archivo de createUIDefinition Hola. En concreto, contiene Hola siguientes archivos:

- **applianceMainTemplate.json**: este archivo de plantilla define todos los recursos de hello aprovisionados por dispositivo de Hola. Este archivo es un archivo de plantilla normal que se usa recursos toocreate.

- **MainTemplate.json**: este archivo de plantilla define recursos de dispositivo de hello (Microsoft.Solutions/appliances). Una propiedad clave definida en este recurso es ManagedResourceGroupId. Esta propiedad indica qué grupo de recursos es toohost usado Hola recursos reales que se definen en applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: este archivo describe cómo se representa la interfaz de usuario necesario para los parámetros de hello definidos en la plantilla de Hola Hola.

### <a name="authorization"></a>Autorización
publicador de Hello debe especificar permisos de hello requeridos por los recursos de hello proveedor toomanage hello en nombre de cliente de Hola. Este permiso aplica toohello grupo de recursos administrados. Establecer Hola siguientes valores:

- **PrincipalID**: Hola identificador de Azure Active Directory (Azure AD) de usuario de hello, grupo o aplicación que se usa el grupo de recursos administrados de toohello de toogrant acceso. Este identificador pertenece a inquilino de toohello publisher.

- **RoleDefinitionID**: Hola identificador de Azure AD de hello rol asignado toohello anterior identificador de entidad Puede ser cualquiera de roles de Control de acceso basado en roles integrados de hello en inquilinos del Editor de Hola. Para más información, consulte [Roles integrados para el control de acceso basado en rol de Azure](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información acerca de la publicación de aplicaciones administradas de toohello Marketplace, vea [Azure administra las aplicaciones de hello Marketplace](managed-application-author-marketplace.md).
* Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).
* Para información sobre cómo publicar una aplicación administrada del catálogo de servicios, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).
* Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).
* toocreate un archivo de definición de interfaz de usuario, consulte [empezar a trabajar con CreateUiDefinition](managed-application-createuidefinition-overview.md).
