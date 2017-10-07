---
title: "una aplicación web de hello Azure Marketplace aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una nueva aplicación web de WordPress de hello Azure Marketplace usando Hola Portal de Azure."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Crear una aplicación web de hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Hello Azure Marketplace proporciona una amplia gama de aplicaciones web populares desarrollado por las Comunidades del software de código abierto, por ejemplo WordPress y Umbraco CMS. En este tutorial, aprenderá cómo toocreate WordPress aplicación de Azure marketplace.
con lo que se crean una aplicación web de Azure y una base de datos MySQL. 

![Panel de aplicación web de WordPress de ejemplo](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Antes de empezar 

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="deploy-from-azure-marketplace"></a>Implementación desde Azure Marketplace
Siga estos pasos hello toodeploy WordPress de Azure Marketplace.

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure
Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Plantilla de implementación de WordPress
Hello Azure Marketplace proporciona plantillas para la configuración de recursos, Hola el programa de instalación [WordPress](https://portal.azure.com/#create/WordPress.WordPress) tooget de plantilla que se inició.
   
Escriba Hola siguiente aplicación de WordPress de información toodeploy hello y sus recursos.

  ![Flujo de creación de WordPress](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Campo         | Valor sugerido           | Descripción  |
| ------------- |-------------------------|-------------|
| Nombre de la aplicación      | miAplicaciónDeWordPress          | Escriba **un nombre único para la aplicación web**. Este nombre se usa como parte del nombre DNS de hello predeterminado para la aplicación `<app_name>.azurewebsites.net`, por lo que necesita toobe único en todas las aplicaciones de Azure. Más adelante puede asignar una aplicación de tooyour de nombre de dominio personalizado antes de exponer a los usuarios de tooyour |
| La suscripción  | Pay-As-You-Go             | Seleccione una opción en **Suscripción**. Si tiene varias suscripciones, elija suscripción adecuado de Hola. |
| Grupo de recursos| miGrupoDeRecursosDeWordPress                 |    Escriba un **grupo de recursos**. Un grupo de recursos es un contenedor lógico en el que se implementan recursos de Azure y se administran, como aplicaciones web y bases de datos. Puede crear un grupo de recursos o usar uno existente. |
| Plan de servicio de aplicación | miPlanDeAplicaciones          | Planes de servicio de aplicaciones representan colección Hola de recursos físicos que usa toohost sus aplicaciones. Seleccione hello **ubicación** hello y **tarifa**. Para obtener más información sobre tarifas, consulte [Planes de tarifa de App Service](https://azure.microsoft.com/pricing/details/app-service/). |
| Base de datos      | miAplicaciónDeWordPress          | Seleccione proveedor de base de datos adecuada de Hola para MySQL. Web Apps admite **ClearDB**, **Azure Database for MySQL** y **MySQL en aplicación**. Para obtener más información, consulte la sección [Configuración de bases de datos](#database-config) más adelante. |
| Application Insights | ON (Activado) u OFF (Desactivado)          | Esto es opcional. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) proporciona servicios de supervisión para aplicaciones web al hacer clic en **ON** (Activado).|

<a name="database-config"></a>

### <a name="database-configuration"></a>Configuración de bases de datos
Siga los pasos de hello siguientes en función de su elección del proveedor de base de datos de MySQL.  Se recomienda esa base de datos de aplicación Web y MySQL en hello misma ubicación.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) es una solución desarrollada por terceros que proporciona un servicio de MySQL totalmente integrado en Azure. En bases de datos de orden toouse ClearDB, será necesario tooassociate una tarjeta de crédito tooyour [cuenta de Azure](http://account.windowsazure.com/subscriptions). Si ha seleccionado el proveedor de base de datos ClearDB, puede ver una lista de toochoose de las bases de datos existente de o haga clic en **crear nuevo** botón toocreate una base de datos.

![Crear base de datos ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Azure Database for MySQL (versión preliminar)
[Base de datos de Azure para MySQL](https://azure.microsoft.com/en-us/services/mysql) proporciona un servicio de base de datos administrados para el desarrollo de aplicaciones y una implementación que le permite toostand la base de datos MySQL en minutos y la escala en hello volar en la nube de hello confía más. Con los modelos de precios inclusivos, obtendrá todas las capacidades de Hola que desee como alta disponibilidad, seguridad y recuperación: incorporada, sin costo adicional. Haga clic en **tarifa** toochoose otra [tarifa](https://azure.microsoft.com/pricing/details/mysql). toouse existente de base de datos o existente de MySQL server, use un grupo de recursos existente en qué Hola reside el servidor. 

![Configurar opciones de base de datos de hello para la aplicación web de Hola](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure Database for MySQL (versión preliminar) y Web App on Linux de Azure (versión preliminar) no están disponibles en todas las regiones. más información acerca de toolearn [base de datos de Azure para MySQL (versión preliminar)](https://docs.microsoft.com/en-us/azure/mysql) y [Web App en Linux](./app-service-linux-intro.md) limitaciones. 

#### <a name="mysql-in-app"></a>MySQL en aplicación
[En la aplicación de MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) es una característica del servicio de aplicación que permite la ejecución MySql de forma nativa en la plataforma de Hola. funcionalidad básica de Hello compatible con la versión de Hola de característica de hello:

- Servidor de MySQL que se ejecuta en hello misma instancia junto con el servidor web que hospeda el sitio de Hola. De este modo, se incrementa el rendimiento de la aplicación.
- El almacenamiento se comparte entre los archivos de MySQL y los de la aplicación web. Tenga en cuenta que con los planes gratuito y compartido que puede alcanzar nuestros límites de cuota para utilizar Hola sitio basado en acciones de hello realizan. Consulte [las limitaciones de las cuotas](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) de los planes Gratis y Compartido.
- Puede activar el registro de consultas lentas y el registro general para MySQL. Tenga en cuenta que esto puede afectar al rendimiento del sitio de hello y no debe estar siempre activo. característica de registro de Hello le ayuda a investigar los problemas de la aplicación. 

Para obtener más información, consulte este [artículo](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ ).

![Administración de MySQL en aplicación](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Puede ver el progreso de hello haciendo clic en un icono de campana hello en parte superior de Hola de página del portal Hola mientras Hola se va a implementar la aplicación de WordPress.    
![Indicador de progreso](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Administración de la nueva aplicación web de Azure

Vaya toohello tootake portal Azure un vistazo a la aplicación web de hello que acaba de crear.

toodo esto, inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).

Hola menú izquierdo, haga clic en **servicios de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Ha llegado a la _hoja_ de su aplicación web (una página del portal que se abre horizontalmente).

De forma predeterminada, la hoja de la aplicación web muestra hello **Introducción** página. Esta página proporciona una visión del funcionamiento de la aplicación. En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. pestañas de Hola a la izquierda Hola de hoja de hello muestra páginas de configuración diferente de hello puede abrir.

![Hoja de App Service en Azure Portal](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Estas pestañas de hoja de hello mostrarán hello muchas características excepcionales, puede agregar la aplicación web de tooyour. Hola lista siguiente proporciona solo algunas de las posibilidades de hello:

* Asignación de un nombre DNS personalizado
* Enlace de un certificado SSL personalizado
* Configuración de la implementación continua
* Escalado vertical y horizontal
* Adición de la autenticación de usuarios

Completar 5 minutos WordPress instalación Asistente toohave WordPress aplicación hello activos y en funcionamiento. Extraer del repositorio [Wordpress documentación](https://codex.WordPress.org/) toodevelop su aplicación web.

![Asistente para instalación de WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Configuración de la aplicación 
Es necesario llevar a cabo varias tareas de administración en la aplicación de WordPress antes de poder usarla para producir. Siga estos pasos tooconfigure y administrar la aplicación WordPress:

| toodo esto... | Use esto... |
| --- | --- |
| **Cargar o almacenar archivos grandes** |[Complemento de WordPress para usar Blob Storage](https://wordpress.org/plugins/windows-azure-storage/)|
| **Enviar correo electrónico** |Compra [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) servicio de correo electrónico y usar hello [complemento WordPress para usar SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure,|
| **Nombres de dominio personalizados** |[Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Habilitación de HTTPS para una aplicación web en Azure App Service](app-service-web-tutorial-custom-ssl.md) |
| **Validación previa de la producción** |[Configuración de entornos de ensayo y desarrollo para aplicaciones web en Azure App Service](web-sites-staged-publishing.md)|
| **Supervisión y solución de problemas** |[Habilitación del registro de diagnóstico para aplicaciones web en Azure App Service](web-sites-enable-diagnostic-log.md) y [Supervisión de aplicaciones web en Azure App Service](app-service-web-tutorial-monitoring.md) |
| **Implementación de su sitio** |[Implementación de una aplicación web en Azure App Service](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Protección de la aplicación 
Es necesario llevar a cabo varias tareas de administración en la aplicación de WordPress antes de poder usarla para producir. Siga estos pasos tooconfigure y administrar la aplicación WordPress:

| toodo esto... | Use esto... |
| --- | --- |
| **Un nombre de usuario y una contraseña seguros**|  Cambie de contraseña con frecuencia. Evite usar nombres de usuario comunes, como *admin* o *wordpress*. Forzar que todos los nombres de usuario únicos de WordPress usuarios toouse y las contraseñas seguras. |
| **Manténgase al día** | Mantenga el núcleo de WordPress, temas, complementos de toodate. Usar hello más reciente PHP en tiempo de ejecución disponible en el servicio de aplicaciones de Azure |
| **Actualice las claves de seguridad de WordPress** | Actualización [clave de seguridad de WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) cifrado tooimprove almacenado en las cookies|

## <a name="improve-performance"></a>Mejora del rendimiento
Se consigue un rendimiento en la nube de hello principalmente a través de almacenamiento en caché y la escalabilidad horizontal. Sin embargo, deben considerarse Hola memoria, ancho de banda y otros atributos de hospedaje de aplicaciones Web.

| toodo esto... | Use esto... |
| --- | --- |
| **Conocer las capacidades de las instancias del Servicio de aplicaciones** |[Información sobre tarifas, incluidas las funcionalidades de los planes de App Service](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Almacenar recursos en caché** |Use [caché en Redis de Azure](https://azure.microsoft.com/en-us/services/cache/), o uno de Hola otras ofertas de almacenamiento en caché en hello [tienda de Azure](https://azuremarketplace.microsoft.com) |
| **Escalar su aplicación** |Necesita tooscale [aplicación web de hello en el servicio de aplicación de Azure](web-sites-scale.md) o base de datos de MySQL. MySQL en aplicación no admite el escalado horizontal, por lo que debe elegir ClearDB o Azure Database for MySQL (versión preliminar). [Escalar la base de datos de Azure para MySQL (versión preliminar)](https://azure.microsoft.com/en-us/pricing/details/mysql/) o si usa [ClearDB alta disponibilidad enrutamiento](http://w2.cleardb.net/faqs/) tooscale una base de datos |

## <a name="availability-and-disaster-recovery"></a>Disponibilidad y recuperación ante desastres
Alta disponibilidad incluye aspecto Hola de continuidad del negocio de toomaintain de recuperación de desastres. Planear para los errores y desastres en la nube de hello requiere errores de hello toorecognize rápidamente. Estas soluciones ayudan a implementar una estrategia de alta disponibilidad.

| toodo esto... | Use esto... |
| --- | --- |
| **Sitios de equilibrio de carga** o **sitios distribuidos geográficamente** |[Redirección del tráfico con Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Copia de seguridad y restauración** |[Copia de seguridad de una aplicación web en Azure App Service](web-sites-backup.md) y [Restauración de una aplicación web en Azure App Service](web-sites-restore.md) |

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de diversas características de [toodevelop de servicio de aplicaciones y la escala](/app-service-web/).
