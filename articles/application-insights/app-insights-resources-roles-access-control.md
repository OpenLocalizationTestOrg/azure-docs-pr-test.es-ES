---
title: aaaResources, roles y control de acceso en Azure Application Insights | Documentos de Microsoft
description: "Propietarios, colaboradores y lectores de las perspectivas de su organización."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Recursos, roles y control de acceso en Application Insights
Puede controlar quién ha leído y actualizar tooyour acceder a los datos en Azure [Application Insights][start], mediante el uso de [control de acceso basado en roles en Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Asignar acceso toousers Hola **grupo de recursos o suscripción** toowhich pertenece el recurso de aplicación - no está en el propio recurso Hola. Asignar Hola **colaborador de componente de Application Insights** rol. Esto garantiza uniforme control de acceso tooweb pruebas y las alertas junto con el recurso de aplicación. [Más información](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Recursos, grupos y suscripciones
En primer lugar, vamos a ver algunas definiciones:

* **Recurso** : una instancia de un servicio de Microsoft Azure. El recurso de Application Insights recopila, analiza y muestra los datos de telemetría de hello enviados desde la aplicación.  Otros tipos de recursos de Azure son aplicaciones web, bases de datos y máquinas virtuales.
  
    toosee sus recursos, abra hello [Portal de Azure][portal], inicie sesión y haga clic en todos los recursos. toofind un recurso, tipo de parte de su nombre en el campo de filtro de Hola.
  
    ![Enumeración de los recursos de Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Grupo de recursos** ] [ group] -tooone grupo pertenece de cada recurso. Un grupo es una práctica manera toomanage relacionados con recursos, especialmente para el control de acceso. Por ejemplo, en un recurso de grupo podría poner una aplicación Web, una aplicación de Application Insights recursos toomonitor hello y una tookeep de recursos de almacenamiento exporta datos.

    ![Elija Examinar, Grupos de recursos, y luego elija un grupo.](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Suscripción** ](https://manage.windowsazure.com) -toouse Application Insights u otros recursos de Azure, inicie sesión en tooan suscripción de Azure. Cada grupo de recursos pertenece tooone suscripción de Azure, donde puede seleccionar el paquete de precios y, si es una suscripción de la organización, elegir los miembros de Hola y sus permisos de acceso.
* [**Cuenta de Microsoft** ] [ account] -Hola nombre de usuario y la contraseña que usa toosign en tooMicrosoft Azure suscripciones, XBox Live, Outlook.com y otros servicios de Microsoft.

## <a name="access"></a>Controlar el acceso en el grupo de recursos de Hola
Es importante toounderstand que en recursos de toohello de suma que creó para la aplicación, hay también separar recursos ocultos para las alertas y las pruebas web. Únicamente son toohello adjunto mismo [grupo de recursos](#resource-group) que la aplicación. También podría haber colocado ahí otros servicios de Azure, como sitios web o almacenamiento.

![Recursos en Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

toocontrol tener acceso a recursos de toothese, por tanto, se recomienda:

* Controlar el acceso en hello **grupo de recursos o suscripción** nivel.
* Asignar Hola **colaborador de componente de aplicación visión** toousers de rol. Esto les permite tooedit las pruebas web, alertas y recursos de Application Insights, sin proporcionar acceso tooany otros servicios de grupo de Hola.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide acceso tooanother usuario
Debe tener la suscripción de toohello de derechos de propietario o grupo de recursos de Hola.

Hola usuario debe tener un [Account Microsoft][account], u obtener acceso a tootheir [Account Microsoft profesional](../active-directory/sign-up-organization.md). Puede proporcionar acceso tooindividuals y también los grupos de toouser definidos en Azure Active Directory.

#### <a name="navigate-toohello-resource-group"></a>Navegar por el grupo de recursos de toohello
Agregar usuario de hello no existe.

![En la hoja de recursos de la aplicación, abra Essentials, abrir el grupo de recursos de Hola y seleccionar Configuración/usuarios. Haga clic en Agregar.](./media/app-insights-resources-roles-access-control/01-add-user.png)

O bien, puede ascender a otro nivel y agregar Hola usuario toohello suscripción.

#### <a name="select-a-role"></a>Seleccione un rol.
![Seleccione un rol de usuario nuevo de Hola](./media/app-insights-resources-roles-access-control/03-role.png)

| Rol | En el grupo de recursos de Hola |
| --- | --- |
| Propietario |Puede cambiar cualquier cosa, incluido el acceso de usuario. |
| Colaborador |Puede editar cualquier cosa, incluidos todos los recursos. |
| colaborador de componentes de Application Insights |Puede editar alertas, pruebas web y recursos de Application Insights. |
| Lector |Puede ver, pero no puede cambiar nada. |

La "edición" incluye la creación, la eliminación y la actualización:

* Recursos
* Pruebas web
* Alertas
* Exportación continua

#### <a name="select-hello-user"></a>Seleccione usuario Hola

Si el usuario Hola que desea no está en el directorio de hello, puede invitar a cualquier persona con una cuenta de Microsoft.
(Si se usan servicios como Outlook.com, OneDrive, Windows Phone o XBox Live, se tiene una cuenta Microsoft).

## <a name="related-content"></a>Contenido relacionado

* [Control de acceso basado en rol de Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
