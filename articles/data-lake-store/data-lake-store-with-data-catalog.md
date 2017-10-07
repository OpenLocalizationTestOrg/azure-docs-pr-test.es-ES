---
title: "aaaRegister datos de almacén de Data Lake en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Registro de datos del Almacén de Data Lake en el Catálogo de datos de Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Registro de datos del Almacén de Data Lake en el Catálogo de datos de Azure
En este artículo, aprenderá cómo las toointegrate Azure Data Lake almacenar con el catálogo de datos toomake los datos que se pueda detectables dentro de una organización mediante la integración con el catálogo de datos. Para más información sobre la catalogación de datos, consulte [¿Qué es el Catálogo de datos de Azure?](../data-catalog/data-catalog-what-is-data-catalog.md). escenarios de toounderstand en el que puede usar el catálogo de datos, vea [escenarios comunes de catálogo de datos de Azure](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Habilite su suscripción de Azure** para la versión preliminar pública de Azure Data Lake Store. Consulte las [instrucciones](data-lake-store-get-started-portal.md).
* **Cuenta del Almacén de Azure Data Lake**. Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md). Para este tutorial, vamos a crear una cuenta de Almacén de datos de Data Lake denominada **datacatalogstore**.

    Una vez haya creado la cuenta de hello, cargue un tooit de conjunto de datos de ejemplo. Para este tutorial, nos gustaría cargar todos los archivos .csv de hello en hello **AmbulanceData** carpeta Hola [repositorio de Git de Azure datos Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). Puede usar varios clientes, como [Azure Storage Explorer](http://storageexplorer.com/), contenedor de blobs de tooupload datos tooa.
* **Catálogo de datos de Azure**. Su organización ya debe tener un Catálogo de datos de Azure creado. Se permite solo un catálogo por cada organización.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Registro del Almacén de Data Lake como origen para el Catálogo de datos

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Vaya demasiado`https://azure.microsoft.com/services/data-catalog`y haga clic en **Introducción**.
2. Inicie sesión en el portal del catálogo de datos de Azure de Hola y haga clic en **publicar datos**.

    ![Registrar un origen de datos](./media/data-lake-store-with-data-catalog/register-data-source.png "Registrar un origen de datos")
3. En la página siguiente de hello, haga clic en **Iniciar aplicación**. Se descargará el archivo de manifiesto de aplicación hello en el equipo. Haga doble clic en la aplicación de hello toostart de hello archivo de manifiesto.
4. En la página de bienvenida de hello, haga clic en **iniciar sesión en**y escriba sus credenciales.

    ![Pantalla de bienvenida](./media/data-lake-store-with-data-catalog/welcome.screen.png "Pantalla de bienvenida")
5. En la página Seleccionar un origen de datos de hello, seleccione **Azure Data Lake**y, a continuación, haga clic en **siguiente**.

    ![Seleccionar origen de datos](./media/data-lake-store-with-data-catalog/select-source.png "Seleccionar origen de datos")
6. En la página siguiente de hello, proporcionar Hola nombre de cuenta de almacén de Data Lake que deseas tooregister en el catálogo de datos. Deje Hola otras opciones como valor predeterminado y, a continuación, haga clic en **conectar**.

    ![Conectar toodata origen](./media/data-lake-store-with-data-catalog/connect-to-source.png "conectar toodata origen")
7. página siguiente de Hello puede dividirse en hello después de segmentos.

    a. Hola **jerarquía del servidor** cuadro representa la estructura de carpetas de cuenta de almacén de Data Lake Hola. **$Root** representa Hola raíz de la cuenta de almacén de Data Lake, y **AmbulanceData** representa Hola carpeta creada en la raíz de Hola de hello cuenta de almacén de Data Lake.

    b. Hola **objetos disponibles** cuadro muestra hello archivos y carpetas en hello **AmbulanceData** carpeta.

    c. **Objetos toobe registrado cuadro** Hola de listas de archivos y carpetas que desea que tooregister en el catálogo de datos.

    ![Ver estructura de datos](./media/data-lake-store-with-data-catalog/view-data-structure.png "Ver estructura de datos")
8. Para este tutorial, debe registrar todos los archivos de hello en el directorio de Hola. Para ello, haga clic en hello (![mover objetos](./media/data-lake-store-with-data-catalog/move-objects.png "mover objetos")) toomove botón Hola a todos los archivos demasiado**toobe de objetos registrado** cuadro.

    Dado que datos de Hola se registrará en un catálogo de datos de toda la organización, es un recomendado enfocar tooadd algunos metadatos que se pueden usar más adelante tooquickly localizar datos Hola. Por ejemplo, puede agregar una dirección de correo electrónico para el propietario de datos de hello (por ejemplo, uno que está cargando datos hello) o agregar una etiqueta tooidentify Hola de datos. en la siguiente captura de pantalla de Hello muestra una etiqueta que se agregue toohello datos.

    ![Ver estructura de datos](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "Ver estructura de datos")

    Haga clic en **Registrar**.
9. Hello captura de pantalla siguiente indica que se ha registrado correctamente datos de Hola Hola catálogo de datos.

    ![Registro completo](./media/data-lake-store-with-data-catalog/registration-complete.png "Ver estructura de datos")
10. Haga clic en **Portal de vista** toogo copia portal del catálogo de datos de toohello y compruebe que puede ahora Hola acceso registrado datos desde el portal de Hola. datos de Hola de toosearch, se puede utilizar la etiqueta de Hola que usó al registrar datos de Hola.

     ![Buscar datos en el catálogo](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Buscar datos en el catálogo")
11. Ahora puede realizar operaciones como agregar anotaciones y datos de toohello de documentación. Para obtener más información, vea Hola siguientes vínculos.

    * [Anotación de orígenes de datos](../data-catalog/data-catalog-how-to-annotate.md)
    * [Orígenes de datos de documentos](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Otras referencias
* [Anotación de orígenes de datos](../data-catalog/data-catalog-how-to-annotate.md)
* [Orígenes de datos de documentos](../data-catalog/data-catalog-how-to-documentation.md)
* [Integración del Almacén de Data Lake con otros servicios de Azure](data-lake-store-integrate-with-other-services.md)
