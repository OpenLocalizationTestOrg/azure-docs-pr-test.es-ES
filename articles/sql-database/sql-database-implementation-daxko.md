---
title: aaaAzure estudio de caso de Azure de base de datos de SQL - Daxko/CSI | Documentos de Microsoft
description: "Obtenga información acerca de cómo Daxko/CSI usa tooaccelerate de base de datos SQL de su ciclo de desarrollo y tooenhance su atención al cliente y el rendimiento"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI usa Azure tooaccelerate su ciclo de desarrollo y tooenhance su atención al cliente y el rendimiento
![Logotipo de Daxko/CSI](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Software de Daxko/CSI enfrentan un desafío: su base de clientes de centros de idoneidad y recreo aumenta rápidamente, gracias toohello correcto de su solución de software de empresa completa, pero mantenerse al día con la infraestructura de TI necesita para que crezca de Hola base de clientes estaba probando la compañía de hello personal de TI. empresa Hola cada vez más se restringido por una sobrecarga de operaciones creciente, especialmente para administrar sus bases de datos cada vez más. Lo que es peor, se Cortar esa sobrecarga de las operaciones en recursos de desarrollo para las nuevas iniciativas, como nuevas características de movilidad de software de la empresa de Hola.

Según tooDavid Molina, Director de desarrollo del producto en Daxko/CSI, Azure Software CSI proporcionado con el modelo de hello plataforma como servicio (PaaS) que sea necesario toosimplify administración de bases de datos, aumentar la escalabilidad y liberar recursos toofocus en software en lugar de operaciones. "Azure SQL Database resultó una excelente opción para nosotros. No tener tooworry acerca del mantenimiento de un servidor SQL Server, un clúster de conmutación por error, todos los hello y otras necesidades de la infraestructura era ideal para que podamos."

Puesto que migrar tooAzure, CSI Software necesita un personal de operaciones de solo dos toomanage entre 600 bases de datos de cliente. la compañía Hola utiliza grupos elásticos de base de datos de SQL Azure bases de datos de cliente de toomove basándose en tamaño y necesitan.

Continúa Molina, "nuestros clientes sentía Hola cambiar inmediatamente. Antes de implantar los grupos elásticos, solían encontrarse con tiempos de espera y otros problemas durante los periodos de ráfaga. Con Azure grupos elásticos, pueden irrumpir según sea necesario y usar software de hello sin problemas."

Además tooimproving rendimiento para los clientes, Azure grupos elásticos liberan los recursos de Software CSI toofocus sobre el desarrollo de nuevos servicios y características, en lugar de tratar directamente con las operaciones y administración. Los recursos de TI ayudó a Software CSI a mejorar su software de empresa de la oferta, SpectrumNG, toohelp captar miembros gimnasio, mejorar la eficacia de personal y proporcione personal y los miembros acceso móvil para tareas interactivas y notificaciones en tiempo real.

Azure también ha ayudado a Software CSI acelerar y mejorar Hola ciclo de desarrollo y control de calidad (QA) al habilitar las opciones de automatización. Con la implementación de Azure de la compañía de hello, los administradores de generación pueden empaquetar los componentes con hello clic de un botón. Como se describe en Molina, "como parte del ciclo de versiones de hello, preguntas y respuestas es ahora capaz de toodeploy tooa entorno de prueba en Azure, que imita mejor nuestra pila de producción. Podemos implementar compilaciones inmediatamente toovet de entorno de desarrollo tooour cambia. lo que supone una gran ventaja para nosotros, ya que, hasta ahora, no habíamos tenido paridad en las pruebas".

## <a name="offloading-toohello-cloud"></a>La descarga de toohello en la nube
Antes de mover en la nube toohello, Software de CSI tenía componen correctamente su propia infraestructura para varios inquilinos en un centro de datos local Houston. Empresa Hola expandidos, enfrentan crecientes quebraderos de compra, aprovisionamiento y mantener todo Hola hardware y software necesario toosupport sus clientes. Operaciones de toohandle personal de TI se convirtió en otro cuello de botella que ha provocado la ralentización de tooa de aprovisionamiento de nuevos recursos y efectuando nuevos toocustomers de servicios.

CSI Software analizó opciones de soluciones en la nube para eliminar esa sobrecarga y poder centrarse en el código en lugar de en las operaciones. empresa Hola detecta muchos de los proveedores de nube superior Hola solo ofrecen las soluciones de infraestructura como servicio (IaaS) que aún requieren una pila de IaaS de TI personal toomanage Hola grande. Final de hello, CSI Software determinó que soluciones de PaaS de Azure de Hola Hola mejor para sus necesidades. Molina lo explica así: "Azure obtiene software de hardware y del sistema de hello fuera del modo de hello, por lo que podemos centrar en nuestras ofertas de software, al tiempo que reduce la sobrecarga de TI".

## <a name="making-hello-transition-tooazure"></a>Realizar Hola transición tooAzure
Después de seleccionar Azure para su solución de PaaS, Software CSI comenzó a migrar su nube de toohello de infraestructura y las bases de datos de back-end. TooAzure anterior, los clientes de SpectrumNG necesitan tooinstall una aplicación cliente que comunica con un servicio de Windows Communication Foundation (WCF) en el back-end de Hola. Según tooMolina, "aunque algunos clientes hospedan todo el contenido de sus propios centros de datos, se crean para varios inquilinos de hello producto toobe. Se hospeda todo el contenido de un centro de datos Houston, con SQL Server como almacén de datos de Hola.

"La oferta de nuestros productos también incluye un portal de la web a nivel de miembro (escrito en ASP.net), que era la presencia en el web del cliente de toobe diseñada con etiqueta blanco toomatch hello y una API de SOAP toosupport hello en línea las páginas y una integración de aplicaciones de terceros."

en la nube Hola migración toohello no tuvo tiempo de arquitectura de Hola. Según tooMolina, "mayoría Hola de esfuerzo de hello aborda modificar modo de Hola que hemos leído la información de archivo de configuración, una modificación de la cadena de conexión centralizada y automatizar Hola empaquetado, la carga y la implementación de nuestros boletines."

Hola toodevelop crear una automatización, CSI informáticos que usan PowerShell de Azure y toocreate de las API de REST paquetes y cargarlos tooa el entorno de ensayo para versión todas las noches.
Hello general transición tooan implementación basada en la nube de Azure se incluyó rápidamente y sin problemas Hola CSI Software equipo de TI. Molina lo explica así: "en todos, ha surgido un entorno beta en nube de hello en tres semanas toofour de seguridad en el proyecto de Hola. lo que supuso una sorprendente ventaja para nosotros".

Después de configurar y probar hello entorno, CSI Software empezó a migrar los clientes. Para los clientes que ya está usando Software CSI de hospedaje, la transición de hello fue casi sin problemas. Migración de clientes de una implementación local, en la nube Hola migración toohello llevó algún tiempo adicional, pero estaba siendo principalmente sin complicaciones para los clientes y CSI Software.

Para los del nuevos clientes, Software CSI personal de TI utilizar Hola siguiente proceso tooon-panel ellos tooAzure:

1. Los scripts de PowerShell Azure son toospin usa la base de datos nueva para el cliente de hello; todos los clientes comienzan en un tooensure de nivel premium suficiente rendimiento inicial para la transición de Hola.
2. Cuando sea posible, Software de CSI utiliza Hola Asistente para migración de SQL Azure toomove datos tooan base de datos de SQL Azure instancia existente.
3. Por último, Microsoft SQL Server Integration Services (SSIS) son utilizado tooreconcile necesarios de las operaciones de limpieza de datos como de cualquier discrepancia en los datos de Hola o tooperform.

En la actualidad, el 99 % de los clientes de CSI Software están hospedados en cuatro centros de datos regionales de Azure (centro-norte, centro-sur, este y oeste de EE. UU.). Debido a los centros de datos en la región geográfica de cada cliente, la latencia se mantiene tooa mínimo.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Los grupos elásticos de Azure liberan recursos de TI
Varias características de Azure han ayudado a Software CSI Mayús se característica toobeing tiene el foco de infraestructura y operaciones y desarrollo centrado. Quizás ha sido mayor ventaja de Hola de grupos elásticos.

En estos momentos, CSI Software proporciona unas 550 bases de datos a los clientes. Antes de grupos elásticos, era difícil toomanage que muchas bases de datos dentro de una estructura de niveles. Administradores de OPS tenían tooassign niveles de rendimiento en función de necesidades de ráfaga de Hola de clientes, que requiere importantes recursos de TI sobrecarga. Gracias a los grupos elásticos, los administradores pueden asignar inquilinos a un grupo estándar o Premium, según corresponda y, después, transferir los clientes en función del tamaño y las necesidades. Los clientes pensaban efectos de Hola de grupos elásticos Hola casi inmediatamente; antes de grupos elásticos, los clientes tenían los tiempos de espera y otros problemas durante los períodos de uso de ráfaga, pero con grupos elásticos, los clientes pueden experimentar ráfagas de actividad según sea necesario y podrán seguir toouse SpectrumNG sin problemas.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>La replicación geográfica activa de Azure acelera la generación de informes
Varios clientes de CSI Software también están aprovechando las ventajas de la replicación geográfica activa de Azure. Con la replicación geográfica activa, la toofour bases de datos secundarias legibles pueden configurarse en hello regiones de centro de datos iguales o distintos. Software de CSI hace uso de replicación geográfica activa de dos maneras: en primer lugar, bases de datos secundarias de hello están disponibles en caso de hello de un centro de datos interrupción o hello incapacidad tooconnect toohello base de datos principal; y en segundo lugar, bases de datos secundarias de hello son legibles y pueden ser usado toooffload cargas de trabajo de solo lectura como trabajos de informes. Algunos clientes de Software de CSI utilizan este tooaccelerate beneficio reporting flujos de trabajo.

## <a name="csi-software-application-logic-and-architecture"></a>Arquitectura y lógica de aplicación de CSI Software
SpectrumNG utiliza roles web. Como aplicación hello es multiempresa, un servicio WCF es solicitud de conexión inicial de hello toohandle utilizado de los clientes. Como los Estados de Molina "solicitud Hola identifica cada cliente, lo que permite a continuación, nos compilar una cadena de conexión espera tootheir toodo de bases de datos y cualquier otra cosa necesite toodo."

Nivel de web Hola de su servicio, Software CSI aprovecha las ventajas de Azure el escalado automático, en función de día y hora. Recursos disponibles son tooaccommodate mayor automáticamente un mayor uso durante el horario comercial, según la zona horaria de toohello de cada centro de datos regional. Los recursos también se establecen tooscale hacia abajo los fines de semana, cuando son inferiores necesidades del cliente.

![Arquitectura de Daxko/CSI](./media/sql-database-implementation-daxko/figure1.png)

Figura 1. Un rol de trabajo de servicios en la nube extrae los datos estructurados de Azure SQL Database y los semiestructurados de Table Storage. Los usuarios de SpectrumNG interactúan con los datos a través de un rol web de servicios en la nube.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Uso de aplicaciones web y un nivel de plan web para las aplicaciones móviles
Usar base de datos de SQL de Azure liberan recursos para Software CSI tooenable nuevas iniciativas, incluida una completa plataforma móvil se basan en una API personalizada que se hospeda en aplicaciones web de Azure. plataforma de Hello permite a los miembros de gimnasio y programaciones de toocheck de personal toouse dispositivos móviles, las clases de libro y recibir mensajes.

plataforma Hello usa tootake un único componente de arquitectura orientada a servicios (SOA), al igual que un sistema de punto de venta (POS) o un sistema de ventas: mover en plan de hello tooanother Volar web y, a continuación, haga clic en un servicio toosupport ese componente, dejando todo lo demás en plan de web original Hola. Esta funcionalidad proporciona a CSI Software una flexibilidad extraordinaria y ayuda a reducir los costos.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure permite a los desarrolladores de CSI Software centrarse en las aplicaciones y los servicios
La base de datos de SQL Azure no es simplemente un boon tooSpectrumNG para aquellos clientes que disfrutan servicio rápida y confiable de hello, también es una ventaja más del Software de CSI importante del personal de TI y desarrolladores. Mediante la descarga de ops tooAzure en la nube de hello, CSI Software reduce la sobrecarga de recursos y la infraestructura, acelera en gran medida sus ciclos de desarrollo y ya no necesita rendimiento toooptimize de toomicromanage las bases de datos para sus inquilinos.

## <a name="more-information"></a>Más información
* toolearn más información acerca de los grupos elásticos Azure, consulte [grupos elásticos](sql-database-elastic-pool.md).
* toolearn más información sobre herramientas de la base de datos y el ajuste de escala elástica, consulte [escalado flexible y herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).
* vea toolearn más acerca de cómo migrar una base de datos de SQL Server, vea [migrar un tooAzure de base de datos de SQL Server](sql-database-cloud-migrate.md).
* toolearn más información acerca de la replicación geográfica activa, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md).
* toolearn más información acerca de los roles Web y roles de trabajo, consulte [roles de trabajo](../fundamentals-introduction-to-azure.md#compute).    
* toolearn más información acerca de Service Bus de Azure, consulte [Service Bus de Azure](https://azure.microsoft.com/services/service-bus/).
* toolearn más información acerca de la escala automática, consulte [ajuste de escala en los servicios de nube](../cloud-services/cloud-services-how-to-scale.md).

