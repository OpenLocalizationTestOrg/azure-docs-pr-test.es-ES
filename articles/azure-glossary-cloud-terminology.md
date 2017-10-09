---
title: Glosario de aaaAzure - diccionario Azure | Documentos de Microsoft
description: "Utilice terminología de nube de hello Glosario de Azure toounderstand en hello plataforma Windows Azure. Este breve diccionario de Azure define algunos términos comunes de la nube para Azure."
keywords: "Diccionario de Azure, terminología de la nube, glosario de Azure, definiciones de terminología, términos de la nube"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Glosario de Microsoft Azure: un diccionario de la terminología de nube en hello plataforma Windows Azure

Glosario de Microsoft Azure Hello es un diccionario breve de la terminología de nube para hello plataforma Windows Azure. Consulte también:

* [Microsoft Azure y Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/): definiciones de los servicios de Azure y sus equivalentes de AWS.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Términos de informática en la nube](https://azure.microsoft.com/overview/cloud-computing-dictionary/): términos generales sobre informática en la nube.

## <a name="account"></a>cuenta
Una cuenta que ha utilizado tooaccess y administrar una suscripción de Azure. A menudo, dice tooas un Azure cuenta aunque una cuenta puede ser cualquiera de ellos: un trabajo existente, escuela, o personal cuenta Microsoft, o un nombre de usuario de Office 365 y contraseña. También puede crear una cuenta toomanage una suscripción de Azure cuando suscribe a hello [evaluación gratuita](https://azure.microsoft.com).  
Vea [registrarse para obtener una suscripción de Azure con su cuenta de Office 365](billing/billing-use-existing-office-365-account-azure-subscription.md) y [cuentas que pueda utilizar toosign en](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>Aplicación de API
Otro nombre para [aplicación de App Service](#app-service-app).

## <a name="app-service-app"></a>Aplicación de App Service
Hola recursos de proceso que [servicio de aplicaciones de Azure](app-service/app-service-value-prop-what-is.md) proporciona para hospedar un [aplicación web o sitio](app-service-web/app-service-web-overview.md), [web API](app-service-api/app-service-api-apps-why-best-platform.md), o [back-end de aplicación móvil](app-service-mobile/app-service-mobile-value-prop.md). Aplicaciones de servicio de aplicaciones también son que se hace referencia tooas *servicios de aplicaciones*, *aplicaciones web*, *aplicaciones de API*, y *aplicaciones móviles*.

## <a name="availability-set"></a>conjunto de disponibilidad
Una colección de máquinas virtuales que administra de manera conjunta de confiabilidad y redundancia de la aplicación tooprovide. uso de Hola de un conjunto de disponibilidad garantiza que durante un evento de mantenimiento planeado o no está disponible al menos una máquina virtual.  
Vea [administrar Hola disponibilidad de máquinas virtuales de Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [administrar Hola disponibilidad de máquinas virtuales de Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>modelo de implementación clásica de Azure
Uno de los dos [modelos de implementación](resource-manager-deployment-model.md) toodeploy recursos que se utilizan en Azure (Hola nuevo modelo es el Administrador de recursos de Azure). Algunos servicios de Azure admiten solo el modelo de implementación del Administrador de recursos de hello, algunos admiten solo el modelo de implementación clásica hello y algunos admiten ambos. documentación de Hola para cada servicio de Azure especifica qué modelos que admiten.

## <a name="cli"></a>Interfaz de la línea de comandos (CLI) de Azure
Una interfaz de línea de comandos que pueden ser toomanage usa servicios de Azure de Windows, Mac OS y Linux.  Algunos servicios o características del servicio se pueden administrar a través de PowerShell o CLI Hola. Consulte [CLI de Azure 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
Un toomanage de interfaz de línea de comandos de servicios de Azure a través de una línea de comandos de PC Windows. Algunos servicios o características del servicio se pueden administrar a través de PowerShell o CLI Hola.
Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>Modelo de implementación de Azure Resource Manager
Uno de los dos [modelos de implementación](resource-manager-deployment-model.md) toodeploy recursos que se utilizan en Microsoft Azure (Hola otro es el modelo de implementación clásica de hello). Algunos servicios de Azure admiten solo el modelo de implementación del Administrador de recursos de hello, algunos admiten solo el modelo de implementación clásica hello y algunos admiten ambos. documentación de Hola para cada servicio de Azure especifica qué modelos que admiten.

## <a name="fault-domain"></a>dominio de error
Hola colección de máquinas virtuales en un conjunto de disponibilidad que puede posiblemente producirá un error en hello mismo tiempo. Un ejemplo es un grupo de máquinas en bastidor que comparten una fuente de alimentación y un conmutador de red. En Azure, máquinas virtuales de hello en un conjunto de disponibilidad se separan automáticamente a través de varios dominios de error.  
Vea [administrar Hola disponibilidad de máquinas virtuales de Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [administrar Hola disponibilidad de máquinas virtuales de Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>geoárea
Un límite definido para la residencia de datos que normalmente contiene dos o más regiones. los límites de Hello pueden ser dentro o fuera de las fronteras nacionales y se ven afectados por la normativa de impuestos. Cada geoárea tiene al menos una región. Ejemplos de geoáreas son Asia Pacífico y Japón. Este concepto está relacionado con la *geografía*.  
Vea [Regiones de Azure](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>replicación geográfica
proceso de Hola de replicar automáticamente el contenido como blobs, tablas y colas dentro de un par regional.  
Vea [Replicación geográfica activa para Azure SQL Database](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>imagen
Un archivo que contiene sistema operativo de Hola y configuración de aplicaciones que puede ser utilizado toocreate cualquier número de máquinas virtuales. En Azure existen dos tipos de imágenes: imagen de máquina virtual e imagen de sistema operativo. Una imagen de VM incluye un sistema operativo y todos los discos conectados tooa virtual machine cuando se crea la imagen de Hola. Una imagen de sistema operativo contiene solo un sistema operativo generalizado sin configuraciones de disco de datos.  
Vea [navegar y seleccionadas imágenes de máquina virtual de Windows en Azure con PowerShell o hello CLI](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>límites
número de Hola de recursos que pueden crearse u Hola pruebas comparativas de rendimiento que se pueden lograr. Los límites se suelen asociar a las suscripciones, los servicios y las ofertas.  
Vea [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>load balancer
Un recurso que distribuye el tráfico entrante entre equipos en una red. En Azure, un equilibrador de carga distribuye máquinas de toovirtual tráfico definidas en un conjunto de equilibrador de carga. Un [equilibrador de carga](load-balancer/load-balancer-overview.md) puede ser accesible desde Internet o de uso interno.  

## <a name="mobile-app"></a>aplicación móvil
Otro nombre para [aplicación de App Service](#app-service-app).

## <a name="offer"></a>offer
precios de Hello, créditos y términos relacionados aplicable tooan suscripción de Azure.  
Vea hello [página de detalles de la oferta de Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portal
portal web segura de Hello usa toodeploy y administrar los servicios de Azure.  Hay dos portales: Hola [portal de Azure](http://portal.azure.com/) hello y [portal clásico](http://manage.windowsazure.com/). Algunos servicios están disponibles en ambos portales, mientras que otras solo están disponibles en uno u Hola sí. Hola [gráfico de disponibilidad de portal de Azure](https://azure.microsoft.com/features/azure-portal/availability/) muestra los servicios que están disponibles en el portal.

## <a name="region"></a>region
Un área dentro de una geoárea que no traspasa las fronteras nacionales y contiene uno o varios centros de datos. Precios, servicios regionales y tipos de oferta se exponen en el nivel de la región de Hola. Normalmente, una región se empareja con otra región, que puede ser una tooseveral cientos millas. Las parejas regionales pueden utilizarse como un mecanismo para escenarios de alta disponibilidad y recuperación ante desastres. También denominada tooas *ubicación*.  
Vea [Regiones de Azure](best-practices-availability-paired-regions.md)

## <a name="resource"></a>resource
Un elemento que forma parte de la solución de Azure. Cada servicio de Azure permite a toodeploy diferentes tipos de recursos, como bases de datos o máquinas virtuales.   
Vea [Información general del Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>resource group
Un contenedor en Resource Manager que incluye los recursos relacionados de una aplicación. grupo de recursos de Hello puede incluir todos los recursos de Hola para una aplicación, o sólo aquellos recursos que lógicamente se agrupan juntos. Puede decidir cómo desea que los recursos de tooallocate tooresource grupos basan en lo que le resulte hello más conveniente para su organización.  
Vea [Información general del Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>plantilla de Resource Manager
Un archivo JSON de manera declarativa que define uno o varios recursos de Azure y que define las dependencias existentes entre Hola implementa recursos. plantilla de Hello puede ser usado toodeploy Hola recursos varias veces y de forma coherente.  
Vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>proveedor de recursos
Un servicio que proporciona recursos de hello puede implementar y administrar mediante el Administrador de recursos. Cada proveedor de recursos proporciona operaciones para trabajar con recursos de Hola que se implementan. Proveedores de recursos pueden obtenerse a través de hello portal de Azure, PowerShell de Azure y varios SDK de programación.  
Vea [Información general del Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>role
Un medio para controlar el acceso que se pueden asignar toousers, grupos y servicios. Los roles son tooperform capaz de acciones como crear, administrar y leer en recursos de Azure.  
Vea [RBAC: roles integrados](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>contrato de nivel de servicio (SLA)
acuerdo de Hola que describe los compromisos de Microsoft para el tiempo de actividad y la conectividad. Cada servicio de Azure tiene un acuerdo de nivel de servicio específico.  
Vea [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>firma de acceso compartido (SAS)
Una firma que permite el recurso de tooa de acceso de toogrant limitado, sin exponer su clave de cuenta. Por ejemplo, [el almacenamiento de Azure usa SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant tooobjects de acceso de cliente, como blobs. [Centro de IoT usa SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) telemetría de toogrant dispositivos permiso toosend.

## <a name="storage-account"></a>Cuenta de almacenamiento
Una cuenta que proporciona acceso a servicios de Azure Blob, cola, tabla y archivo de toohello en el almacenamiento de Azure. nombre de cuenta de almacenamiento de Hello define Hola espacio de nombres único para los objetos de datos de almacenamiento de Azure.  
Consulte [Acerca de las cuentas de Azure Storage](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>suscripción
Acuerdo de un cliente con Microsoft que les permite tooobtain Azure servicios. precios de suscripción de Hola y los términos relacionados son gobernadas por oferta Hola elegido para la suscripción de Hola.
Consulte [Contrato Microsoft Online Subscription](https://azure.microsoft.com/support/legal/subscription-agreement/) y [Asociación de las suscripciones de Azure con Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>etiqueta
Un término de indización que se permite que los recursos de toocategorize según los requisitos de tooyour para administrar o facturación. Cuando tenga un conjunto complejo de recursos, puede usar etiquetas toovisualize esos recursos en forma de Hola que le resulte hello más conveniente. Por ejemplo, podría etiquetar recursos que no sirven para una función similar en su organización o pertenecen toohello mismo departamento.  
Vea [mediante etiquetas tooorganize los recursos de Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>actualizar dominio
Hola colección de máquinas virtuales en un conjunto de disponibilidad que se actualizan con hello mismo tiempo. Máquinas virtuales en hello al mismo dominio de actualización se reinician juntas durante el mantenimiento planeado. Azure no reinicia nunca más de un dominio de actualización a la vez. También se conoce tooas un dominio de actualización.  
Vea [administrar Hola disponibilidad de máquinas virtuales de Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [administrar Hola disponibilidad de máquinas virtuales de Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>máquina virtual
Hola implementación de software de un equipo físico que ejecuta un sistema operativo. Varias máquinas virtuales se pueden ejecutar simultáneamente en Hola mismo hardware. En Azure, hay máquinas virtuales disponibles en diferentes tamaños.  
Consulte [Documentación sobre máquinas virtuales](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>extensión de máquina virtual
Un recurso que implemente comportamientos o características que ya sea ayudan a otros programas de trabajo o proporcionar capacidad de Hola para toointeract con un equipo en ejecución. Por ejemplo, podría utilizar tooreset de extensión de acceso a máquinas virtuales de Hola o modificar los valores de acceso remoto en una máquina virtual de Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Consulte [Acerca de las características y extensiones de las máquinas virtuales (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Acerca de las características y extensiones de las máquinas virtuales (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>red virtual
Una red que proporciona conectividad entre los recursos de Azure que se encuentra aislada del resto de inquilinos de Azure. Una [puerta de enlace de VPN de Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) le permite establecer conexiones entre redes virtuales y [entre una red virtual y una red local](vpn-gateway/vpn-gateway-plan-design.md). Puede controlar completamente bloques de direcciones IP de hello, configuración de DNS, las directivas de seguridad y tablas de rutas en una red virtual.  
Consulte [Información general sobre redes virtuales](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Aplicación web
Otro nombre para [aplicación de App Service](#app-service-app).

## <a name="see-also"></a>Otras referencias

* [Comience a usar Azure](https://azure.microsoft.com/get-started/)
* [Centro de recursos en la nube](https://azure.microsoft.com/resources/)  
* [Azure para aplicaciones empresariales](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure en su centro de datos](https://azure.microsoft.com/overview/business-apps-on-azure/)

