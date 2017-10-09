---
title: aaaAzure estudio de caso de Azure de base de datos de SQL - Snelstart | Documentos de Microsoft
description: "Obtenga información acerca de cómo SnelStart utiliza base de datos SQL toorapidly expande sus servicios de negocios a una velocidad de 1.000 nuevas bases de datos de Azure al mes"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Con Azure, SnelStart ha expandido rápidamente sus servicios empresariales con una cifra de 1000 nuevas bases de datos SQL de Azure cada mes
![SnelStartLogo](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart hace popular financieros y business-software de administración para pequeñas y medianas empresas (PYME) en países bajos Hola. Un personal compuesto por 110 empleados —entre ellos, un equipo de TI de 35 miembros— atiende a 55 000 clientes. Moviendo de oferta de software como-servicio (SaaS) tooa de software de escritorio basada en Azure, SnelStart realizados Hola más de servicios integrados, automatizar la administración con entorno familiar de C# y optimizar el rendimiento y la escalabilidad ni over- o aprovisionamiento en las empresas que usan grupos elásticos. Uso de Azure proporciona fluidez de hello SnelStart de cambio de los clientes entre hello y local en la nube.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>¿Por qué SnelStart extendidos servicios de nube de escritorio toohello Hola
> "Trabajar con Azure significa que podemos entregar software más rápidamente, reaccionar frente a las peticiones de toocustomer rápidamente y escalar soluciones cuando aumenta la demanda".
> 
> Henry Been, arquitecto de software
> 
> 

SnelStart utilizó, durante años y con éxito, un modelo de desarrollo de software tradicional: codificación, empaquetado, envío y repetición. Con el tiempo, el Hola ritmo de cambio ha crecido más rápido y más rápido. Normativa cambia con frecuencia, y los clientes necesarios más fáciles registros financieros tooprocess de formas y colaboran con sus contables y gobierno tookeep seguridad con esos cambios.

"El software toocustomers de envío está costosos y limitación," según tooHenry sido, arquitecto de software. "Los gastos de producción, empaquetado y envío limitaban la frecuencia con la que podíamos publicar software. Tuvimos que toopackage actualizaciones para los envíos periódicos, pero que realizan toomeet disco duro cambio necesidades de nuestros clientes. No se podríamos nunca se asegura de que nuestros clientes actualizan toohello la versión más reciente del producto de Hola. Por lo tanto, ha surgido toosupport varias versiones, realizar Hola admiten también toodo muy difícil de trabajo."

Sido agrega, "Queríamos una manera tooprogram y la versión de las actualizaciones en un acelerado de la velocidad, por lo que podríamos innovar con mayor rapidez y crear nuevos servicios para nuestros clientes. También deseamos que un tooautomate de manera más procesa en orden toosimplify las necesidades de administración de negocios de nuestros clientes."

Para SnelStart, Hola solución fue tooextend sus servicios suscribiéndose a un proveedor de SaaS en la nube. plataforma de base de datos de SQL Azure Hola ayudó a SnelStart alcanzarlo sin incurrir en gastos TI principales hello, tendrías que hacer una solución de infraestructura como-servicio (IaaS).

modelo de nube de Hello también permite SnelStart toofix errores y proporciona características nuevas rápidamente, sin los clientes que necesitan toodownload y software para la actualización. TooBeen correspondiente, "servicios de nube de Azure mediante nos permite tooquickly act tras cambiantes requerimientos de terceros. En lugar de tener tooship un nuevo toothousands de versión de los clientes, podemos adaptar información enviada desde nuestros formatos de toonew de aplicación de escritorio requeridos por terceros."

## <a name="a-modern-company-with-traditional-roots"></a>Una empresa moderna con raíces tradicionales
SnelStart trata de una empresa moderna, ágil de vanguardia con raíces modesto desde too1964, cuando fundadores Hola inicia empresa Hola como un fabricante de piezas de instrumentos. corazón Hola de hello SnelStart negocio de software inició realmente late en hello década de 1980, durante la proliferación de Hola de hello PC. empresa Hola es necesario un mejor software de contabilidad de toohello alternativas disponible en el momento de hello, así que tardó es importante en sus propio manos. En 1982, empresa Hola crea foundation Hola de lo que finalmente se convertiría SnelStart un software de contabilidad. Desde el principio de hello, se ha terminado de software de Hola para su simplicidad y velocidad, tanto para que la empresa Hola finalmente cambia el foco y reinventado en una compañía de software.

En 1995, SnelStart publicó su primera aplicación de contabilidad para Windows. aplicación Hello, basado en las bases de datos de Microsoft Visual Basic 1.0 y Microsoft Access, ha ayudado a crecer Hola cliente base toomore de 5.000 usuarios.

En la actualidad, SnelStart es un importante proveedor de aplicaciones de línea de negocio (LOB) y administración empresarial destinadas a pymes neerlandesas y emprendedores autónomos. Como Carlo Kuip, arquitecto de TI, dice, "nuestro objetivo es tooprovide de automatización de 100 por ciento de los servicios de administración de negocios para nuestros clientes."

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Optimización del rendimiento y los costos con los grupos elásticos
SnelStart fue pionera a gran escala en utilizar los grupos elásticos. Grupos elásticos ayudar a los costos de límite de empresa de Hola y administración los requisitos de rendimiento de manera más eficaz. Según tooBeen, "mediante el uso de grupos elásticos, se pueda optimizar rendimiento según las necesidades de nuestros clientes, Hola sin el aprovisionamiento es excesivo. Si ha surgido tooprovision según la carga pico, sería muy costoso. En su lugar, Hola recursos de tooshare opción entre varias bases de datos de escaso uso nos permite toocreate una solución que funciona bien y es rentable. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Azure SQL Databases ayuda a agregar los datos en contenedores para disfrutar de aislamiento y seguridad
La base de datos de SQL Azure permite SnelStart tooeasily y mover de manera transparente tooAzure de datos de administración de negocios de los clientes locales. Hola base de datos de SQL Azure es un contenedor conveniente que proporciona aislamiento, un límite para la autenticación, autorización y fácil capacidades de copia de seguridad y restauración. Las bases de datos proporcionan un modelo conceptual adecuado para la administración empresarial. TooCarlo correspondiente Kuip, arquitecto de TI, "elementos dentro de este límite de contenedor contienen datos confidenciales que es fundamental tooa business y almacenar esos elementos en un mantiene aislada de la base de datos que ellos bien protegidos. Podemos administrar la autorización en el nivel de base de datos de Hola e incluso automatizar la administración de Hola y escalado horizontal de estas bases de datos sin necesidad de los administradores de base de datos (DBA) personal."

Almacenamiento de datos de SQL Azure también desempeña un papel en caso de seguridad y administración de SnelStart hello, ya que la empresa de hello recopilar datos de telemetría, como la detección de intrusiones, el registro de actividad de usuario y la conectividad.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure elimina la sobrecarga para que los desarrolladores pueden dedicar más tiempo a proporcionar valor
modelo de la plataforma Windows Azure de Hello quita la sobrecarga de infraestructura y había habilitado SnelStart tooautomate implementaciones mediante las bibliotecas de administración de C#. Como se indica Kuip, "hemos toogrow capaz de nuestras operaciones actuales con muy poco personal durante la recuperación ante desastres, la velocidad y la escalabilidad simultáneamente creciente opciones para nuestros clientes. desarrollo de Hello MAYÚS tooservices libera recursos toofocus en nuevos servicios y características, en lugar de simplemente actualizar tookeep de código existente de con nuevas normativas o impuestos códigos." Agrega, "Al automatizar la administración y usar la oferta de SaaS hello, estamos toodeliver capaz de más valor para nuestros clientes sin necesidad de toomake grandes inversiones en personal de operaciones." Por ejemplo, mediante el uso de grupos de Azure y flexibles, SnelStart era capaz de tooadd una variedad de características nuevas, incluida la integración de datos de clientes más sólida con los bancos, facturación nuevos servicios, comprobaciones de antecedentes de pequeñas empresas y servicios de correo electrónico.

> "Hola simplemente primeros meses de 2016, se expanden nuestras implementaciones de base de datos de SQL Azure desde unos 5.500 toomore de 12.000, y actualmente estamos agregando unos 1.000 bases de datos por mes".
> 
> Henry Been, arquitecto de software
> 
> 

Administración de base de datos se automatiza aún más mediante Hola trabajos elástico característica. Como se indica Kuip, "alta agradecemos la detección automática de Hola de bases de datos en una instancia de base de datos SQL [server]." Esto permite SnelStart tooexecute las operaciones de administración a través de su cliente dinámicamente creciente base sin una sobrecarga adicional.

La empresa también está desarrollando una API que actúa como agente entre los datos del cliente y las aplicaciones creadas por los asociados de software terceros. Como los Estados Kuip, "esta API permitirá otro software tooour proveedores tooadd funcionalidad, como la eliminación de la entrada de datos para las facturas y otros documentos." Los clientes ya no tendrán toomanually facturas de tipo en su software de administración de cuentas para pequeñas empresas; Hola SnelStart software intercambiarán la información necesaria de hello directamente. Esto permite a los clientes toojoin su negocios-administración tareas con el ecosistema de Hola de información que emergentes de transformación digital en el sector de Hola.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Cómo los servicios de Azure permiten que SnelStart use el modelo SaaS
Mediante el uso de Azure, SnelStart puede servir de sus clientes y sus contables más fácilmente en la nube de Hola. Por ejemplo, los clientes y contables pueden compartir información accediendo directamente a las API cliente de SnelStart, que está hospedada en Azure. Estados de Kuip "estos servicios reutilizables son aplicaciones web de tooour disponible orientado al cliente y proporcionan una infraestructura y las funciones comunes tooallow administración de toobusiness de acceso para los clientes y el software de terceros toothird utilizado por nuestros clientes. Por ejemplo, características de configuración del producto, administración de reglas de firewall y gestión de procesos de larga ejecución, como las copias de seguridad".

> Nuestro objetivo es tooprovide de automatización de 100 por ciento de los servicios de administración de negocios para nuestros clientes." 
> 
> Carlo Kuip, arquitecto de TI
> 
> 

Además, servicios web de SnelStart permitir que los clientes y contables tooeasily acceder a los datos en grupos elásticos de base de datos de SQL Azure. Este modelo de SaaS, junto con la elasticidad de las bases de datos y Azure Resource Manager, brinda a SnelStart las características de escalabilidad que complementan cada implementación de Azure. implementación de Hello es automatizar íntegramente mediante las bibliotecas de administración de C#.

![Arquitectura de SnelStart](./media/sql-database-implementation-snelstart/figure1.png)

Figura 1. Desde junio de 2016, SnelStart tiene más de 11 000 bases de datos y más de 50 grupos elásticos

## <a name="simplicity-from-hello-cloud"></a>Simplicidad de la nube de Hola
Desde que se movió tooan solución basada en la nube de Azure, SnelStart ha sido toosupport capaz de crecimiento de cliente rápida al tiempo que ofrece servicios y características innovadoras. Según tooBeen, "con Azure, podemos ofrecemos actualizaciones casi continua para nuestros clientes, sin expandir nuestro personal de operaciones. Y obtenemos Hola todas las otras características de Azure: escalabilidad y recuperación ante desastres, como: agrupados en. "

> "Cuando estábamos realmente sobre en Redmond... Recibió una llamada de un desarrollador en países bajos hello, llamar a mí sobre un problema concreto. Se estaban tooget capaz de Microsoft toodeliver un cambio en su entorno de producción dentro de 48 horas toosolve nuestro problema. "
> 
> Henry Been, arquitecto de software
> 
> 

SnelStart aprecia también ha desarrollado con el equipo de base de datos de SQL de Microsoft Azure Hola sólida de asociación de Hola. Como los Estados Kuip, "tenemos las discusiones sobre características y cómo la tecnología toouse, que es algo agradecería en ambos lados."
objetivo inmediato de Hola para SnelStart es tookeep aumentando a los clientes satisfechos de su base. Como ha indica, "Sin Hola técnica y limitaciones de los recursos que ha surgido como ISV, hay ninguna toohow límite ahora podemos ampliar".

## <a name="more-information"></a>Más información
* toolearn más información acerca de los grupos elásticos Azure, consulte [grupos elásticos](sql-database-elastic-pool.md).
* toolearn más información acerca de los roles Web y roles de trabajo, consulte [roles de trabajo](../fundamentals-introduction-to-azure.md#compute).    
* toolearn más información acerca del almacenamiento de datos de SQL Azure, consulte [almacenamiento de datos SQL](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn más información sobre SnelStart, consulte [SnelStart](http://www.snelstart.nl).

