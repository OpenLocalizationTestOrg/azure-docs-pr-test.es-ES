---
title: "aaaGet a trabajar con el catálogo de datos | Documentos de Microsoft"
description: "To-end tutorial presenta escenarios de Hola y funciones de catálogo de datos de Azure."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Introducción al Catálogo de datos de Azure
El Catálogo de datos de Azure es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección para recursos de datos empresariales. Si desea información detallada, consulte [¿Qué es el Catálogo de datos de Azure](data-catalog-what-is-data-catalog.md).

Este tutorial le ayudará a empezar a trabajar con el Catálogo de datos de Azure. Realizar Hola sigue los procedimientos de este tutorial:

| Procedimiento | Descripción |
|:--- |:--- |
| [Aprovisionamiento del catálogo de datos](#provision-data-catalog) |En este procedimiento, se aprovisiona o se configura Azure Data Catalog. Realice este paso solo si el catálogo de hello no se ha configurado antes. Solo puede haber un catálogo de datos por organización (dominio de Microsoft Azure Active Directory), aunque haya varias suscripciones asociadas a su cuenta de Azure. |
| [Registro de los recursos de datos](#register-data-assets) |En este procedimiento, deberá registrar activos de datos de la base de datos de ejemplo de Hola AdventureWorks2014 con el catálogo de datos Hola. El registro es proceso Hola de extraer metadatos estructurales clave como nombres, tipos y ubicaciones de origen de datos de Hola y copiar los metadatos toohello catálogo. Hello origen de datos y activos de datos siguen siendo donde son, pero usan metadatos Hola Hola catálogo toomake ellos más fácilmente reconocible y de fácil comprensión. |
| [Detección de los recursos de datos](#discover-data-assets) |En este procedimiento, utilizará activos de datos de portal toodiscover de catálogo de datos de Azure de Hola que se registraron en el paso anterior de Hola. Una vez registrado un origen de datos con el catálogo de datos de Azure, sus metadatos se indizan por servicio de Hola para que los usuarios pueden buscar fácilmente datos de Hola que necesitan. |
| [Anotación de los recursos de datos](#annotate-data-assets) |En este procedimiento, proporcionar anotaciones (información como descripciones, etiquetas, documentación o expertos) para hello activos de datos. Esta información complementa los metadatos de hello extraídos del origen de datos de Hola y más comprensibles toomore personas del origen de datos de hello toomake. |
| [Conectar toodata activos](#connect-to-data-assets) |En este procedimiento se abren los recursos de datos en herramientas de cliente integradas (como Excel y SQL Server Data Tools) y en una herramienta no integrada (SQL Server Management Studio). |
| [Administración de recursos de datos](#manage-data-assets) |En este procedimiento, se configura la seguridad de los recursos de datos. El catálogo de datos no le otorga a los usuarios acceder a los datos de toohello propio. propietario de Hola Hola del origen de datos controla el acceso a datos. <br/><br/> Con el catálogo de datos, puede detectar hello de vista y orígenes de datos **metadatos** relacionados con los orígenes de toohello registrados en el catálogo de Hola. Puede haber situaciones, sin embargo, donde los orígenes de datos deben ser visible toospecific solo a los usuarios o toomembers de grupos específicos. Para estos escenarios, puede utilizar la propiedad de tootake de catálogo de datos de activos de datos registrada dentro de visibilidad de Hola de hello catálogo y el control de activos de Hola que usted es el propietario. |
| [Eliminación de los recursos de datos](#remove-data-assets) |En este procedimiento, aprenderá cómo Hola a tooremove los activos de datos desde el catálogo de datos. |

## <a name="tutorial-prerequisites"></a>Requisitos previos de tutoriales
### <a name="azure-subscription"></a>Suscripción de Azure
tooset el catálogo de datos de Azure, debe ser propietario de Hola o copropietario de una suscripción de Azure.

Las suscripciones de Azure le ayudarán a organizar los recursos del servicio de acceso toocloud como el catálogo de datos. También le ayudan a controlar cómo se informa, factura y paga el uso de recursos. Cada suscripción puede tener una configuración de facturación y pago diferente, por lo que puede tener varias suscripciones y planes diferentes por departamento, proyecto, oficina regional, etc. Cada servicio en la nube pertenece tooa suscripción, y deberá toohave una suscripción antes de configurar el catálogo de datos. más información, consulte toolearn [administrar cuentas, suscripciones y roles administrativos](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos. Para más información, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/) .

### <a name="azure-active-directory"></a>Azure Active Directory
tooset el catálogo de datos de Azure, debe haber iniciado sesión con una cuenta de usuario de Azure Active Directory (Azure AD). Debe ser propietario de Hola o copropietario de una suscripción de Azure.  

Azure AD proporciona una manera sencilla para la identidad de negocio toomanage y acceso, tanto en la nube de Hola y local. Puede usar un único trabajo o escuela cuenta toosign en tooany en la nube o local de aplicación web. Catálogo de datos de Azure usa inicio de sesión en Azure AD tooauthenticate. más información, consulte toolearn [¿qué es Azure Active Directory](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Configuración de directivas de Azure Active Directory
Puede encontrarse con una situación donde puede iniciar sesión en el portal del catálogo de datos de Azure de toohello, pero al intentar toosign en la herramienta de registro de origen de datos de toohello, recibirá un mensaje de error que le impide el inicio de sesión. Este error puede producirse cuando se utiliza la red de la empresa de Hola o al realizar la conexión de red de empresa de hello exterior.

utiliza la herramienta de registro de Hello *autenticación mediante formularios* toovalidate inicios de sesión en Azure Active Directory. Para el inicio de sesión correcto, un administrador de Azure Active Directory debe habilitar la autenticación de formularios en hello *directiva de autenticación global*.

Con la directiva de autenticación global de hello, puede habilitar la autenticación por separado para la intranet y las conexiones de extranet, como se muestra en hello después de la imagen. Errores de inicio de sesión pueden producirse si la autenticación de formularios no está habilitada para red de Hola desde el que se está conectando.

 ![Directiva de autenticación global de Azure Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

Para más información, consulte [Configuración de directivas de autenticación](https://technet.microsoft.com/library/dn486781.aspx).

## <a name="provision-data-catalog"></a>Aprovisionamiento del catálogo de datos
Solo se puede aprovisionar un catálogo de datos por organización (dominio de Azure Active Directory). Por lo tanto, si el propietario de Hola o copropietario de una suscripción de Azure que pertenezca toothis dominio de Active Directory de Azure ya ha creado un catálogo, no será capaz de toocreate un catálogo nuevo incluso si tiene varias suscripciones de Azure. tootest si se ha creado un catálogo de datos de usuario de dominio de Active Directory de Azure, vaya toohello [página principal de catálogo de datos de Azure](http://azuredatacatalog.com) y compruebe si puede ver el catálogo de Hola. Si ya ha creado un catálogo para usted, omitir Hola pasos de procedimiento y vaya toohello la sección siguiente.    

1. Vaya toohello [página de servicio de catálogo de datos](https://azure.microsoft.com/services/data-catalog) y haga clic en **Introducción**.
   
    ![Catálogo de datos de Azure: página de aterrizaje de marketing](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Inicie sesión con una cuenta de usuario que es propietario de Hola o copropietario de una suscripción de Azure. Vea Hola después de página después de iniciar sesión.
   
    ![Catálogo de datos de Azure: aprovisionamiento del catálogo de datos](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Especifique un **nombre** para el catálogo de datos de hello, Hola **suscripción** desee toouse y Hola **ubicación** para el catálogo de Hola.
4. Expanda **Precios** y seleccione una **edición** de Azure Data Catalog (Gratis o Estándar).
    ![Catálogo de datos de Azure: selección de edición](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Expanda **usuarios catálogo** y haga clic en **agregar** tooadd a los usuarios para el catálogo de datos de Hola. Grupo toothis se agregan automáticamente.
    ![Catálogo de datos de Azure: usuarios](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Expanda **los administradores del catálogo** y haga clic en **agregar** tooadd administradores adicionales para el catálogo de datos de Hola. Grupo toothis se agregan automáticamente.
    ![Catálogo de datos de Azure: administradores](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Haga clic en **crear catálogo** catálogo de datos de hello toocreate para su organización. Vea página de inicio de Hola de catálogo de datos de hello después de crearlo.
    ![Azure Data Catalog: creado](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Buscar un catálogo de datos en hello portal de Azure
1. En una pestaña independiente en el Explorador de web de Hola o en una ventana del explorador web independiente, vaya toohello [portal de Azure](https://portal.azure.com) y de inicio de sesión con Hola misma cuenta que se toocreate usado Hola catálogo de datos en el paso anterior de Hola.
2. Seleccione **Examinar** y haga clic en **Catálogo de datos**.
   
    ![Catálogo de datos de Azure--examinar Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) vea datos Hola de catálogo que ha creado.
   
    ![Catálogo de datos de Azure: visualización de catálogo en lista](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Haga clic en el catálogo de Hola que ha creado. Vea hello **el catálogo de datos** hoja en el portal de Hola.
   
   ![Catálogo de datos de Azure: hoja en el portal ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. Puede ver las propiedades del catálogo de datos de Hola y actualizarlos. Por ejemplo, haga clic en **tarifa** y cambiar Hola edición.
   
    ![Catálogo de datos de Azure: plan de tarifa](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Base de datos de ejemplo Adventure Works
En este tutorial, registrar activos de datos (tablas) de base de datos de ejemplo de Hola AdventureWorks2014 para hello motor de base de datos de SQL Server, pero puede utilizar cualquier origen de datos admitidos si prefiere toowork con los datos que es el rol de tooyour conocidas y pertinentes. Para ver una lista de los orígenes de datos compatibles, consulte [Orígenes de datos compatibles con Azure Data Catalog](data-catalog-dsr.md).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Instalar la base de datos de Adventure Works 2014 OLTP Hola
base de datos de Adventure Works Hello es compatible con escenarios de procesamiento de transacciones en línea estándar para un fabricante de bicicletas ficticio (Adventure Works Cycles), que contiene los productos, ventas y compras. En este tutorial registrará información acerca de los productos en Azure Data Catalog.

datos de ejemplo de Adventure Works de Hola tooinstall:

1. Descargue el archivo [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) en CodePlex.
2. base de datos de toorestore hello en su equipo, siga las instrucciones de hello en [restaurar una copia de seguridad de base de datos mediante SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), o siguiendo estos pasos:
   1. Abra SQL Server Management Studio y conéctese toohello motor de base de datos de SQL Server.
   2. Haga clic con el botón derecho en **Bases de datos** y seleccione **Restaurar base de datos**.
   3. En **Restaurar base de datos**, haga clic en hello **dispositivo** opción **origen** y haga clic en **examinar**.
   4. En **Seleccionar dispositivos de copia de seguridad**, haga clic en **Agregar**.
   5. Carpeta de toohello vaya donde tenga hello **AdventureWorks2014.bak** archivo, archivo hello seleccione y haga clic en **Aceptar** tooclose hello **buscar el archivo de copia de seguridad** cuadro de diálogo.
   6. Haga clic en **Aceptar** tooclose hello **seleccionar dispositivos de copia de seguridad** cuadro de diálogo.    
   7. Haga clic en **Aceptar** tooclose hello **Restore Database** cuadro de diálogo.

Ahora puede registrar activos de datos de base de datos de ejemplo de Adventure Works de hello mediante el catálogo de datos.

## <a name="register-data-assets"></a>Registro de los recursos de datos
En este ejercicio, utilizará activos de datos de hello registro herramienta tooregister de base de datos de Adventure Works Hola con el catálogo de Hola. Registro es Hola proceso de extracción de metadatos estructurales de la clave como nombres, tipos y ubicaciones de Hola origen de datos y activos de hello contiene y copiar metadatos toohello catálogo. Hello origen de datos y activos de datos siguen siendo donde son, pero usan metadatos Hola Hola catálogo toomake ellos más fácilmente reconocible y de fácil comprensión.

### <a name="register-a-data-source"></a>Registro de un origen de datos
1. Vaya toohello [página principal de catálogo de datos de Azure](http://azuredatacatalog.com) y haga clic en **publicar datos**.
   
   ![Catálogo de datos de Azure: botón Publicar datos](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Haga clic en **Iniciar aplicación** toodownload, la instalación y la herramienta de registro de ejecución hello en el equipo.
   
   ![Catálogo de datos de Azure: botón Iniciar](media/data-catalog-get-started/data-catalog-launch-application.png)
3. En hello **bienvenida** página, haga clic en **iniciar sesión en** y escriba sus credenciales.     
   
    ![Catálogo de datos de Azure: página principal](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. En hello **catálogo de datos de Microsoft Azure** página, haga clic en **SQL Server** y **siguiente**.
   
    ![Catálogo de datos de Azure: orígenes de datos](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Especifique las propiedades de conexión de SQL Server de Hola para **AdventureWorks2014** (vea el siguiente ejemplo de Hola) y haga clic en **conectar**.
   
   ![Catálogo de datos de Azure: configuración de conexión con SQL Server](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Registrar Hola metadatos de los datos activos. En este ejemplo, registrar **producción/producto** objetos del espacio de nombres de producción de AdventureWorks de hello:
   
   1. Hola **jerarquía del servidor** de árbol, expanda **AdventureWorks2014** y haga clic en **producción**.
   2. Seleccione **Product**, **ProductCategory**, **ProductDescription** y **ProductPhoto** mediante Ctrl + clic.
   3. Haga clic en hello **mover flecha seleccionado** (**>**). Esta acción mueve todos los objetos seleccionados en hello **toobe de objetos registrado** lista.
      
      ![Catálogo de datos de Azure: examen o selección de objetos](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Seleccione **incluyen una vista previa del** tooinclude una vista previa de instantánea de datos de Hola. instantánea de Hello incluye too20 registros de cada tabla, y se copia en el catálogo de Hola.
   5. Seleccione **incluyen el perfil de datos** tooinclude una instantánea de las estadísticas del objeto hello para el perfil de datos de hello (por ejemplo: los valores mínimos, máximos y promedio para una columna, el número de filas).
   6. Hola **agregar etiquetas** , escriba **adventure funciona, ciclos**. Esta acción agrega etiquetas de búsqueda a estos recursos de datos. Las etiquetas son una excelente manera de toohelp a los usuarios buscar un origen de datos registrada.
   7. Especificar nombre de Hola de un **experto** en estos datos (opcionales).
      
      ![Tutorial de catálogo de datos de Azure--toobe objetos registrado](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. Haga clic en **REGISTRAR**. Catálogo de datos de Azure registra los objetos seleccionados. En este ejercicio, se registran los objetos de hello seleccionado de Adventure Works. herramienta de registro de Hello extrae metadatos del recurso de datos de Hola y copia los datos en el servicio del catálogo de datos de Azure Hola. Hola datos permanecen donde se encuentra actualmente y permanece bajo control de Hola de administradores de Hola y directivas del sistema actual Hola.
      
      ![Catálogo de datos de Azure: objetos registrados](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. Haga clic en los objetos de origen de datos registrada de toosee **Portal de vista**. En el portal del catálogo de datos de Azure hello, confirme que ve todas las base de datos de hello en vista de cuadrícula de Hola y cuatro tablas.
      
      ![Objetos en el portal del catálogo de datos de Azure de Hola ](media/data-catalog-get-started/data-catalog-view-portal.png)

En este ejercicio, objetos de base de datos de ejemplo de Hola Adventure Works ha registrado para que puedan fácilmente detectar los usuarios a través de su organización. En el siguiente ejercicio hello, aprenderá cómo toodiscover había registrado activos de datos.

## <a name="discover-data-assets"></a>Detección de los recursos de datos
La detección en el Catálogo de datos de Azure usa dos mecanismos principales: la búsqueda y el filtrado.

La búsqueda es toobe diseñada intuitiva y eficaz. De forma predeterminada, los términos de búsqueda se comparan con cualquier propiedad de catálogo de hello, incluidas las anotaciones proporcionado por el usuario.

El filtrado está diseñado toocomplement buscar. Puede seleccionar características específicas como expertos, tipo de origen de datos, el tipo de objeto y tooview etiquetas coincidentes activos de datos y búsqueda de tooconstrain da como resultado toomatching activos.

Mediante una combinación de búsqueda y filtrado, puede navegar rápidamente los orígenes de datos de Hola que se han registrado con recursos de datos de catálogo de datos de Azure toodiscover Hola que necesita.

En este ejercicio, utilice activos de datos de portal toodiscover Hola el catálogo de datos que registró en el ejercicio anterior Hola. Para más información acerca de la sintaxis de búsqueda, consulte [Referencia de sintaxis de búsqueda en Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) .

Siguientes son algunos ejemplos para detectar recursos de datos en el catálogo de Hola.  

### <a name="discover-data-assets-with-basic-search"></a>Detección de recursos de datos con la búsqueda básica
La búsqueda básica permite buscar en un catálogo con uno o varios términos de búsqueda. Los resultados son los activos que coinciden en cualquier propiedad con uno o varios de los términos de hello especificados.

1. Haga clic en **inicio** en el portal del catálogo de datos de Azure de Hola. Si ha cerrado el explorador web de hello, vaya toohello [página principal de catálogo de datos de Azure](https://www.azuredatacatalog.com).
2. En el cuadro de búsqueda de hello, escriba `cycles` y presione **ENTRAR**.
   
    ![Catálogo de datos de Azure: búsqueda de texto básica](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Confirme que ve todos los cuatro tablas y la base de datos de hello (AdventureWorks2014) en los resultados de Hola. Puede cambiar entre **vista de cuadrícula** y **vista de lista** haciendo clic en botones de barra de herramientas de hello como se muestra en hello después de la imagen. Tenga en cuenta esa palabra clave de búsqueda de Hola se resalta en resultados de la búsqueda de hello porque hello **resaltar** opción es **ON**. También puede especificar el número de Hola de **resultados por página** en resultados de búsqueda.
   
    ![Catálogo de datos de Azure: resultados de búsqueda de texto básica](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Hola **búsquedas** panel está en deja de Hola y Hola **propiedades** panel está en hello derecho. En hello **búsquedas** panel, puede cambiar los criterios de búsqueda y filtrar los resultados. Hola **propiedades** panel muestra las propiedades de un objeto seleccionado en la cuadrícula de Hola o lista.
4. Haga clic en **producto** en los resultados de búsqueda de Hola. Haga clic en hello **vista previa**, **columnas**, **perfil de datos**, y **documentación** pestañas o haga clic en el panel inferior Hola de hello flecha tooexpand.  
   
    ![Catálogo de datos de Azure: panel inferior](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    En hello **vista previa** pestaña, verá una vista previa de los datos de Hola Hola **producto** tabla.  
5. Haga clic en hello **columnas** ficha toofind detalles acerca de las columnas (como **nombre** y **tipo de datos**) en el recurso de datos de Hola.
6. Haga clic en hello **perfil de datos** ficha toosee Hola de generación de perfiles de datos (por ejemplo: número de filas, el tamaño de datos, o el valor mínimo de una columna) en el recurso de datos de Hola.
7. Filtrar los resultados de hello mediante **filtros** Hola izquierda. Por ejemplo, haga clic en **tabla** para **tipo de objeto**, y ver solo las tablas de hello cuatro, no Hola base de datos.
   
    ![Catálogo de datos de Azure: resultados de búsqueda con filtro](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Detección de recursos de datos con ámbito de propiedad
Propiedad ámbito ayuda a que detectar los activos de datos donde se compara el término de búsqueda de hello con hello propiedad especificada.

1. Desactive hello **tabla** filtrar en **tipo de objeto** en **filtros**.  
2. En el cuadro de búsqueda de hello, escriba `tags:cycles` y presione **ENTRAR**. Vea [referencia de la sintaxis de búsqueda del catálogo de datos](https://msdn.microsoft.com/library/azure/mt267594.aspx) para todas las propiedades que puede utilizar para la búsqueda de catálogo de datos de Hola de Hola.
3. Confirme que ve todos los cuatro tablas y la base de datos de hello (AdventureWorks2014) en los resultados de Hola.  
   
    ![Catálogo de datos: resultados de búsqueda de ámbito de propiedad](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Guardar búsqueda Hola
1. Hola **búsquedas** panel Hola **búsqueda actual** sección, escriba un nombre para la búsqueda de Hola y haga clic en **guardar**.
   
    ![Catálogo de datos de Azure: guardado de búsqueda](media/data-catalog-get-started/data-catalog-save-search.png)
2. Confirme que la búsqueda de hello guardado se muestra en **búsquedas guardadas**.
   
    ![Catálogo de datos de Azure: búsquedas guardadas](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Seleccione una de las acciones de Hola que puede realizar en la búsqueda de hello guardado (**cambiar el nombre de**, **eliminar**, **Guardar como predeterminado** búsqueda).
   
    ![Catálogo de datos de Azure: opciones de búsquedas guardadas](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Operadores booleanos
Cualquier búsqueda puede ampliarse o restringirse con operadores booleanos.

1. En el cuadro de búsqueda de hello, escriba `tags:cycles AND objectType:table`y presione **ENTRAR**.
2. Confirme que ve únicamente las tablas (no base de datos de Hola) en los resultados de Hola.  
   
    ![Catálogo de datos de Azure: operador booleano en búsqueda](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Agrupación con paréntesis
Agrupar con paréntesis, puede agrupar las partes de hello consulta tooachieve lógico de aislamiento, especialmente junto con los operadores booleanos.

1. En el cuadro de búsqueda de hello, escriba `name:product AND (tags:cycles AND objectType:table)` y presione **ENTRAR**.
2. Confirme que ve solo hello **producto** tabla de resultados de la búsqueda de Hola.
   
    ![Catálogo de datos de Azure: búsqueda con agrupación](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Operadores de comparación
Con los operadores de comparación puede usar comparaciones diferentes de la igualdad de propiedades que tengan tipos de datos numéricos y de fechas.

1. En el cuadro de búsqueda de hello, escriba `lastRegisteredTime:>"06/09/2016"`.
2. Desactive hello **tabla** filtrar en **tipo de objeto**.
3. Presione **ENTRAR**.
4. Confirme que aparece hello **producto**, **ProductCategory**, **ProductDescription**, y **ProductPhoto** hello y tablas Base de datos AdventureWorks2014 registrado en resultados de búsqueda.
   
    ![Catálogo de datos de Azure: resultados de búsqueda con comparación](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Vea [cómo activos de datos de toodiscover](data-catalog-how-to-discover.md) para obtener información detallada acerca de la detección de activos de datos y [referencia de la sintaxis de búsqueda del catálogo de datos](https://msdn.microsoft.com/library/azure/mt267594.aspx) de sintaxis de búsqueda.

## <a name="annotate-data-assets"></a>Anotación de los recursos de datos
En este ejercicio, use tooannotate portal del catálogo de datos de Azure de hello (agregar información como descripciones, etiquetas o expertos) activos de datos que se haya registrado previamente en el catálogo de Hola. anotaciones de Hello complementan y mejoran Hola metadatos estructurales extraídos de origen de datos de Hola durante el registro y hace mucho más fácil toodiscover de activos de datos de Hola y entenderán.

En este ejercicio, se anota un único recurso de datos (ProductPhoto). Agregue un nombre descriptivo y un recurso de datos de descripción toohello ProductPhoto.  

1. Vaya toohello [página principal de catálogo de datos de Azure](https://www.azuredatacatalog.com) y buscar con `tags:cycles` activos de datos de hello toofind ha registrado.  
2. Haga clic en **ProductPhoto** en los resultados de la búsqueda.  
3. Escriba **imágenes de producto** para **Nombre_descriptivo** y **fotografías de productos de materiales de marketing** para hello **descripción**.
   
    ![Catálogo de datos de Azure: descripción de ProductPhoto](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Hola **descripción** otros ayuda a detectar y comprender por qué y cómo toouse Hola seleccionado datos activos. También se pueden agregar otras etiquetas y ver columnas. Ahora puede probar activos de datos de búsqueda y filtrado toodiscover mediante el uso de metadatos descriptivos Hola has agregado toohello catálogo.

También puede hacer Hola siguiente de esta página:

* Agregar a expertos de los activos de datos de Hola. Haga clic en **agregar** en hello **expertos** área.
* Agregar etiquetas a nivel de conjunto de datos de Hola. Haga clic en **agregar** en hello **etiquetas** área. Una etiqueta puede ser una etiqueta de usuario o una etiqueta de glosario. Hola edición estándar de catálogo de datos incluye glosarios empresariales que ayuda a los administradores del catálogo definen una taxonomía empresarial central. Después, los usuarios del catálogo pueden anotar los recursos de datos con los términos del glosario. Para obtener más información, vea [cómo tooset seguridad Hola glosarios empresariales para etiquetar los rige](data-catalog-how-to-business-glossary.md)
* Agregar etiquetas a nivel de columna de Hola. Haga clic en **agregar** en **etiquetas** columna Hola se desea tooannotate.
* Agregue la descripción en el nivel de columna de Hola. En **Descripción** , escriba la descripción de la columna. También puede ver metadatos de descripción de hello extraídos del origen de datos de Hola.
* Agregar **solicitar acceso** información que se muestra a los usuarios cómo acceder toorequest a toohello datos activos.
  
    ![Catálogo de datos de Azure: incorporación de etiquetas y descripciones](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Elija hello **documentación** y a proporcionar documentación de los activos de datos de Hola. Con la documentación del catálogo de datos de Azure, puede usar el catálogo de datos como un toocreate una descripción completa de los activos de datos de repositorio de contenido.
  
    ![Catálogo de datos de Azure: pestaña Documentación](media/data-catalog-get-started/data-catalog-documentation.png)

También puede agregar un activos de datos de toomultiple de anotación. Por ejemplo, puede seleccionar todos los activos de datos de hello registrado y especificar a un experto para ellos.

![Catálogo de datos de Azure: anotación de varios recursos de datos](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Catálogo de datos de Azure admite un tooannotations de enfoque multitud de origen. Cualquier usuario del catálogo de datos puede agregar etiquetas (usuario o glosario), descripciones y otros metadatos, para que cualquier usuario con una perspectiva de un recurso de datos y su uso puede tener esa perspectiva capturado y tooother disponibles a los usuarios.

Vea [cómo activos de datos tooannotate](data-catalog-how-to-annotate.md) para obtener información detallada acerca de las anotaciones de activos de datos.

## <a name="connect-toodata-assets"></a>Conectar toodata activos
En este ejercicio, se abren recursos de datos en una herramienta cliente integrada (Excel) y en una herramienta no integrada (SQL Server Management Studio) mediante la información de conexión.

> [!NOTE]
> Es importante tooremember que el catálogo de datos no le ofrece acceso a origen de datos real de toohello, resulta más fácil para toodiscover simplemente y entender. Cuando se conecta el origen de datos de tooa, Hola aplicación cliente que elige usa credenciales de las ventanas o solicita las credenciales según sea necesario. Si no se previamente se ha concedido el origen de datos de access toohello, deberá toobe concedido acceso para poder conectarse.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Conexión tooa datos activos de Excel
1. Seleccione **Product** en los resultados de la búsqueda. Haga clic en **Open In** en la barra de herramientas de Hola y haga clic en **Excel**.
   
    ![Catálogo de datos de Azure--conectarse toodata activo](media/data-catalog-get-started/data-catalog-connect1.png)
2. Haga clic en **abiertos** en la ventana emergente de descarga de Hola. Esta experiencia puede variar según el Explorador de Hola.
   
    ![Catálogo de datos de Azure: archivo de conexión de Excel descargado](media/data-catalog-get-started/data-catalog-download-open.png)
3. Hola **aviso de seguridad de Microsoft Excel** ventana, haga clic en **habilitar**.
   
    ![Catálogo de datos de Azure: mensaje emergente de seguridad de Excel](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Mantener valores predeterminados de Hola Hola **importar datos** cuadro de diálogo y haga clic en **Aceptar**.
   
    ![Catálogo de datos de Azure: datos de importación de Excel](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Ver orígenes de datos de hello en Excel.
   
    ![Catálogo de datos de Azure: tabla de producto en Excel](media/data-catalog-get-started/data-catalog-connect2.png)

En este ejercicio, se conectó activos toodata detectados mediante el catálogo de datos. Con el portal del catálogo de datos de Azure hello, puede conectarse directamente mediante el uso de las aplicaciones de cliente de hello integradas en hello **abierto en** menú. También puede conectar con cualquier aplicación que elija mediante el uso de información de ubicación de hello conexión incluido en los metadatos del activo Hola. Por ejemplo, puede usar datos de saludo del tooaccess de base de datos de SQL Server Management Studio tooconnect toohello AdventureWorks2014 en hello los activos de datos registrados en este tutorial.

1. Abra **SQL Server Management Studio**.
2. Hola **conectar tooServer** diálogo cuadro, escriba el nombre del servidor de Hola de hello **propiedades** panel en el portal del catálogo de datos de Azure de Hola.
3. Usar autenticación adecuado y recurso de datos de credenciales tooaccess Hola. Si no tiene acceso, use información de hello **solicitar acceso** tooget de campo se.
   
    ![Catálogo de datos de Azure: solicitud de acceso](media/data-catalog-get-started/data-catalog-request-access.png)

Haga clic en **ver las cadenas de conexión** tooview y copie ADF.NET, ODBC y OLE DB conexión cadenas toohello Portapapeles para utilizarlo en la aplicación.

## <a name="manage-data-assets"></a>Administración de recursos de datos
En este paso, vea cómo tooset la seguridad de sus activos de datos. El catálogo de datos no le otorga a los usuarios acceder a los datos de toohello propio. propietario de Hola Hola del origen de datos controla el acceso a datos.

Puede usar el catálogo de datos toodiscover los orígenes de datos y metadatos de hello tooview relacionados con los orígenes de toohello registrados en el catálogo de Hola. Puede haber casos, sin embargo, en los orígenes de datos solo deben resultar toospecific visible a los usuarios o toomembers de grupos específicos. En estos casos, puede usar propiedad tootake del catálogo de datos de activos de datos registrado en el catálogo de Hola y toothen controlar la visibilidad de Hola de activos de Hola que usted es el propietario.

> [!NOTE]
> capacidades de administración de Hola que se describe en este ejercicio sólo están disponibles en hello edición estándar de catálogo de datos de Azure, no en Hola edición gratuita.
> En el catálogo de datos, puede tomar posesión de activos de datos, agregar los copropietarios toodata activos y establecer la visibilidad de Hola de activos de datos.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>Toma de propiedad de los recursos de datos y restricción de la visibilidad
1. Vaya toohello [página principal de catálogo de datos de Azure](https://www.azuredatacatalog.com). Hola **búsqueda** texto cuadro, escriba `tags:cycles` y presione **ENTRAR**.
2. Haga clic en un elemento de lista de resultados de Hola y haga clic en **Take Ownership** en la barra de herramientas de Hola.
3. Hola **administración** sección de hello **propiedades** del panel, haga clic en **Take Ownership**.
   
    ![Catálogo de datos de Azure: toma de propiedad](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. visibilidad de toorestrict, elija **propietarios y usuarios de estas** en hello **visibilidad** sección y haga clic en **agregar**. Escriba las direcciones de correo electrónico del usuario en el cuadro de texto hello y presione **ENTRAR**.
   
    ![Catálogo de datos de Azure: restricción de acceso](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Eliminación de los recursos de datos
En este ejercicio, usar el catálogo de datos de Azure portal tooremove vista previa de datos de activos de datos registrados de hello y eliminar activos de datos de catálogo de Hola.

En Azure Data Catalog se pueden eliminar uno o varios recursos.

1. Vaya toohello [página principal de catálogo de datos de Azure](https://www.azuredatacatalog.com).
2. Hola **búsqueda** texto cuadro, escriba `tags:cycles` y haga clic en **ENTRAR**.
3. Seleccione un elemento de lista de resultados de Hola y haga clic en **eliminar** en barra de herramientas de hello como se muestra en hello después de imagen:
   
    ![Catálogo de datos de Azure: eliminación de elemento de cuadrícula](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Si utiliza la vista de lista de hello, Hola casilla es toohello izquierda del elemento de hello tal como se muestra en hello después de imagen:
   
    ![Catálogo de datos de Azure: eliminación de elemento de lista](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    También puede seleccionar varios activos de datos y eliminarlos tal como se muestra en hello después de imagen:
   
    ![Catálogo de datos de Azure: eliminación de varios recursos de datos](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> Hola comportamiento predeterminado del catálogo de hello es tooallow cualquier tooregister de usuario de cualquier origen de datos y tooallow cualquier usuario toodelete cualquier recurso de datos que se ha registrado. capacidades de administración de Hello incluidas en hello edición estándar de catálogo de datos de Azure proporcionan opciones adicionales para la toma de posesión de activos, restringir quién puede detectar activos y para restringir quién puede eliminar activos.
> 
> 

## <a name="summary"></a>Resumen
En este tutorial ha explorado las funcionalidades esenciales del Catálogo de datos de Azure, entre las que se incluyen el registro, la anotación, la detección y la administración de recursos de datos empresariales. Ahora que ha completado el tutorial de hello, es hora de tooget iniciado. Puede empezar hoy en día registrando los orígenes de datos de hello que dependen de usted y su equipo y e invitar a catálogo de compañeros toouse Hola.

## <a name="references"></a>Referencias
* [¿Cómo tooregister activos de datos](data-catalog-how-to-register.md)
* [¿Cómo toodiscover activos de datos](data-catalog-how-to-discover.md)
* [¿Cómo tooannotate activos de datos](data-catalog-how-to-annotate.md)
* [¿Cómo toodocument activos de datos](data-catalog-how-to-documentation.md)
* [Cómo tooconnect toodata activos](data-catalog-how-to-connect.md)
* [¿Cómo toomanage activos de datos](data-catalog-how-to-manage.md)

