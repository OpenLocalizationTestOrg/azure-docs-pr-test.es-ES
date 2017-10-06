---
title: 'Azure Cosmos DB: API de DocumentDB | Microsoft Docs'
description: "Obtenga información acerca de cómo puede usar base de datos de Azure Cosmos toostore y consultas grandes volúmenes de documentos JSON con una latencia baja mediante SQL y JavaScript."
keywords: base de datos json, base de datos de documentos
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Introducción tooAzure DB Cosmos: API de documentos

[Azure Cosmos DB](introduction.md) es un servicio de base de datos con varios modelos y distribución global de Microsoft para aplicaciones críticas. Proporciona la base de datos de Azure Cosmos [distribución global preparada](distribute-data-globally.md), [escalado flexible de rendimiento y almacenamiento](partition-data.md) latencias de milisegundo en todo el mundo, solo dígito se escriben en el percentil 99 de hello, [cinco niveles de coherencia bien definido](consistency-levels.md)y garantiza la alta disponibilidad, todo ello respaldado por [líderes en la industria SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de datos de Azure Cosmos [automáticamente los datos de índices](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sin necesidad de toodeal con administración de esquema y de índice. Sigue varios modelos y es compatible con los modelos de datos de documento, de clave-valor, de grafo y de columnas. 

![API de Azure DocumentDB](./media/documentdb-introduction/cosmosdb-documentdb.png) 

Con hello API de DocumentDB, base de datos de Azure Cosmos proporciona enriquecido y familiar [capacidades de consulta SQL](documentdb-sql-query.md) con latencias bajas coherente basados en datos JSON sin esquemas. En este artículo se proporciona una introducción hello Azure Cosmos DB API de documentos, y cómo puede usarlo toostore grandes volúmenes de datos JSON, consultarlos en orden de latencia de milisegundos y evolucionar con facilidad esquema Hola. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>¿Qué funcionalidades y características clave ofrece Azure Cosmos DB?
Azure DB Cosmos, a través de hello API de documentos, ofrece Hola siguientes ventajas y capacidades clave:

* **Rendimiento escalables de manera flexible y almacenamiento:** fácilmente aumentar o reducir su toomeet de base de datos JSON de la aplicación necesita. Los datos se almacenan en discos de estado sólido (SSD) para las bajas latencias predecibles. Base de datos de Azure Cosmos admite contenedores para almacenar datos JSON denominadas colecciones que se pueden escalar toovirtually tamaños de almacenamiento ilimitado y rendimiento aprovisionado. Según vaya creciendo su aplicación, puede escalar Azure Cosmos DB de manera flexible con un rendimiento predecible impecable. 


* **Replicación de varias regiones:** base de datos de Azure Cosmos replica de forma transparente las áreas de tooall de datos que se ha asociado con la cuenta de base de datos de Azure Cosmos, lo que las aplicaciones de toodevelop que requieren acceso global toodata al proporcionar equilibrio entre la coherencia, la disponibilidad y rendimiento, todos los datos con garantías correspondientes. Base de datos de Azure Cosmos proporciona transparente conmutación por error regional con las API de hospedaje múltiple y el rendimiento de escala de tooelastically de capacidad de Hola y el almacenamiento en todo el mundo de Hola. Más información en [Distribución de datos global con Azure Cosmos DB](distribute-data-globally.md).

* **Consultas ad hoc con sintaxis SQL conocida:** almacene los diferentes documentos JSON en y consúltelos con una sintaxis SQL conocida. Base de datos de Cosmos Azure emplea un grado elevado de simultaneidad, bloqueos, registro estructurado indización índice tooautomatically de tecnología de todo el contenido de documento. Esto permite enriquecidas consultas en tiempo real sin sugerencias de hello necesidad toospecify esquema, los índices secundarios o vistas. Más información en [Consultas en Azure Cosmos DB](documentdb-sql-query.md). 
* **Ejecución de JavaScript dentro de la base de datos de hello:** expresar la lógica de la aplicación como procedimientos almacenados, desencadenadores y funciones definidas por el usuario (UDF) mediante el estándar de JavaScript. Esto permite que su toooperate de lógica de aplicación en datos sin preocuparse de discrepancia de hello entre la aplicación hello y esquema de base de datos de Hola. Hola API de documentos ofrece una ejecución completa transaccional de lógica de la aplicación de JavaScript directamente dentro de motor de base de datos de Hola. fuerte integración de JavaScript de Hello habilita la ejecución de Hola de insertar, reemplazar, eliminar y las operaciones SELECT desde dentro de un programa de JavaScript como una transacción de aislamiento. Obtenga más información en [Programación de servidor DocumentDB](programming.md).

* **Niveles de coherencia ajustables:** Select en cinco bien definida coherencia niveles tooachieve un equilibrio óptimo entre coherencia y rendimiento. Para las consultas y las operaciones de lectura, Azure Cosmos DB ofrece cinco niveles de coherencia diferentes: segura, obsolescencia limitada, sesión, prefijo coherente y posible. Estos niveles de coherencia granular y bien definidos permiten toomake sonido ventajas y desventajas de coherencia, la disponibilidad y la latencia. Obtenga más información en [utilizando coherencia los niveles de rendimiento y la disponibilidad de toomaximize](consistency-levels.md).

* **Totalmente administrados:** eliminar hello toomanage base de datos y máquina recursos de necesidad. Como un servicio de Microsoft Azure completamente administrado, no no necesidad toomanage las máquinas virtuales, implementar y configurar el software, administrar el ajuste de escala o, ocuparse de las actualizaciones de la capa de datos complejos. Se realiza una copia de seguridad de cada base de datos además de protegerlas contra fallas regionales. Puede agregar una cuenta de base de datos de Azure Cosmos fácilmente y aprovisionar capacidad según sea necesario, lo que le toofocus en la aplicación en lugar de operar y administrar la base de datos. 

* **Diseño abierto** : comience rápidamente con las destrezas y herramientas existentes. Programar con hello API de documentos es sencilla, cercana y no requieren que tooadopt nuevas herramientas o cumplir toocustom extensiones tooJSON o JavaScript. Puede tener acceso a toda la funcionalidad de la base de datos de hello incluidos CRUD, consulta y procesar a través de una interfaz HTTP RESTful sencilla de JavaScript. Hola documentos API acoja estándares, idiomas y formatos existentes al tiempo que ofrece valor alto de capacidades de la base de datos encima de ellos.

* **La indexación automática:** de forma predeterminada, base de datos de Azure Cosmos automáticamente indiza todos los documentos de hello en la base de datos de hello y no esperan o requieren cualquier esquema o la creación de índices secundarios. ¿No desea tooindex todo? No se preocupe, también puede [renunciar a las rutas de acceso en los archivos JSON](indexing-policies.md) .

* **Cambiar fuente soporte técnico:** fuente de cambio proporciona una lista ordenada de documentos dentro de una colección de base de datos de Azure Cosmos en orden de hello en el que se han modificado. Esta fuente puede ser usado toolisten para toodata de modificaciones de datos del pedido tooreplicate, desencadenar llamadas a la API o realizar el procesamiento de la secuencia en las actualizaciones. Fuente de cambio está toouse habilita automáticamente y fácil: [aprender más acerca de cómo cambiar fuente](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>¿Cómo se administran los datos con hello API de documentos?
Hola API de documentos le ayuda a administrar datos JSON a través de recursos de base de datos bien definidos. Estos recursos se replican para ofrecer elevados niveles de disponibilidad y solo se pueden direccionar a través de su URI lógico. Hola API de documentos ofrece que una sencilla HTTP según RESTful modelo de programación para todos los recursos. 


cuenta de base de datos de base de datos de Azure Cosmos Hello es un espacio de nombres único que proporciona acceso a tooAzure Cosmos DB. Para poder crear una cuenta de base de datos, debe tener una suscripción de Azure, que proporciona acceso tooa diversos servicios de Azure. 

Todos los recursos de Azure Cosmos DB se modelan y almacenan como documentos JSON. Los recursos se administran como elementos, que son documentos JSON que contienen metadatos, y como fuentes que son recopilaciones de elementos. Las fuentes respectivas contienen los conjuntos de elementos.

imagen de Hello siguiente muestra las relaciones de hello entre los recursos de base de datos de Azure Cosmos hello:

![relación jerárquica de Hello entre recursos de base de datos de Azure Cosmos][1] 

Una cuenta de base de datos consta de un conjunto de bases de datos, cada una con varias recopilaciones. Cada recopilación puede contener, a su vez, procedimientos almacenados, desencadenadores, UDF, documentos y datos adjuntos relacionados. Una base de datos también tiene asociados los usuarios, cada uno con un conjunto de permisos tooaccess varias otras colecciones, procedimientos almacenados, desencadenadores, las UDF, documentos o datos adjuntos. Mientras que las bases de datos, los usuarios, permisos y las recopilaciones son recursos definidos por el sistema con esquemas conocidos, los documentos, procedimientos almacenados, desencadenadores, UDF y datos adjuntos contienen contenido JSON arbitrario y definido por el usuario.  

> [!NOTE]
> Puesto que Hola documentos API estaba disponible anteriormente como Hola servicio de Azure DocumentDB, puede continuar tooprovision, supervisar y administrar las cuentas creadas a través de la API de REST de administración de recursos de Azure de Hola o herramientas utilizando Hola documentos de Azure o base de datos de Azure Cosmos nombres de los recursos. Usamos los nombres Hola indistintamente cuando se hace referencia toohello Azure DocumentDB APIs. 

## <a name="develop"></a>¿Cómo se puede desarrollar aplicaciones con hello API de documentos?

Base de datos de Azure Cosmos expone los recursos a través de hello las API de REST que se pueda llamar desde cualquier lenguaje capaz de realizar solicitudes HTTP/HTTPS. Además, se ofrecen las bibliotecas de programación para varios idiomas populares para hello API de documentos. bibliotecas de cliente de Hello simplifican muchos aspectos sobre cómo trabajar con hello API controlando detalles como el almacenamiento en caché de dirección, administración de excepciones, reintentos automáticos y así sucesivamente. Las bibliotecas están disponibles actualmente para hello siguientes lenguajes y plataformas:  

| Descargar | Documentación |
| --- | --- |
| [.NET SDK](http://go.microsoft.com/fwlink/?LinkID=402989) |[Biblioteca de .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [SDK de Node.js](http://go.microsoft.com/fwlink/?LinkID=402990) |[Biblioteca de Node.js](http://azure.github.io/azure-documentdb-node/) |
| [SDK de Java](http://go.microsoft.com/fwlink/?LinkID=402380) |[Biblioteca de Java](/java/api/com.microsoft.azure.documentdb) |
| [SDK de JavaScript](http://go.microsoft.com/fwlink/?LinkID=402991) |[Biblioteca de JavaScript](http://azure.github.io/azure-documentdb-js/) |
| N/D |[SDK del servidor de JavaScript](http://azure.github.io/azure-documentdb-js-server/) |
| [SDK de Python](https://pypi.python.org/pypi/pydocumentdb) |[Biblioteca de Python](http://azure.github.io/azure-documentdb-python/) |
| N/D | [API para MongoDB](mongodb-introduction.md)


Con hello [emulador de base de datos de Azure Cosmos](local-emulator.md), puede desarrollar y probar la aplicación localmente con hello API de documentos, sin crear una suscripción de Azure o incurrir en los costos. Cuando esté satisfecho con cómo funciona la aplicación en el emulador de hello, puede cambiar una cuenta de base de datos de Azure Cosmos en nube de hello toousing.

Más allá de basic crear, leer, actualizar y eliminar operaciones, Hola API de documentos proporciona una interfaz enriquecida de consulta SQL para recuperar documentos JSON y la compatibilidad con el servidor para su ejecución transaccional de lógica de la aplicación de JavaScript. interfaces de ejecución de consultas y script de Hola están disponibles a través de todas las bibliotecas de plataforma, así como hello las API de REST. 

### <a name="sql-query"></a>Consulta SQL
admite la API de documentos Hola consultar documentos mediante un lenguaje SQL, que se basa en hello escriba JavaScript sistema y expresiones con compatibilidad con las consultas espaciales, relacional y jerárquicas. lenguaje de consulta de documentos de Hello es un documento JSON de tooquery de interfaz sencilla pero eficaz. lenguaje de Hello admite un subconjunto de la gramática de ANSI SQL y agrega integración profunda de objeto JavaScript, matrices, la construcción de objetos y la invocación de función. Hola API de documentos proporciona su modelo de consulta sin ningún esquema explícito o sugerencias de indización del programador de Hola.

Funciones definidas por el usuario (UDF) se pueden registrar con hello API de documentos y al que hace referencia como parte de una consulta SQL, ampliando así la lógica de la aplicación personalizada de hello gramática toosupport. Estos archivos UDF se escriben como programas de JavaScript y se ejecuta dentro de la base de datos de Hola. 

Para desarrolladores. NET, Hola documentos API [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) también ofrece un proveedor de consultas LINQ. 

### <a name="transactions-and-javascript-execution"></a>Transacciones y ejecución de JavaScript
Hola documentos API permite toowrite lógica de la aplicación como con nombre de los programas escritos completamente en JavaScript. Estos programas se registran para una colección y pueden emitir las operaciones de base de datos en documentos de hello dentro de una recopilación determinada. JavaScript se puede registrar para la ejecución como desencadenador, procedimiento almacenado o función definida por el usuario. Procedimientos almacenados y desencadenadores pueden crear, leer, actualizar y eliminar documentos, mientras que las funciones definidas por el usuario que se ejecuten como parte de la lógica de ejecución de consulta de hello sin acceso de escritura toohello recopilación.

Ejecución de JavaScript en hello Cosmos DB se basa en conceptos de hello compatibles con los sistemas de base de datos relacional, con el código de JavaScript como sustituto moderno de Transact-SQL. Toda la lógica de JavaScript se ejecuta en un entorno de transacciones ACID con aislamiento de la instantánea. Durante el transcurso de Hola de su ejecución, si Hola JavaScript produce una excepción, a continuación, Hola toda la transacción se anula.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>¿Hay cursos en línea de Azure Cosmos DB?

Sí, en la [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) hay un curso de Azure DocumentDB. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Pasos siguientes
¿Ya tiene una cuenta de Azure? Entonces puede empezar a trabajar con Azure Cosmos DB; deje que nuestras [guías de inicio rápido](../cosmos-db/create-documentdb-dotnet.md) le indiquen el proceso de creación de una cuenta e iniciación a Cosmos DB.

[1]: ./media/documentdb-introduction/json-database-resources1.png

