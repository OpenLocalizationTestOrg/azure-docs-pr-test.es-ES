---
title: "aaaFAQ para bases de datos de ClearDB MySql con el servicio de aplicación de Azure | Documentos de Microsoft"
description: "Respuestas toocommon preguntas frecuentes acerca del uso de bases de datos ClearDB MySQL con el servicio de aplicación de Azure."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>P+F sobre bases de datos MySql ClearDB con el Servicio de aplicaciones de Azure
Estas P+F responden a preguntas comunes sobre el uso y la adquisición de bases de datos MySQL ClearDB para aplicaciones web de Azure.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>¿Qué opciones tengo para MySQL en Azure?
Tiene varias opciones:

* [Base de datos MySQL ClearDB compartida](/marketplace/partners/cleardb/databases/)
* [Clústeres de MySQL ClearDB Premium](/marketplace/partners/cleardb-clusters/cluster/)
* [Clúster de MySQL en ejecución en una máquina virtual de Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Instancia única de MySQL en ejecución en una máquina virtual de Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB es un servicio de hospedaje de MySQL y administra la infraestructura de MySQL de hello en su nombre. Al ejecutar su propio clúster MySQL o una base de datos en una máquina Virtual de Azure, tiene tooset de servidor de MySQL de Hola y mantenerlo actualizado con las revisiones.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>¿Necesito una tarjeta de crédito para la aplicación Web de hello + plantilla de MySQL en Azure Marketplace Hola?
Esto depende de tipo hello de suscripción que estás usando. Estos son algunos tipos de suscripción de uso frecuente:

* [Pago por uso](/offers/ms-azr-0003p/): requiere una tarjeta de crédito. Al adquirir una base de datos MySQL de pago, se cargará el importe correspondiente en su tarjeta de crédito.
* [Prueba gratuita](https://azure.microsoft.com/pricing/free-trial/): incluye créditos para usarlos con los servicios de Microsoft Azure pero no permite la adquisición de recursos de terceros. suscripción habilitada para servicios de terceros toopurchase o una base de datos de MySQL pago necesita toouse una tarjeta de crédito. Para Web Apps, puede crear una base de datos MySQL ClearDB GRATUITA.
* [Suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) y **MSDN para desarrollo pruebas pago por uso**: Similar tooFree de prueba, una suscripción a MSDN requiere toohave un toopurchase de tarjeta de crédito una solución pagada de MySQL de ClearDB.
* [Contrato Enterprise (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/): los clientes de EA reciben su facturación de EA cada trimestre para todas sus compras en Azure Marketplace (terceros) mediante una factura independiente y consolidada. Se le facturará fuera Hola compromiso monetario para las compras de marketplace. Tenga en cuenta que, en este momento, el almacén de Azure no está disponible toocustomers inscritos en Azerbaiyán, Croacia, Noruega y Puerto Rico. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): Puede crear únicamente bases de datos ClearDB gratis para las aplicaciones web. No hay ningún límite en el número de Hola de bases de datos de ClearDB MySQL libre que puede crear. Observe que las bases de datos gratuitas no son toobe utilizado para las aplicaciones web de producción, como este servicio está destinado sólo para la versión de prueba.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>¿Por qué se me ha cobrado 3,50 USD para una aplicación Web + MySQL de hello Azure Marketplace?
opción de base de datos predeterminada de Hello es Titan, que es 3,50 USD. No va a mostrar el costo de Hola durante la creación de la base de datos y erróneamente podría comprar una base de datos que no quería. Intentamos toofind una experiencia de manera tooimprove Hola pero hasta ese momento, debe comprobar todas las los niveles de precios seleccionados para la aplicación web y la base de datos antes de hacer clic **crear** e iniciar la implementación de Hola de los recursos de Hola.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Estoy ejecutando MySQL en mi propia máquina virtual de Azure. ¿Puedo conectar mi base de datos de toomy de aplicación web de Azure?
Sí. Puede conectar la base de datos de tooyour de aplicación web mientras la VM de Azure le ha concedido acceso remoto tooyour web app. Para más información, consulte [Instalación de MySQL en una máquina virtual creada con el modelo de implementación clásico que disponga de Windows Server 2012 R2](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>¿En qué países se pueden usar los clústeres de MySQL Premium de ClearDB?
[Clústeres de MySQL de ClearDB Premium](/marketplace/partners/cleardb-clusters/cluster/) están disponibles en todas las regiones de Azure en todo el mundo, con excepción de Hola de India, Australia, sur de Brasil y China.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>¿Puedo crear una nueva toocreating anteriores de clúster una base de datos con la solución de clúster de ClearDB premium?
No, no se pueden crear clústeres de ClearDB vacíos. Hello Azure portal le permite toocreate bases de datos en un clúster, lo que puede crear un nuevo clúster en hello mismo tiempo.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>¿Se advertirá si intento toodelete una base de datos ClearDB MySQL que está en uso por una de mis aplicaciones?
No, Azure no avisa si se elimina una compra de Marketplace de la que dependa una aplicación.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>¿En qué regiones puedo crear bases de datos ClearDB?
Azure Marketplace no está disponible toocustomers inscritos de Azerbaiyán, Croacia, Noruega y Puerto Rico. ClearDB no está disponible en estas regiones.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>¿Qué plan de tarifa debo elegir para una base de datos y una aplicación web de producción?
Use el plan de tarifa Básico o uno de nivel superior para las aplicaciones web. Para ClearDB, se recomienda un plan Júpiter o Saturno. Revise las características de Hola y limitaciones de cada nivel de precios para ambos [aplicaciones Web](https://azure.microsoft.com/pricing/details/app-service/) y [bases de datos ClearDB MySQL](/marketplace/partners/cleardb/databases/) hello toochoose uno que se adapte a sus necesidades.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>¿Cómo puedo actualizar mi base de datos ClearDB de tooanother de un plan?
Hola [portal de Azure](https://portal.azure.com), se puede escalar una base de datos de hospedaje compartido de ClearDB. Lea esta [artículo](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn más. Actualmente no se admite la actualización para los clústeres de ClearDB Premium en hello portal de Azure.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>¿Por qué no veo la base de datos ClearDB en Azure Portal?
Si se crea con el Administrador de recursos de Azure de base de datos ClearDB o [nuevo Portal de Azure](https://portal.azure.com), no serán visible en hello [antiguo Portal de Azure](https://manage.windowsazure.com). toowork-resolver este problema es toolink la base de datos manualmente toohello web app. Del mismo modo si crear base de datos ClearDB en hello [antiguo portal](https://manage.windowsazure.com) que se van a no ser capaz de toosee la base de datos en hello [nuevo Portal de Azure](https://portal.azure.com). No hay ninguna solución alternativa para este último escenario de Hola.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>¿Con quién debo ponerme en contacto para obtener soporte técnico cuando tenga problemas con la base de datos?
Si tiene algún problema relacionado con la base de datos, póngase en contacto con el [soporte técnico de ClearDB](https://www.cleardb.com/developers/help/support) . Prepararán tooprovide con la información de suscripción de Azure.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>¿Puedo crear usuarios adicionales para la solución de clúster de base de datos MySQL ClearDB?
No. No se pueden crear usuarios adicionales, pero puede crear bases de datos adicionales en el clúster de base de datos de ClearDB.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>¿Pueden ser bases de datos de serie de Basic/Pro planes en lugar de tooPlanetary similares actualizado hoy en día en el portal de ClearDB?
Sí, las bases de datos de la serie Basic se pueden actualizar localmente (de Basic 60 a Basic 500). La serie Pro se puede actualizar localmente (de Pro 125 a Pro 1000) con la excepción de Pro 60. En estos momentos, no se admite la actualización de la base de datos Pro 60. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>¿Cuando migración los recursos de tooanother de una suscripción, mi base de datos de ClearDB MySQL se pueden migrar también?
Al realizar una migración de recursos entre suscripciones, se aplican algunas [limitaciones](app-service-web/app-service-move-resources.md) . Una base de datos MySQL ClearDB es un servicio de terceros, de ahí que no se migre durante la migración de la suscripción de Azure. Si no administra la migración de Hola de su MySQL la base de datos anterior toomigrating Azure recursos, su ClearDB MySQL se pueden deshabilitar las bases de datos. En primer lugar migre manualmente las bases de datos y luego realice la migración de la suscripción de Azure de la aplicación web. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>Alcanzó Hola límite de gasto en mi suscripción. Quitó el límite de Hola y el servicio de aplicación está en línea, sin embargo, la base de datos de hello no es accesible. ¿Cómo se habilita volver a base de datos de hello ClearDB?
Póngase en contacto con [ClearDB compatibilidad](https://www.cleardb.com/developers/help/support) base de datos de toore-enable Hola. Proporcióneles información de suscripción de Azure y el nombre de la base de datos.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>¿Se puede transferir una base de datos ClearDB de una suscripción de tarjeta de crédito suscripción tooan EA?
Bases de datos existentes de ClearDB usar Hola tarjeta de crédito asociada a las suscripciones existentes de Hola. toouse una suscripción de EA necesita toomigrate la base de datos nueva tooa de datos:

* Adquiera una nueva base de datos de ClearDB con su suscripción de EA.
* Migrar los datos tooyour nueva base de datos.
* Actualizar la aplicación toouse Hola nueva base de datos.
* Elimine la base de datos antigua de ClearDB.

Cuando se crea una nueva aplicación web con MySQL (ClearDB) o una base de datos de MySQL (ClearDB), Hola suscripción que elige determina cómo se paga por el servicio de Hola. Con una suscripción de EA, no se bloqueará adquisiciones de hello de servicios de terceros de hello como ClearDB Hola portal de Azure. Las suscripciones de EA se facturan fuera del compromiso monetario y se facturan de forma trimestral a pago vencido. cliente EA Hola tendría tooset de un método de pago como un toopay de tarjeta de crédito para los servicios de marketplace de terceros.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>¿Dónde puedo ver los cargos de Hola de ClearDB recursos en una suscripción de EA?
Para los clientes de EA directa, cargos de Marketplace de Azure están visibles en hello Enterprise Portal. Tenga en cuenta que todas las compras y los consumos de Marketplace se facturan fuera del compromiso monetario y se facturan trimestralmente a pago vencido. Los clientes EA tienen toopay directamente can y proveedores de servicios de terceros de toohello por lo que al habilitar un método de pago como una tarjeta de crédito con su EA cuenta.

Clientes indirectos de EA pueden buscar sus suscripciones de Azure Marketplace en hello **administrar suscripciones** página de hello Enterprise Portal, pero el precio está oculto. Los clientes deben ponerse en contacto con su LSP para obtener información sobre los gastos en Marketplace.

Acceso tooAzure Marketplace para los servicios de terceros puede administrarse por los administradores de inscripción de Azure EA. Se puede deshabilitar o volver a habilitar acceso too3rd entidad compras de hello almacén de administración de cuentas y suscripciones en la sección de cuentas de Hola Hola Enterprise Portal.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>¿Con quién puedo ponerme en contacto si tengo dudas sobre la factura de los servicios de ClearDB en mi suscripción EA?
Póngase en contacto con [de soporte al cliente Enterprise](http://aka.ms/AzureEntSupport) con lo que respecta toobilling bajo su inscripción EA. Hola, equipo de soporte técnico de EA Portal se responder su pregunta o ayudar a resolver el problema.

## <a name="more-information"></a>Más información
[P+F sobre Azure Marketplace](/marketplace/faq/)

