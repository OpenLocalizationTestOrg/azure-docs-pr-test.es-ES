---
title: "aaaGet a trabajar con el Explorador de almacenamiento (versión preliminar) | Documentos de Microsoft"
description: "Administración de recursos de almacenamiento de Azure con el Explorador de almacenamiento (versión preliminar)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Introducción al Explorador de Storage (versión preliminar)
## <a name="overview"></a>Información general
Explorador de almacenamiento de Azure (vista previa) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux. En este artículo, aprenderá Hola diversas formas de conectarse tooand administrar sus cuentas de almacenamiento de Azure.

![Explorador de almacenamiento de Microsoft Azure (versión preliminar)][15]

## <a name="prerequisites"></a>Requisitos previos
* [Descargue e instale el Explorador de Storage (versión preliminar)](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Conecte tooa cuenta de almacenamiento o servicio
Explorador de almacenamiento (versión preliminar) proporciona varias maneras de tooconnect toostorage cuentas. Por ejemplo, puede:
* Conectar las cuentas de toostorage asociadas a las suscripciones de Azure.
* Conectar toostorage cuentas y los servicios que se comparten desde otras suscripciones de Azure.
* Conectar tooand administrar el almacenamiento local mediante el uso de hello emulador de almacenamiento de Azure. 

Además, puede trabajar con cuentas de almacenamiento en nubes de Azure globales y nacionales:

* [Conectar tooan suscripción de Azure](#connect-to-an-azure-subscription): administrar recursos de almacenamiento que pertenecen tooyour suscripción de Azure.
* [Trabajar con almacenamiento de desarrollo local](#work-with-local-development-storage): administrar el almacenamiento local mediante el uso de hello emulador de almacenamiento de Azure.
* [Conectar almacenamiento tooexternal](#attach-or-detach-an-external-storage-account): administrar recursos de almacenamiento que pertenecen tooanother suscripción de Azure o que están bajo nubes Azure nacionales mediante nombre de la cuenta de almacenamiento de hello, claves y los puntos de conexión.
* [Asociar una cuenta de almacenamiento mediante una SAS](#attach-storage-account-using-sas): administrar recursos de almacenamiento que pertenecen tooanother suscripción de Azure utilizando una firma de acceso compartido (SAS).
* [Asociar un servicio mediante una SAS](#attach-service-using-sas): administrar un servicio de almacenamiento específica (contenedor de blob, cola o tabla) que pertenece tooanother suscripción de Azure mediante el uso de una SAS.

## <a name="connect-tooan-azure-subscription"></a>Conectar tooan suscripción de Azure
> [!NOTE]
> Si aún no tiene ninguna cuenta de Azure, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. En el Explorador de almacenamiento (versión preliminar), seleccione **Configuración de la cuenta de Azure**.

    ![Configuración de la cuenta de Azure][0]

2. panel izquierdo de Hello muestra todas las cuentas de Microsoft de Hola que ha iniciado la sesión. cuenta de tooconnect tooanother, seleccione **agregar una cuenta**y, a continuación, siga Hola instrucciones toosign con una cuenta de Microsoft que está asociada con al menos una suscripción activa de Azure.

    >[!NOTE]
    >Conexión toonational Azure (por ejemplo, Azure en Alemania, administración pública de Azure y Azure China a través de inicio de sesión) actualmente no se admite. Vea Hola "adjuntar o separar una cuenta de almacenamiento externo" sección para saber cómo las cuentas de almacenamiento de Azure de toonational tooconnect.

3. Después de iniciar sesión correctamente con una cuenta de Microsoft, Hola izquierda panel se llena con hello Azure suscripciones asociadas a esa cuenta. Seleccione Hola suscripciones de Azure que desee toowork con y, a continuación, seleccione **aplicar**. (Seleccione **todas las suscripciones** alterna seleccionando todas o ninguna de hello muestran las suscripciones de Azure.)

    ![Selección de suscripciones de Azure][3]  
    panel izquierdo de Hello muestra las cuentas de almacenamiento de hello asociadas con suscripciones de Azure Hola seleccionado.

    ![Suscripciones de Azure seleccionadas][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Conectar suscripción de Azure pila tooan

Para obtener información acerca de la suscripción de Azure pila tooan conexión, consulte [conectar Explorador de almacenamiento tooan suscripción de Azure pila](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Trabajo con el almacenamiento de desarrollo local
Con el Explorador de almacenamiento (vista previa), puede trabajar en el almacenamiento local mediante el uso de hello emulador de almacenamiento de Azure. Este enfoque le permite escribir código frente a y el almacenamiento de prueba sin necesidad de tener una cuenta de almacenamiento implementada en Azure, porque la cuenta de almacenamiento de hello está siendo emulado por hello emulador de almacenamiento de Azure.

> [!NOTE]
> Hola emulador de almacenamiento de Azure actualmente solo se admite para Windows.
>
>

1. En el panel izquierdo de hello del explorador de almacenamiento (versión preliminar), expanda hello **(locales y adjuntas)** > **cuentas de almacenamiento** > **(desarrollo)** nodo.

    ![Nodo de desarrollo local][21]

2. Si aún no ha instalado Hola emulador de almacenamiento de Azure, son toodo solicitada por lo que a través de una barra de información. Si se muestra la barra de información de hello, seleccione **descargue la versión más reciente de hello**y, a continuación, instalar el emulador de Hola.

    ![Mensaje para descargar el emulador de Almacenamiento de Azure][22]

3. Después de instala el emulador de hello, puede crear y trabajar con tablas, colas y blobs locales. toolearn cómo escribe toowork con cada cuenta de almacenamiento, consulte uno de los siguientes hello:

    * [Administración de recursos de Azure Blob Storage](vs-azure-tools-storage-explorer-blobs.md)
    * Administración de recursos de almacenamiento de recurso compartido de archivos de Azure; *próximamente*
    * Administración de recursos de Azure Queue Storage; *próximamente*
    * Administración de recursos de Azure Table Storage; *próximamente*

## <a name="attach-or-detach-an-external-storage-account"></a>Conexión a almacenamiento externo
Con el Explorador de almacenamiento (vista previa), puede asociar las cuentas de almacenamiento de tooexternal para que pueden compartirse fácilmente las cuentas de almacenamiento. Esta sección se explica cómo tooattach too(and detach from) cuentas de almacenamiento externo.

### <a name="get-hello-storage-account-credentials"></a>Obtener las credenciales de cuenta de almacenamiento de Hola
tooshare una cuenta de almacenamiento externo, el propietario de Hola de esa cuenta debe primero obtener credenciales de hello (nombre de cuenta y clave) para la cuenta de hello y, a continuación, compartir esa información con hello quien desea tooattach toothat (externo) cuenta. Puede obtener credenciales de cuenta de almacenamiento de Hola a través del portal de Azure Hola haciendo Hola siguiente:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. Seleccione **Examinar**.

3. Seleccione **Cuentas de almacenamiento**.

4. En hello **cuentas de almacenamiento** hoja, seleccione Hola deseado cuenta de almacenamiento.

5. En hello **configuración** hoja para hello seleccionado cuenta de almacenamiento, seleccione **las claves de acceso**.

    ![Opción de teclas de acceso][5]

6. En hello **las claves de acceso** hoja, Hola copia **nombre de la cuenta de almacenamiento** y **key1** valores para su uso al asociar la cuenta de almacenamiento de toohello.

    ![Claves de acceso][6]

### <a name="attach-tooan-external-storage-account"></a>Asociar la cuenta de almacenamiento externa tooan
cuenta de almacenamiento externo de tooattach tooan, necesita la cuenta de hello nombre y clave. Hola "Obtener credenciales de cuenta de hello almacenamiento" sección explica cómo tooobtain estos valores de hello portal de Azure. Sin embargo, en el portal de hello, clave de cuenta de hello se denomina **key1**. Por tanto, cuando el Explorador de almacenamiento (versión preliminar) solicita una clave de cuenta, escriba Hola **key1** valor.

1. En el Explorador de almacenamiento (versión preliminar), seleccione **conectar almacenamiento tooAzure**.

    ![Opción de almacenamiento de tooAzure de conexión][23]

2. Hola **conectar tooAzure almacenamiento** diálogo cuadro, especifique la clave de la cuenta de hello (hello **key1** valor de hello portal de Azure) y, a continuación, seleccione **siguiente**.

    > [!NOTE]
    > Puede escribir la cadena de conexión de almacenamiento de Hola desde una cuenta de almacenamiento en Azure nacional. Por ejemplo, cuentas de almacenamiento de tooconnect tooAzure Alemania, escriba similar toohello siguiente de cadenas de conexión: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >Puede obtener la cadena de conexión de Hola de hello Azure portal Hola igual manera que se describe en Hola sección "Obtener credenciales de cuenta de almacenamiento de Hola".

    ![Cuadro de diálogo de almacenamiento de tooAzure conectar][24]

3. Hola **adjuntar almacenamiento externo** cuadro de diálogo hello **nombre-cuenta** cuadro, escriba el nombre de cuenta de almacenamiento de hello, especifique cualquier otro valor deseado y, a continuación, seleccione **siguiente**.

    ![Cuadro de diálogo Attach External Storage (Asociar almacenamiento externo)][8]

4. Hola **conexión resumen** diálogo cuadro, compruebe la información de Hola. Seleccione si desea toochange nada, **volver** y vuelva a escribir la configuración de hello deseado. 

5. Seleccione **Conectar**.

6. Cuando está conectado correctamente, se muestra la cuenta de almacenamiento externo de hello con **(externo)** anexa toohello nombre de la cuenta de almacenamiento.

    ![Resultado de conexión de cuenta de almacenamiento externo tooan][9]

### <a name="detach-from-an-external-storage-account"></a>Desasociación de una cuenta de almacenamiento externo
1. Haga clic en la cuenta de almacenamiento externo de Hola que desee toodetach y, a continuación, seleccione **separar**.

    ![Opción para desasociar del almacenamiento][10]

2. En el mensaje de confirmación de hello, seleccione **Sí** desasociación de hello tooconfirm de cuenta de almacenamiento externo de Hola.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Asociación de una cuenta de almacenamiento mediante una SAS
Un [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) permite Hola, Administrador de una suscripción de Azure conceder acceso temporal de cuenta de almacenamiento de tooa sin necesidad de credenciales de suscripción de Azure tooprovide.

tooillustrate este escenario, vamos a decir que ese UserA es un administrador de una suscripción de Azure y UserA desea tooallow UserB tooaccess cuenta de almacenamiento durante un tiempo limitado con permisos específicos:

1. UserA genera una SAS (que consta de cadena de conexión de Hola Hola cuenta de almacenamiento) de una hora específica período y con permisos de hello deseado.

2. Recursos compartidos de UserA Hola SAS con persona hello (UserB, en nuestro ejemplo) que desea la cuenta de almacenamiento de toohello de acceso.  

3. UserB registrará el Explorador de almacenamiento (versión preliminar) tooattach toohello pertenece tooUserA mediante el uso de hello proporcionado SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Obtener una SAS para la cuenta de hello que desea tooshare
1. En el Explorador de almacenamiento (vista previa), haga clic en la cuenta de almacenamiento de Hola que desee compartir y, a continuación, seleccione **obtener firma de acceso compartido**.

    ![Opción de menú contextual para obtener la SAS][13]

2. Hola **firma de acceso compartido** diálogo cuadro, especifique el período de tiempo de Hola y los permisos que desee para la cuenta de hello y, a continuación, seleccione **crear**.

    ![Cuadro de diálogo Get SAS (Obtener SAS)][14]  
    Hola **firma de acceso compartido** cuadro de diálogo se abre y muestra hello SAS.

3. Siguiente toohello **cadena de conexión**, seleccione **copia** toocopy se toohello Portapapeles y, a continuación, seleccione **cerrar**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Asociar cuenta toohello compartido mediante Hola SAS
1. En el Explorador de almacenamiento (versión preliminar), seleccione **conectar almacenamiento tooAzure**.

    ![Opción de almacenamiento de tooAzure de conexión][23]

2. Hola **conectar tooAzure almacenamiento** cuadro de diálogo, especifique la cadena de conexión de hello y, a continuación, seleccione **siguiente**.

    ![Cuadro de diálogo de almacenamiento de tooAzure conectar][24]

3. Hola **conexión resumen** diálogo cuadro, compruebe la información de Hola. cambios de toomake, seleccione **volver**y, a continuación, escriba la configuración de Hola que desee. 

4. Seleccione **Conectar**.

5. Después de que está conectado, se muestra la cuenta de almacenamiento de hello con **(SAS)** anexa el nombre de la cuenta de toohello que ha proporcionado.

    ![Resultado de la cuenta de tooan conectados mediante el uso de SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a>Asociación de un servicio mediante una SAS
sección de "Adjuntar una cuenta de almacenamiento mediante una SAS" Hello explica cómo un administrador de suscripción de Azure puede conceder cuenta de almacenamiento de acceso temporal tooa generar y compartir una SAS Hola cuenta de almacenamiento. De igual forma, se puede generar una SAS para un servicio específico (contenedor de blobs, cola o tabla) dentro de una cuenta de almacenamiento.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Generar una SAS para el servicio de Hola que desea tooshare
En este contexto, un servicio puede ser un contenedor de blobs, una cola o una tabla. Hola toogenerate SAS para un servicio de la lista, vea:

* [Obtener Hola SAS para un contenedor de blobs](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Obtener Hola SAS para un recurso compartido de archivos: *próximamente*
* Obtener Hola SAS para una cola: *próximamente*
* Obtener Hola SAS para una tabla: *próximamente*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Asociar cuenta toohello compartido Hola de servicio mediante el uso de SAS
1. En el Explorador de almacenamiento (versión preliminar), seleccione **conectar almacenamiento tooAzure**.

    ![Opción de almacenamiento de tooAzure de conexión][23]

2. Hola **conectar tooAzure almacenamiento** cuadro de diálogo, especifique el URI de SAS de hello y, a continuación, seleccione **siguiente**.

    ![Cuadro de diálogo de almacenamiento de tooAzure conectar][24]

3. Hola **conexión resumen** diálogo cuadro, compruebe la información de Hola. cambios de toomake, seleccione **volver**y, a continuación, escriba la configuración de Hola que desee. 

4. Seleccione **Conectar**.

5. Una vez que se conecta, hello servicio recién conectado se muestra en hello **(servicio SAS)** nodo.

    ![Resultado de adjuntar servicio tooa compartido mediante una SAS][20]

## <a name="search-for-storage-accounts"></a>Búsqueda de cuentas de almacenamiento
Si tiene una larga lista de cuentas de almacenamiento, un toolocate de forma rápida una cuenta de almacenamiento concreta es toouse Hola búsqueda cuadro Hola parte superior del panel izquierdo de Hola.

Cuando escribe en el cuadro de búsqueda de hello, Hola panel izquierdo de las cuentas de almacenamiento de hello muestra que coinciden con el valor de búsqueda de Hola que ha especificado seguridad toothat punto. Por ejemplo, una búsqueda para todo el almacenamiento de cuentas cuyo nombre contenga **tarcher** se muestra en la siguiente captura de pantalla de hello:

![Búsqueda de cuenta de almacenamiento][11]

## <a name="next-steps"></a>Pasos siguientes
* [Administración de recursos de Azure Blob Storage con el Explorador de Storage (versión preliminar)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
