---
title: aaaCommon preguntas acerca de Microsoft Azure Service Fabric | Documentos de Microsoft
description: "Preguntas más frecuentes acerca de Service Fabric y sus respuestas"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Preguntas frecuentes sobre Service Fabric

Hay muchas preguntas que se plantean con frecuencia acerca de qué puede hacer Service Fabric y cómo se debe usar. En este documento se incluyen muchas de esas preguntas y sus respuestas.

## <a name="cluster-setup-and-management"></a>Instalación y administración de clústeres

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>¿Puedo crear un clúster que abarque varias regiones de Azure o mis propios centros de datos?

Sí. 

núcleo de Hello tecnología de agrupación en clústeres de Service Fabric puede ser máquinas de toocombine usado ejecutando en ningún lugar de Hola a todos, siempre y cuando tienen red de conectividad tooeach otros. Sin embargo, compilar y ejecutar clústeres de este tipo puede resultar complicado.

Si está interesado en este escenario, le recomendamos tooget en contacto a través de hello [lista de problemas de Service Fabric Github](https://github.com/azure/service-fabric-issues) o a través de su representante de soporte técnico en instrucciones adicionales de orden tooobtain. equipo de Service Fabric Hola funciona una explicación adicional de tooprovide, instrucciones y recomendaciones para este escenario. 

Algunos tooconsider cosas: 

1. Hola recurso de clúster de Service Fabric en Azure hoy en día es regional, como son la escala de máquinas virtuales de hello establece ese clúster Hola se basa en. Esto significa que en caso de hello de un error regional puede perder el clúster de hello capacidad toomanage Hola a través de hello Azure Resource Manager u Hola Portal de Azure. Esto puede ocurrir aunque clúster Hola sigue ejecutándose y se pueda toointeract con él directamente. Además, Azure actualmente no ofrecen Hola capacidad toohave una única red virtual que se pueda usar en diferentes regiones. Esto significa que un clúster de varias regiones de Azure necesita las palabras clave [direcciones IP públicas para cada máquina virtual de hello conjuntos de escalas de VM](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) o [puertas de enlace de VPN de Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md). Estas opciones de red tengan efectos diferentes en diseño de aplicaciones de grado de costos, rendimiento y toosome, por lo que se requiere un cuidadoso análisis y planeación antes preparado tal entorno.
2. Hello mantenimiento, administración y supervisión de estas máquinas pueden llegar a complicarse, especialmente cuando se distribuye en _tipos_ de entornos, por ejemplo, como entre diferentes proveedores de nube o entre recursos locales y Azure . Se deben tener cuidado tooensure que actualiza, supervisión, administración y diagnóstico se entiende para clúster hello y aplicaciones de hello antes de ejecutar las cargas de trabajo de producción en un entorno de este tipo. Si ya tiene amplia experiencia en la resolución de estos problemas en Azure o dentro de sus propios centros de datos, es probable que esas mismas soluciones que utiliza se puedan aplicar al crear o ejecutar el clúster de Service Fabric. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>¿Los nodos de Service Fabric reciben automáticamente actualizaciones del sistema operativo?

No en la actualidad, pero también es una solicitud común que Azure pretende toodeliver.

Hola provisional, tenemos [proporciona una aplicación](service-fabric-patch-orchestration-application.md) que los sistemas operativos de hello debajo de los nodos de Service Fabric permanezcan revisado y seguridad toodate.

desafío de Hello con actualizaciones del sistema operativo es que normalmente requiere un reinicio de máquina de hello, lo que resulta en pérdida de disponibilidad temporal. Por sí mismo, que no es un problema, puesto que Service Fabric le redirigirá automáticamente el tráfico a los nodos de tooother de servicios. Sin embargo, si no se coordinan actualizaciones del sistema operativo en el clúster de hello, hay posibilidad de Hola que muchos nodos dejan de funcionar a la vez. Estos reinicios simultáneos pueden provocar la pérdida de disponibilidad completa para un servicio, o por lo menos para una partición específica (para un servicio con estado).

Hola futura, tenemos previsto directiva de actualización de toosupport un sistema operativo que está totalmente automatizada y coordinada entre dominios de actualización, asegurándose de que se mantiene la disponibilidad a pesar de los reinicios y otros errores inesperados.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>¿Puedo usar conjuntos de escalado grandes de máquinas virtuales en el clúster SF? 

**Respuesta corta**: no. 

**Responder a la larga** : aunque Hola grandes conjuntos de escalas de máquina Virtual le permiten tooscale una escala de máquinas virtuales establece hasta 1000 instancias de máquina virtual, lo hace mediante el uso de Hola de grupos de selección de ubicación (documento). Dominios de error (FD) y dominios de actualización (ud) solo son coherentes en un tejido de servicio de selección de ubicación grupo utiliza FD y ud toomake decisiones de selección de ubicación de las instancias de servicio/réplicas de servicio. Puesto que FD hello y ud es comparables solo dentro de un grupo de selección de ubicación SF no puede usarlo. Por ejemplo, si VM1 en PG1 tiene una topología de FD = 0 y VM9 en PG2 tiene una topología de FD = 4, no significa que VM1 y VM2 se encuentran en dos diferentes bastidores de Hardware, por lo tanto, SF no puede utilizar valores de hello FD este decisiones de selección de ubicación toomake mayúsculas.

Hay otros problemas con conjuntos de escalas de máquina virtual grande, como la compatibilidad de equilibrio de carga de falta de Hola de nivel 4. Consulte toofor [obtener más información sobre grande escala conjuntos](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>¿Cuál es el tamaño mínimo de Hola de un clúster de Service Fabric? ¿Por qué no puede ser menor?

tamaño mínimo de admitido Hola para un clúster de Service Fabric ejecutan cargas de trabajo de producción es cinco nodos. Para escenarios de desarrollo y prueba, se admiten los nodos de tres clústeres.

Estos mínimos existen como clúster de Service Fabric Hola ejecuta un conjunto de servicios del sistema con estado, incluido el servicio de nomenclatura de Hola y el Administrador de conmutación por error de Hola. Estos servicios, que realizar un seguimiento de servicios que han sido implementados toohello clúster y donde se aloja actualmente, dependen de homogeneidad. Esa coherencia fuerte, a su vez, depende de hello capacidad tooacquire una *quórum* para una actualización determinada toohello estado de esos servicios, donde un quórum representa una mayoría estricta de réplicas de hello (N/2 + 1) para un servicio determinado.

Con esta información, examinemos algunas posibles configuraciones de clúster:

**Un nodo**: esta opción no proporciona alta disponibilidad dado que la pérdida de Hola de nodo único de Hola por cualquier motivo significa pérdida de Hola de clúster completo Hola.

**Dos nodos**: un cuórum para un servicio implementado en dos nodos (N = 2) is 2 (2/2 + 1 = 2). Cuando se pierde una única réplica, resulta imposible toocreate un quórum. Teniendo en cuenta que realizar una actualización del servicio requiere desconectar una réplica, esta no es una configuración útil.

**Tres nodos**: con tres nodos (N = 3), Hola requisito toocreate un quórum sigue siendo dos nodos (3/2 + 1 = 2). Esto significa que se puede perder un solo nodo y continuar manteniendo el cuórum.

configuración del clúster de tres nodos de Hello es compatible con desarrollo/pruebas porque puede realizar las actualizaciones y sobreviven a errores en los nodos individuales, siempre y cuando no realizan de manera simultánea. Para las cargas de trabajo de producción, debe ser resistente toosuch un error simultáneo, por lo que se requieren cinco nodos.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>¿Puedo desactivar el clúster en los costos de toosave de noche/fines de semana?

En general, no. Service Fabric almacena el estado de los discos locales efímeros, lo que significa que si máquina virtual de hello es tooa movida otro host, Hola datos no se mueven con él. Durante el funcionamiento normal, que no es un problema como nuevo nodo de Hola se plantea toodate otros nodos. Sin embargo, si detiene todos los nodos y reiniciarlas una vez más adelante, hay una posibilidad significativa que la mayoría de nodos de hello inicia en nuevos hosts y realizar Hola sistema no se puede toorecover.

Si desea que los clústeres de toocreate para probar la aplicación antes de implementarla, le recomendamos que cree dinámicamente esos clústeres como parte de su [canalización de implementación continua/integración continua](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>¿Cómo puedo actualizar mi sistema operativo (por ejemplo, de Windows Server 2012 tooWindows Server 2016)?

Mientras estamos trabajando en una experiencia mejorada, en la actualidad, usted es responsable de la actualización de Hola. Debe actualizar la imagen de SO de hello en hello una máquina virtual de clúster de máquinas virtuales de Hola a la vez. 

## <a name="container-support"></a>Compatibilidad con contenedores

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>¿Por qué mi contenedores tooSF implementado no se puede tooresolve DNS direcciones?

Este problema se ha informado en los clústeres de la versión 5.6.204.9494 

**Mitigación** : siga [este documento](service-fabric-dnsservice.md) tooenable Hola DNS de servicio servicio de fabric en el clúster.

**Corregir** : tooa actualización admitida la versión de clúster que sea mayor de 5.6.204.9494, cuando esté disponible. Si el clúster se establece tooautomatic actualizaciones, clúster de Hola actualizará automáticamente versión toohello que tiene este problema fijo.

  
## <a name="application-design"></a>Diseño de aplicaciones

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>¿Qué es Hola mejor forma tooquery que los datos en particiones de una colección de confianza?

Suelen ser colecciones confiables [con particiones](service-fabric-concepts-partitioning.md) tooenable escalada de mayor rendimiento y la capacidad. Esto significa que el estado de Hola para un servicio determinado puede estar repartido por 10s o 100s de máquinas. operaciones de tooperform a través de ese conjunto de datos completo, tiene algunas opciones:

- Crear un servicio que realiza consultas en todas las particiones de otro toopull de servicio en los datos de hello necesario.
- Crear un servicio que puede recibir datos de todas las particiones de otro servicio.
- Insertar periódicamente los datos de cada almacén externo tooan del servicio. Este método solo es adecuado si va a realizar una de las consultas de hello no forman parte de la lógica de negocios básica.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>¿Qué es Hola mejor forma tooquery que los datos a través de mi actores?

Actores están diseñadas toobe unidades independientes del estado y proceso, por lo que no es recomienda tooperform extensas consultas de estado de actor en tiempo de ejecución. Si tiene una necesidad tooquery en el conjunto completo de Hola de estado de actor, debe considerar ya sea:

- Reemplazar los servicios de actor con los servicios de confianza con estado, tal que el número de Hola de red solicita toogather todos los datos de número de hello toohello de actores de particiones en el servicio.
- Diseñar la inserción de tooperiodically actores en su almacén externo tooan de estado para consultar más fácil. Como anteriormente, este método sólo es viable si las consultas de Hola que se va a realizar no son necesarias para su comportamiento en tiempo de ejecución.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>¿Qué cantidad de datos puedo almacenar en una instancia de Reliable Collection?

Servicios de confianza normalmente tienen particiones, por lo que cantidad Hola que puede almacenar solo está limitado por número de Hola de máquinas que tienen en clúster de Hola y Hola mucha memoria disponible en los equipos.

Por ejemplo, suponga que tiene una colección confiable de un servicio con 100 particiones y 3 réplicas, en donde se almacenan objetos que tienen un tamaño medio de 1 kB. Ahora suponga que tiene un clúster de 10 máquinas con 16 GB de memoria por máquina. Para mayor simplicidad y toobe muy conservador, suponga que sistema de operativo hello y servicios del sistema, en tiempo de ejecución de Service Fabric de Hola y los servicios de consumen 6gb de estas cosas, salir de 10gb disponibles por equipo, o 100gb para clúster Hola.

Teniendo en cuenta que cada objeto tiene que almacenarse tres veces (una principal y dos réplicas), debería tener suficiente memoria para aproximadamente 35 millones de objetos en la colección cuando se trabaja con la máxima capacidad. Sin embargo, se recomienda que se va a toohello resistente pérdida simultánea de un dominio de error y un dominio de actualización, que representa aproximadamente 1/3 de la capacidad y reduciría Hola número tooroughly millones de 23.

Tenga en cuenta que en este cálculo también se da por supuesto:

- Distribución de los datos entre particiones Hola Hola es aproximadamente uniforme o que está informando toohello de métricas de carga el Administrador de recursos de clúster. De forma predeterminada, Service Fabric equilibra la carga según el número de réplicas. En nuestro ejemplo anterior, que tendría que poner 10 réplicas principales y 20 réplicas secundarias en cada nodo de clúster de Hola. Eso funciona bien para la carga que se distribuye uniformemente a través de las particiones de Hola. Si carga no es par, debe notificar carga para que hello Administrador de recursos puede empaquetar réplicas más pequeñas y permitir mayor tooconsume réplicas más memoria en un nodo individual.

- Ese servicio confiable de hello en cuestión es un solo estado almacenar hello en clúster de Hola. Dado que puede implementar varios clústeres de tooa de servicios, deberá toobe prestar atención a los recursos de Hola que cada uno tendrá toorun y administrar su estado.

- Ese propio clúster hello no se están aumentando o disminuyendo. Si agrega más máquinas, Service Fabric se reequilibrar la capacidad adicional de réplicas tooleverage Hola hasta que el número de Hola de máquinas supera el número de Hola de particiones en el servicio, puesto que una réplica individual no puede abarcar varias máquinas. Por el contrario, si reducir tamaño de Hola de clúster de hello mediante la eliminación de las máquinas, las réplicas se empaquetarán íntegramente y tienen menos capacidad en general.

### <a name="how-much-data-can-i-store-in-an-actor"></a>¿Cuántos datos puedo almacenar en un actor?

Al igual que con los servicios de confianza, la cantidad de Hola de datos que se pueden almacenar en un servicio de actor está limitada solo por hello espacio total en disco y memoria disponible en todos los nodos de hello en el clúster. Sin embargo, actores individuales son más eficaces cuando se usa tooencapsulate una pequeña cantidad de lógica de negocios de estado y asociado. Como norma general, un actor individual debe tener un estado que se mida en kilobytes.

## <a name="other-questions"></a>Otras preguntas

### <a name="how-does-service-fabric-relate-toocontainers"></a>¿Cómo se relacionan Service Fabric a toocontainers?

Los contenedores ofrecen una manera simple toopackage los servicios y sus dependencias de forma que se ejecuten de forma coherente en todos los entornos y puede funcionar de forma aislada en una única máquina. Service Fabric ofrece una manera toodeploy y administrar servicios, incluidos los [servicios empaquetadas en un contenedor](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>¿Piensa tooopen origen Service Fabric?

Se piensa servicios confiables de tooopen origen hello y marcos de actores confiable en GitHub y aceptarán proyectos de toothose de las contribuciones de comunidad. Siga hello [blog de Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/) para obtener más detalles a medida que se anuncien.

Hola están actualmente no hay planes tooopen origen Hola Service Fabric en tiempo de ejecución.

## <a name="next-steps"></a>Pasos siguientes

- [Obtenga información sobre conceptos fundamentales de Service Fabric y procedimientos recomendados](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
