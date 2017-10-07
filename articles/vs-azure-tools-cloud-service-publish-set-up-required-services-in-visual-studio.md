---
title: "aaaPrepare toopublish o implementar una aplicación de Azure desde Visual Studio | Documentos de Microsoft"
description: "Obtenga información acerca de hello procedimientos tooset los servicios de cuenta en la nube y el almacenamiento y configurar la aplicación de Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Preparar tooPublish o implementar una aplicación de Azure desde Visual Studio
## <a name="overview"></a>Información general
Para poder publicar un proyecto de servicio de nube, debe configurar Hola siguientes servicios:

* A **servicio en la nube** toorun sus roles en hello entorno de Azure
* A **cuenta de almacenamiento** que proporciona acceso a los servicios de Blob, cola y tabla de toohello.

Usar hello siguiendo los procedimientos tooset estos servicios y configurar la aplicación

## <a name="create-a-cloud-service"></a>un servicio en la nube
toopublish un tooAzure de servicio de nube, primero debe crear un servicio de nube que ejecute sus roles en hello entorno de Azure. Puede crear un servicio de nube en hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), tal y como se describe en la sección de hello **toocreate un servicio de nube mediante el uso de Hola portal de Azure clásico**, más adelante en este tema. También puede crear un servicio de nube en Visual Studio mediante Asistente para publicación de Hola.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate un servicio en la nube con Visual Studio
1. Abra el menú contextual Hola Hola proyecto de Azure y elija **publicar**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Si no ha iniciado sesión, inicie sesión con su nombre de usuario y contraseña para la cuenta de Microsoft de Hola o cuenta profesional asociada a su suscripción de Azure.
3. Elija hello **siguiente** botón tooadvance toohello **configuración** página.

    ![Configuración común del Asistente para la publicación](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. Hola **servicios en la nube** elija **crear nuevo**. Hola **crear servicios de Azure** aparece el cuadro de diálogo.
5. Escriba el nombre de hello del servicio en la nube. nombre de Hello forma parte de la dirección URL de hello para el servicio y, por tanto, debe ser único globalmente. nombre de Hello no distingue mayúsculas de minúsculas.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate un servicio de nube mediante el uso de hello portal de Azure clásico
1. Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkId=253103) Hola sitio Web de Microsoft.
2. toodisplay (opcional) una lista de servicios de nube que ya haya creado, elija el vínculo de servicios en la nube de Hola a la izquierda Hola de página Hola.
3. Elija hello  **+**  icono Hola inferior izquierda de las esquinas y, a continuación, elija **servicio de nube** en el menú de Hola que aparece. Aparecerá otra pantalla con dos opciones: **Creación rápida** y **Creación personalizada**. Si elige **creación rápida**, puede crear un servicio de nube simplemente especificando su dirección URL y Hola la región donde será hospedado físicamente. Si elige **Creación personalizada**, puede publicar inmediatamente un servicio en la nube especificando un paquete (archivo .cspkg), un archivo de configuración (.cscfg) y un certificado. Creación personalizada no es necesario si tiene previsto toopublish su servicio en la nube mediante el uso de hello **publicar** comando en un proyecto de Azure. Hola **publicar** comando está disponible en el menú contextual de Hola para un proyecto de Azure.
4. Elija **creación rápida** toolater publicar su servicio en la nube con Visual Studio.
5. Especifique un nombre para el servicio en la nube. dirección URL completa de Hello aparece el siguiente nombre de toohello.
6. En lista de hello, elija la región de Hola donde se encuentran la mayoría de los usuarios.
7. En parte inferior de Hola de ventana hello, elija hello **Create Cloud Service** vínculo.

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
Una cuenta de almacenamiento proporciona acceso a servicios de Blob, cola y tabla de toohello. Puede crear una cuenta de almacenamiento mediante Visual Studio o hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate una cuenta de almacenamiento mediante Visual Studio
1. En **el Explorador de soluciones**, abra menú contextual Hola Hola **almacenamiento** nodo y, a continuación, elija **crear cuenta de almacenamiento**.

    ![Crear una nueva cuenta de almacenamiento de Azure](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Seleccione o escriba Hola siguiente información para la nueva cuenta de almacenamiento Hola Hola **crear cuenta de almacenamiento** cuadro de diálogo.

   * Hola toowhich de suscripción de Azure que desee cuenta de almacenamiento de tooadd Hola.
   * nombre de Hola que desea toouse Hola nueva cuenta de almacenamiento.
   * región de Hola o grupo de afinidad (por ejemplo, oeste de Estados Unidos o Asia oriental).
   * Hola tipo de replicación que desea toouse Hola cuenta de almacenamiento, por ejemplo, con redundancia geográfica.
3. Cuando haya terminado, elija **crear**.hello nueva cuenta de almacenamiento aparece en hello **almacenamiento** lista **Explorador de servidores**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate una cuenta de almacenamiento mediante el uso de hello portal de Azure clásico
1. Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkId=253103) Hola sitio Web de Microsoft.
2. (Opcional) tooview sus cuentas de almacenamiento, elija hello **almacenamiento** vínculo en el panel Hola Hola parte izquierda de la página de Hola.
3. En la esquina inferior izquierda de Hola de página de hello, elija hello  **+**  icono.
4. En el menú de Hola que aparece, elija **almacenamiento**y, a continuación, elija **creación rápida**.
5. Asigne un nombre que dará como resultado una dirección url única a cuenta de almacenamiento de Hola.
6. Asigne un nombre al servicio en la nube. dirección URL completa de Hello aparece el siguiente nombre de toohello.
7. En la lista Hola de regiones, elija una región donde se encuentran la mayoría de los usuarios.
8. Especifique si desea que la replicación geográfica de tooenable. Si habilita la replicación geográfica, los datos se guardará en la posibilidad de Hola de tooreduce de varias ubicaciones físicas de pérdida. Esta característica hace que el almacenamiento sea más costoso, pero puede reducir el costo de hello habilitando la ubicación geográfica al crear la cuenta de almacenamiento de hello en lugar de agregar la característica de hello más tarde. Para obtener más información, consulte [Replicación geográfica](http://go.microsoft.com/fwlink/?LinkId=253108).
9. En parte inferior de Hola de ventana hello, elija hello **crear cuenta de almacenamiento** vínculo.

Después de crear la cuenta de almacenamiento, verá hello las direcciones URL que puede usar recursos de tooaccess en cada uno de los servicios de almacenamiento de Azure de Hola y Hola también las teclas de acceso principal y secundaria para la cuenta. Utilice estas claves de las solicitudes de tooauthenticate realizadas en los servicios de almacenamiento de Hola.

> [!NOTE]
> clave de acceso secundaria de Hello proporciona Hola igual a tooyour cuenta de almacenamiento como clave de acceso principal de Hola y se genera como una copia de seguridad debe en peligro su clave de acceso principal. Además, se recomienda volver a generar las claves de acceso de forma periódica. Puede modificar conexión cadena configuración toouse Hola clave secundaria mientras regenera la clave principal de hello, a continuación, puede modificarla clave principal de toouse Hola vuelve a generar mientras regenera la clave secundaria Hola.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Configurar los servicios de toouse aplicación proporcionados por cuenta de almacenamiento de Hola
Debe configurar cualquier rol que tiene acceso a almacenamiento toouse Hola almacenamiento de Azure de servicios que haya creado. toodo esto, puede utilizar varias configuraciones del servicio del proyecto de Azure. De forma predeterminada, se crean dos en su proyecto de Azure. Mediante el uso de varias configuraciones del servicio, puede usar Hola misma conexión de cadena en el código, pero tiene un valor diferente para una cadena de conexión en cada configuración del servicio. Por ejemplo, puede usar un toorun de configuración de servicio y depurar la aplicación localmente mediante el emulador de almacenamiento de Azure de Hola y un toopublish de configuración de servicio diferente tooAzure de su aplicación. Para obtener más información sobre configuraciones del servicio, consulte [Configuración de un proyecto de Azure mediante varias configuraciones del servicio](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>Proporciona los servicios de toouse aplicación Hola cuenta de almacenamiento de tooconfigure
1. Abra la solución de Azure en Visual Studio. En el Explorador de soluciones, abra el menú de acceso directo de Hola para cada rol en su proyecto de Azure que tiene acceso a los servicios de almacenamiento de Hola y elija **propiedades**. Se muestra una página con el nombre de Hola de rol de Hola Hola editor de Visual Studio. página de Hello muestra campos de Hola de hello **configuración** ficha.
2. En las páginas de propiedades de hello para el rol de hello, elija **configuración**.
3. Hola **configuración del servicio** elija nombre Hola de configuración del servicio de Hola que desea tooedit. Si desea toomake tooall de cambios de configuraciones de servicio de Hola para este rol, puede elegir **todas las configuraciones de**.  Para obtener más información acerca de cómo tooupdate service configuraciones, vea la sección de Hola **administrar cadenas de conexión para las cuentas de almacenamiento** en el tema de hello [configurar Roles de Hola para un servicio de nube de Azure con Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify cualquier configuración de la cadena de conexión, elija hello **...** botón siguiente opción de configuración toohello. Hola **crear cadenas de conexión de almacenamiento** aparece el cuadro de diálogo.
5. En **conectarse mediante**, elija hello **su suscripción** opción.
6. Hola **suscripción** elija su suscripción. Si lista Hola de suscripciones no incluye Hola uno que desee, elija hello **descargar configuración de publicación** vínculo.
7. Hola **nombre de la cuenta** lista, elija el nombre de cuenta de almacenamiento. Azure Tools obtiene automáticamente las credenciales de cuenta de almacenamiento mediante el uso de archivo .publishsettings de Hola. toospecify credenciales de la cuenta de almacenamiento manualmente, elija hello **credenciales escritas manualmente** opción y, a continuación, continúe con este procedimiento. Puede obtener el nombre de la cuenta de almacenamiento y la clave principal de hello [portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885). Si no desea que toospecify la configuración de su cuenta de almacenamiento manualmente, elija hello **Aceptar** cuadro de diálogo de botón tooclose Hola.
8. Elija hello **escriba la cuenta de almacenamiento** vínculo de credenciales.
9. Hola **nombre de la cuenta** cuadro, escriba el nombre de hello de la cuenta de almacenamiento.

   > [!NOTE]
   > Inicie sesión en hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885)y, a continuación, elija hello **almacenamiento** botón. portal de Hello muestra una lista de cuentas de almacenamiento. Si elige una cuenta, se abre una página para ella. Puede copiar Hola nombre de cuenta de almacenamiento de Hola desde esta página. Si está utilizando una versión anterior del portal clásico de hello, nombre de hello de la cuenta de almacenamiento aparece en hello **cuentas de almacenamiento** vista. toocopy este nombre, resáltelo en hello **propiedades** ventana de este ver y, a continuación, elija las claves de hello CTRL+c. nombre de hello toopaste en Visual Studio, elija hello **nombre de la cuenta** texto cuadro y, a continuación, elija teclas de CTRL+v Hola.
   >
   >
10. Hola **clave de cuenta** cuadro, escriba la clave principal, o copiar y pegar desde hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
     toocopy este clave:

    1. En parte inferior de Hola de página de hello para la cuenta de almacenamiento adecuada de hello, elija hello **administrar claves** botón.
    2. En hello **administrar claves de acceso** , seleccione el texto hello de clave de acceso principal de Hola y, a continuación, elija teclas CTRL+c de Hola.
    3. En Azure Tools, pegue la clave de Hola en hello **clave de cuenta** cuadro.
    4. Debe seleccionar una de hello después opciones toodetermine cómo servicio Hola accederán a la cuenta de almacenamiento de hello:

       * **Usar HTTP**. Se trata de una opción estándar de Hola. Por ejemplo: `http://<account name>.blob.core.windows.net`.
       * **Usar HTTPS** para una conexión segura. Por ejemplo: `https://<accountname>.blob.core.windows.net`.
       * **Especificar extremos personalizados** para cada uno de los servicios de hello tres. A continuación, puede escribir estos extremos en campo hello para el servicio específico de Hola.

         > [!NOTE]
         > Si crea extremos personalizados, puede crear una cadena de conexión más compleja. Cuando se utiliza este formato de cadena, puede especificar extremos de servicio de almacenamiento que incluyan un nombre de dominio personalizado que haya registrado para la cuenta de almacenamiento con hello servicio Blob. También puede conceder acceso solo tooblob recursos en un único contenedor a través de una firma de acceso compartido. Para obtener más información acerca de cómo toocreate extremos personalizados, consulte [configurar cadenas de conexión de almacenamiento de Azure](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave estos cambios de la cadena de conexión, elija hello **Aceptar** botón y, a continuación, elija hello **guardar** botón de barra de herramientas de Hola. Después de guardar estos cambios, puede obtener valor de Hola de esta cadena de conexión en el código mediante el uso de [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Al publicar su aplicación tooAzure, elija la configuración del servicio de Hola que contiene la cuenta de almacenamiento de Azure de hello para la cadena de conexión de Hola. Una vez publicada la aplicación, compruebe que la aplicación hello funciona según lo previsto con los servicios de almacenamiento de Azure Hola

## <a name="next-steps"></a>Pasos siguientes
toolearn más acerca de cómo publicar aplicaciones tooAzure desde Visual Studio, vea [publicar un servicio de nube mediante herramientas de Azure de hello](vs-azure-tools-publishing-a-cloud-service.md).
