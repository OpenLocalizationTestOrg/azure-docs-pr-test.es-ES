---
title: aaaAzure estudio de caso de Azure de base de datos de SQL - Umbraco | Documentos de Microsoft
description: "Obtenga información acerca de cómo Umbraco usa servicios de escala para miles de inquilinos y aprovisionamiento de tooquickly de base de datos de SQL en la nube de Hola"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco usa aprovisionar tooquickly de base de datos de SQL Azure y servicios de escala para miles de inquilinos en la nube de Hola
![Logotipo de Umbraco](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco es un sistema de administración de contenido de código abierto popular (CMS) que se puede ejecutar nada desde pequeños sitios campaña o un folleto toocomplex aplicaciones para las empresas de Fortune 500 y sitios Web de medios global. 

> "Tenemos bastante una gran comunidad de desarrolladores que usan el sistema de hello, con más de 100.000 a los desarrolladores en nuestros foros y más de 350.000 sitios que son dinámicos, ejecutando Umbraco."
> 
> Morten Christensen, director técnico de Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

las implementaciones de clientes de toosimplify Umbraco agregado Umbraco-as-a-Service (UaaS): una oferta de software como-servicio (SaaS) que elimina la necesidad de Hola para las implementaciones locales, proporciona escalado integrados y elimina la administración de sobrecarga habilitando los desarrolladores toofocus en administración de innovación, en lugar de solución de producto. Umbraco es capaz de tooprovide Hola a todos esos beneficios al depender de modelo flexible de (PaaS) de plataforma como servicio ofrecido por Microsoft Azure.

UaaS permite a los clientes de SaaS toouse Umbraco CMS funcionalidades que anteriormente se encontraban fuera de su alcance. Estos clientes se aprovisionan con un entorno CMS de trabajo que incluye una base de datos de producción. Los clientes pueden agregar seguridad tootwo bases de datos adicionales para el desarrollo y entornos, dependiendo de sus requisitos de almacenamiento provisional. Cuando se solicita un nuevo entorno, un proceso automatizado asigna automáticamente ese cliente a una base de datos. nueva base de datos de Hello está listo en segundos, porque la base de datos de hello ya se ha aprovisionado previamente por Umbraco desde un grupo elástico Azure de bases de datos disponibles (consulte la figura 1).

![Ciclo de vida de aprovisionamiento de Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Figura 1. Aprovisionamiento del ciclo de vida de Umbraco as a Service (UaaS)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>La automatización y los grupos elásticos de Azure simplifican las implementaciones
Con Azure SQL Database y otros servicios de Azure, los clientes de Umbraco pueden aprovisionar automáticamente sus entornos. Además, Umbraco puede supervisar y administrar con facilidad las bases de datos como parte de un flujo de trabajo intuitivo:

1. Aprovisionamiento
   
   Umbraco mantiene una capacidad de 200 bases de datos aprovisionadas previamente de grupos elásticos. Cuando un nuevo cliente se suscribe a UaaS, Umbraco proporciona a un nuevo entorno de CMS casi en tiempo real de cliente de Hola asignándoles una base de datos del grupo de disponibilidad de Hola.
   
   Cuando un grupo de disponibilidad alcanza el umbral, se crea un nuevo grupo elástico y nuevas bases de datos son toobe aprovisionado previamente asignado toocustomers según sea necesario.
   
   La implementación se automatiza por completo mediante el uso de bibliotecas de administración en C# y colas de Azure Service Bus.
2. Uso
   
   Los clientes usar una toothree entornos (para producción, almacenamiento provisional o desarrollo), cada con su propia base de datos. Las bases de datos de cliente están en grupos elásticos, que permite Umbraco tooprovide eficaz escalado sin tener tooover el aprovisionamiento.
   
   ![Información general del proyecto de Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Detalles del proyecto de Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Ilustración 2. Sitio web de cliente de Umbraco as a Service (UaaS), que muestra los detalles y un resumen del proyecto
   
   La base de datos de SQL Azure usa la energía relativa unidades de transacción de base de datos (Dtu) toorepresent Hola necesario para las transacciones de base de datos del mundo real. Para los clientes de UaaS, bases de datos suelen funcionan en unos 10 Dtu, pero cada uno tiene tooscale de elasticidad de Hola a petición. Es decir, UaaS puede garantizar que los clientes siempre tengan los recursos necesarios, incluso durante las horas pico. Por ejemplo, durante un evento de deportes los domingos recientes, un cliente UaaS experimentó picos de base de datos de Dtu de too100 durante Hola del juego de Hola. Azure grupos elásticos habían hecho que sea posible Umbraco toosupport que exigen gran sin una degradación del rendimiento.
3. Supervisión
   
   Monitores de Umbraco actividad dentro de hello portal de Azure, junto con las alertas de correo electrónico personalizadas en los paneles de la base de datos.
4. Recuperación ante desastres
   
   Azure ofrece dos opciones de recuperación ante desastres (DR): la replicación geográfica activa y la restauración geográfica. depende de la opción de recuperación ante desastres que debe seleccionar una compañía de Hello su [objetivos de continuidad del negocio](sql-database-business-continuity.md).
   
   replicación geográfica activa proporciona el nivel más rápida de Hola de respuesta en caso de hello de tiempo de inactividad. Con la replicación geográfica activa, puede crear hasta toofour secundarias legibles en servidores en regiones diferentes y, a continuación, puede iniciar tooany de conmutación por error de servidores secundarios de hello en caso de hello de un error.
   
   Umbraco no requiere la replicación geográfica, pero sacar provecho de la restauración geográfica Azure toohelp Asegúrese mínimo tiempo de inactividad en caso de hello de una interrupción. La restauración geográfica se basa en copias de seguridad de bases de datos en el almacenamiento de Azure con redundancia geográfica, Que permite a los usuarios toorestore desde una copia de seguridad cuando hay una interrupción en la región principal de Hola.
5. Desaprovisionamiento
   
   Cuando se elimina un entorno de proyecto, se quitan las bases de datos asociadas (desarrollo, ensayo o producción) durante la limpieza de colas de Azure Service Bus. Este proceso automatizado restauraciones Hola grupo de disponibilidad de base de datos elástica del tooUmbraco de bases de datos sin usar, ponerlas a disposición de aprovisionamiento futuras manteniendo la utilización máxima.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Grupos elásticos permiten UaaS tooscale con facilidad
Aprovechando las ventajas de Azure grupos elásticos, Umbraco puede optimizar el rendimiento de sus clientes sin necesidad de tooover o aprovisionar incompleta. Umbraco actualmente tiene casi 3.000 bases de datos a través de 19 grupos elásticos, con hello capacidad tooeasily escalar como sea necesario tooaccommodate cualquiera de sus 325.000 clientes existentes o nuevos clientes que están listo toodeploy un CMS en nube de Hola.

De hecho, según tooMorten Christensen, responsable técnico de Umbraco, "UaaS está ahora experimentando un crecimiento de aproximadamente 30 nuevos clientes al día. Nuestros clientes están encantados con comodidad Hola de ser capaz de tooprovision nuevos proyectos en segundos, publicar actualizaciones tootheir sitios activos de un entorno de desarrollo utilizando la 'implementación de un solo clic' al instante y realice cambios lo más rápidamente si encuentran errores . "

Si un cliente no vuelve a necesitar un segundo o tercero entorno, puede eliminarlos. Que libera los recursos que pueden usarse para otros clientes como parte del programa Hola a grupo de disponibilidad de base de datos elástica Umbraco.

![Arquitectura de implementación de Umbraco](./media/sql-database-implementation-umbraco/figure4.png)

Figura 3. Arquitectura de implementación de UaaS en Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>ruta de acceso de Hola desde toocloud del centro de datos
Cuando los desarrolladores de Umbraco Hola inicialmente realizan Hola decisión toomove tooa modelo SaaS, conoce que tienen un toobuild de manera rentable y escalable servicio Hola.

> "Los grupos elásticos son ideales para nuestra oferta de SaaS, ya que podemos ampliar y reducir la capacidad según sea necesario. El aprovisionamiento se realiza de forma sencilla, y con nuestra configuración, podemos mantener un nivel de uso máximo".
> 
> Morten Christensen, director técnico de Umbraco
> 
> 

"Deseamos toospend nuestro tiempo en la solución de problemas para nuestros clientes, no administrar la infraestructura. Deseamos toomake más sencilla para nuestro clientes tooget Hola mayor valor, "dice Niels Hartvig, fundador de Umbraco. "Se considera inicialmente servidores Hola desarrollamos de hospedaje, pero planeamiento de capacidad habría sido una pesadilla." Casualmente, Umbraco no emplea administradores de base de datos, lo que destaca una propuesta de valor importante para utilizar UaaS.

Un objetivo importante para los desarrolladores de Umbraco Hola era tooprovide una manera para que los entornos de tooprovision de los clientes de UaaS rápidamente y sin limitaciones de capacidad. Pero lo que proporciona que un servicio hospedado dedicado en centros de datos de Umbraco tendría requiere una gran cantidad de capacidad de sobra toohandle estalla de procesamiento. Es decir, tendrían que haber agregado una infraestructura de proceso considerable que se habría infrautilizado constantemente.

Además, el equipo de desarrollo de hello Umbraco deseaba una solución que les permitiera tooreuse como gran parte de su código existente como sea posible. Como desarrollador de Umbraco Estados Mikkel Madsen, "se estaban satisfechos con herramientas de desarrollo de Microsoft de Hola que ya hemos familiarizados con, como Microsoft SQL Server, base de datos SQL de Microsoft Azure, ASP.net y servicios de Internet Information Server (IIS). Antes de invertir en un IaaS o un PaaS en la nube solución, deseamos toomake seguro de que admitirían nuestras herramientas de Microsoft y plataformas, por lo que no tenemos toomake cambios masivos tooour la base de código. "

todos los toomeet de sus criterios, Umbraco buscará un socio en la nube con hello siguientes requisitos:

* Capacidad y confiabilidad suficientes
* Compatibilidad con herramientas de desarrollo de Microsoft, por lo que ese Umbraco ingenieros no sería forzada toocompletely inventar su entorno de desarrollo
* Presencia en todos los mercados geográficos hello en el que UaaS compite (empresas necesidad tooensure que puede tener acceso a sus datos rápidamente y que sus datos se almacenan en una ubicación que cumpla sus requisitos de regulación regionales)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Por qué Umbraco eligió Azure para UaaS
Según tooMorten Christensen "después de considerar todas las opciones de nuestro, hemos seleccionado Azure porque cumplieran todos nuestros criterios, de facilidad de uso y la escalabilidad toofamiliarity y la rentabilidad. Configurar entornos de hello en máquinas virtuales de Azure, y cada entorno tiene su propia instancia de la base de datos de SQL Azure, con todas las instancias de hello en grupos elásticos. Mediante la separación de bases de datos entre los entornos de desarrollo, ensayo y en vivo, podemos ofrecer a nuestros clientes sólido rendimiento tooscale coincide con el aislamiento, una gran victoria. "

Continúa Morten, "antes, tuvimos tooprovision servidores de bases de datos web manualmente. Ahora, no tenemos toothink sobre él. Todo es automático, desde el aprovisionamiento toocleanup. "

Morten también está satisfecho con hello escalar las capacidades proporcionadas por Azure. "Los grupos elásticos son ideales para nuestra oferta de SaaS, ya que podemos ampliar y reducir la capacidad según sea necesario. El aprovisionamiento se realiza de forma sencilla, y con nuestra configuración, podemos mantener un nivel de uso máximo". Estados de Morten, "sencillez de Hola de grupos elásticos, junto con la garantía de Hola de Dtu basado en el nivel de servicios, nos da Hola power tooprovision nuevos grupos de recursos a petición. Recientemente, uno de nuestros clientes mayor descendió too100 Dtu en su entorno activo. Con Azure, nuestro grupos elásticos proporcionan las bases de datos del cliente de hello con recursos de Hola que tenían en tiempo real sin necesidad de requisitos de DTU de toopredict. En pocas palabras, nuestros clientes obtienen Hola tiempo que esperan y podemos satisfacer nuestros acuerdos de nivel de servicio de rendimiento".

Mikkel Madsen la suma los: "nos hemos que adoptan algoritmo Azure eficaz Hola que se conecta a un patrón habitual de SaaS escenario (incorporación nuevos clientes en tiempo real a escala) tooour aplicación (aprovisionar bases de datos, ambos desarrollo y en directo) en la parte superior Hola tecnología subyacente (uso de colas de Service Bus de Azure junto con la base de datos de SQL Azure)."

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Con Azure, UaaS supera las expectativas de los clientes
Desde elegir Azure como su asociado de la nube, Umbraco ha sido capaz de tooprovide UaaS clientes con rendimiento optimizado de administración de contenido, sin necesidad de inversión de hello recursos de TI requerido a partir de una solución hospedada por sí mismo. Como Morten dice, "nos encanta comodidad de desarrollador de Hola y escalabilidad que nos da Azure y nuestros clientes están encantados con características de Hola y confiabilidad. En líneas generales, nos ha aportado un sinfín de ventajas".

## <a name="more-information"></a>Más información
* toolearn más información acerca de los grupos elásticos Azure, consulte [grupos elásticos](sql-database-elastic-pool.md).
* toolearn más información acerca de Service Bus de Azure, consulte [Service Bus de Azure](https://azure.microsoft.com/services/service-bus/).
* toolearn más información acerca de los roles Web y roles de trabajo, consulte [roles de trabajo](../fundamentals-introduction-to-azure.md#compute).    
* toolearn más información acerca de una red virtual, vea [redes virtuales](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn más información acerca de copia de seguridad y recuperación, consulte [continuidad del negocio](sql-database-business-continuity.md).    
* vea toolearn más información acerca de la supervisión de ppols, [supervisión grupos](sql-database-elastic-pool-manage-portal.md).    
* toolearn más información acerca de Umbraco como un servicio, consulte [Umbraco](https://umbraco.com/cloud).

