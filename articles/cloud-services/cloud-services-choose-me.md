---
title: opciones - servicios de nube de proceso aaaAzure | Documentos de Microsoft
description: "Obtenga información sobre cómo Azure hospeda las opciones y cómo funcionan: Servicio de aplicaciones, servicios en la nube y máquinas virtuales"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>¿Debo elegir los servicios en la nube o alguna otra opción?
¿Es la elección de hello de servicios en la nube para usted? Azure proporciona distintos modelos de hospedaje para ejecutar aplicaciones. Cada una de ellas ofrece un conjunto diferente de servicios, por lo que cuál que elija depende exactamente lo que está tratando de toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Información sobre los servicios en la nube
Los servicios en la nube son un ejemplo de [plataforma como servicio](https://azure.microsoft.com/overview/what-is-paas/) (PaaS). Al igual que [servicio de aplicaciones](../app-service-web/app-service-web-overview.md), esta tecnología es toosupport diseñado aplicaciones escalables y fiables y toooperate barato. Al igual que un servicio de aplicación se hospeda en máquinas virtuales, por lo que también son servicios en la nube, sin embargo, tener más control sobre hello las máquinas virtuales. Puede instalar su propio software en máquinas virtuales de Servicio en la nube y tener acceso remoto a ellas.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Más control también significa menos facilidad de uso. A menos que necesita opciones de control adicionales de hello, normalmente es más rápido y fácil tooget una aplicación web y ejecutan en aplicaciones Web en el servicio de aplicaciones en comparación con servicios de tooCloud.

Existen dos tipos de roles de servicio en la nube. Hello la única diferencia entre Hola dos es cómo se hospeda su rol en la máquina virtual de Hola.

* **Rol web**  
Implementa y hospeda automáticamente la aplicación a través de IIS.

* **Rol de trabajo**  
No usa IIS y ejecuta la aplicación independiente.

Por ejemplo, una aplicación simple podría utilizar solo un rol web, para dar servicio a un sitio web. Una aplicación más compleja podría usar un toohandle de rol web las solicitudes entrantes de los usuarios, a continuación, pasar las solicitudes en tooa el rol de trabajo para el procesamiento. (esta comunicación podría utilizar [Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) o [Azure Queues](../storage/common/storage-introduction.md)).

Como Hola sugiere la figura anterior, todas las máquinas virtuales de Hola en una sola aplicación que se ejecute en hello mismo servicio en la nube. Los usuarios acceso Hola aplicación a través de una única dirección IP pública, con las solicitudes automáticamente la carga equilibrada entre máquinas virtuales de la aplicación hello. plataforma de Hello [escala e implementa](cloud-services-how-to-scale.md) Hola máquinas virtuales en una aplicación de servicios en la nube de forma que evita un único punto de error de hardware.

Aunque las aplicaciones se ejecutan en máquinas virtuales, es importante toounderstand que los servicios de nube proporciona PaaS, no IaaS. Esta es una manera de toothink sobre él: con IaaS, como máquinas de virtuales de Azure, crear y configurar la aplicación se ejecuta en el entorno de Hola y después implementar la aplicación en este entorno. Es responsable de administrar gran parte de este mundo, hacer las cosas como la implementación de nuevas versiones revisadas del sistema operativo de hello en cada máquina virtual. En PaaS, por el contrario, es como si el entorno de hello ya existe. Lo único que toodo es implementar la aplicación. Administración de plataforma de Hola que se ejecuta, incluida la implementación de nuevas versiones del sistema operativo de hello, se administra para usted.

## <a name="scaling-and-management"></a>Escalado y administración
Con Servicios en la nube no se crean máquinas virtuales. En su lugar, proporcionar un archivo de configuración que informa de cuántas de cada uno de ellos lo desea, como Azure **tres instancias de rol de web** y **dos instancias de rol de trabajo**, y plataforma de hello las creará automáticamente.  Sigue siendo necesario que elija [qué tamaño](cloud-services-sizes-specs.md) deben tener esas máquinas virtuales (las opciones son las mismas que con las máquinas virtuales de Azure), pero no tiene que crearlas por sí mismo explícitamente. Si la aplicación necesita toohandle una carga mayor, puede pedir más máquinas virtuales y Azure crea esas instancias. Si se reduce la carga de hello, puede apagar esas instancias y detener pagar por ellos.

Una aplicación de servicios en la nube se realiza normalmente toousers disponible a través de un proceso de dos pasos. Un desarrollador primera [cargas Hola aplicación](cloud-services-how-to-create-deploy.md) toohello plataforma del área de ensayo. Cuando esté listo para desarrolladores de hello en vivo de la aplicación de hello toomake, usan almacenamiento provisional de hello Azure tooswap portal con producción. Esto [conmutador entre ensayo y producción](cloud-services-nodejs-stage-application.md) puede realizarse sin tiempo de inactividad, lo que permite que una aplicación en ejecución pueden tooa actualizado nueva versión sin afectar a sus usuarios.

## <a name="monitoring"></a>Supervisión
Servicios en la nube también brinda supervisión. Como máquinas de virtuales de Azure, se detecta un error al servidor físico y reinicia las máquinas virtuales de Hola que se estaban ejecutando en ese servidor en un equipo nuevo. Pero Servicios en la nube también detecta máquinas virtuales y aplicaciones con errores, no solo errores de hardware. A diferencia de las máquinas virtuales, tiene un agente en cada rol web y de trabajo y, por lo que es capaz de toostart nuevas máquinas virtuales e instancias de aplicación cuando se producen errores.

Hola naturaleza de PaaS de servicios en la nube tiene otras consecuencias, demasiado. Uno de hello más importante es que las aplicaciones basadas en esta tecnología deben escribirse toorun correctamente cuando se produce un error en cualquier instancia de rol web o de trabajo. tooachieve esto, una aplicación no debe mantener los servicios de nube de estado de sistema de archivos de sus propias máquinas virtuales de Hola. A diferencia de las máquinas virtuales creadas con máquinas virtuales de Azure, escrituras que se efectúen las máquinas virtuales de tooCloud servicios no son persistentes; No hay nada como un disco de datos de máquinas virtuales. En su lugar, una aplicación debe explícitamente los servicios de nube escribir tooSQL de estado de todas las bases de datos, blobs, tablas, o algún otro tipo de almacenamiento externo. Compilar aplicaciones de este modo hace que sean tooscale más fácil y más resistente toofailure, dos objetivos importantes de servicios en la nube.

## <a name="next-steps"></a>Pasos siguientes
[Crear una aplicación de servicio en la nube en .NET](cloud-services-dotnet-get-started.md)  
[Crear una aplicación de servicio en la nube en Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Crear una aplicación de servicio en la nube en PHP](../cloud-services-php-create-web-role.md)  
[Creación de una aplicación de servicio en la nube en Python](cloud-services-python-ptvs.md)

