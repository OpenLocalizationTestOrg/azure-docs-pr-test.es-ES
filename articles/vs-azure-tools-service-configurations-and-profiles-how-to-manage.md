---
title: aaaHow toomanage configuraciones del servicio y perfiles | Documentos de Microsoft
description: "Obtenga información acerca de cómo toowork con los archivos de configuración de perfiles y las configuraciones de servicio | que almacena la configuración de entornos de implementación de Hola y configuración de publicación de servicios en la nube."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>¿Cómo toomanage configuraciones del servicio y perfiles
## <a name="overview"></a>Información general
Al publicar un servicio en la nube, Visual Studio almacena la información de configuración en dos tipos de archivos de configuración: configuraciones de servicio y perfiles. Configuraciones del servicio (archivos .cscfg) almacenan valores para entornos de implementación de Hola para un servicio de nube de Azure. Azure emplea estos archivos de configuración para administrar sus servicios en la nube. En Hola otra parte, el almacén de perfiles (archivos .azurePubxml) configuración de publicación de servicios en la nube. Esta configuración es un registro de los que elija cuando utilice Hola Asistente para la publicación y Visual Studio los utiliza localmente. Este tema se explica cómo toowork con ambos tipos de archivos de configuración.

## <a name="service-configurations"></a>Configuraciones de servicio
Puede crear varios toouse de configuraciones de servicio para cada uno de los entornos de implementación. Por ejemplo, podría crear una configuración de servicio para el entorno local de Hola que use toorun y probar una aplicación de Azure y otra configuración de servicio para el entorno de producción.

Puede agregar, eliminar, cambiar el nombre y modificar las configuraciones de servicio según sus necesidades. Puede administrar estas configuraciones del servicio desde Visual Studio, como se muestra en hello siguiente ilustración.

![Administrar configuraciones de servicio](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

También puede abrir hello **administrar configuraciones** cuadro de diálogo de páginas de propiedades del rol de Hola. propiedades de hello tooopen para un rol en su proyecto de Azure, abra el acceso directo de Hola para ese rol y, a continuación, elija **propiedades**. En hello **configuración** , expanda hello **configuración del servicio** lista y, a continuación, seleccione **administrar** tooopen hello **administrar configuraciones**cuadro de diálogo.

### <a name="tooadd-a-service-configuration"></a>tooadd una configuración del servicio
1. En el Explorador de soluciones, abra el menú contextual Hola Hola proyecto de Azure y, a continuación, seleccione **administrar configuraciones**.
   
    Hola **administrar configuraciones de servicio** aparece el cuadro de diálogo.
2. tooadd una configuración de servicio, debe crear una copia de una configuración existente. toodo, elija Configuración de Hola que desee toocopy desde la lista de nombres de hello y, a continuación, seleccione **crear copia**.
3. Configuración de servicio de hello toogive (opcional) un nombre diferente, elija Hola nueva configuración del servicio de lista de nombres de hello y, a continuación, seleccione **cambiar el nombre de**. Hola **nombre** cuadro de texto, escriba un nombre hello que desee toouse para esta configuración de servicio y, a continuación, seleccione **Aceptar**.
   
    Un nuevo archivo de configuración de servicio denominado ServiceConfiguration. [Nuevo nombre] .cscfg se agrega toohello proyecto de Azure en el Explorador de soluciones.

### <a name="toodelete-a-service-configuration"></a>toodelete una configuración del servicio
1. En el Explorador de soluciones, abra el menú contextual Hola Hola proyecto de Azure y, a continuación, seleccione **administrar configuraciones**.
   
    Hola **administrar configuraciones de servicio** aparece el cuadro de diálogo.
2. toodelete una configuración del servicio, elija la configuración de Hola que desea toodelete de hello **nombre** lista y, a continuación, seleccione **quitar**. Un cuadro de diálogo aparece tooverify que desea toodelete esta configuración.
3. Seleccione **Eliminar**.
   
     archivo de configuración de servicio de Hola se quita de hello proyecto de Azure en el Explorador de soluciones.

### <a name="toorename-a-service-configuration"></a>toorename una configuración del servicio
1. En el Explorador de soluciones, abra el acceso directo de Hola para hello proyecto de Azure y, a continuación, seleccione **administrar configuraciones**.
   
    Hola **administrar configuraciones de servicio** aparece el cuadro de diálogo.
2. toorename una configuración del servicio, elija Hola nueva configuración del servicio de hello **nombre** lista y, a continuación, seleccione **cambiar el nombre de**. Hola **nombre** cuadro de texto, escriba un nombre hello que desee toouse para esta configuración de servicio y, a continuación, seleccione **Aceptar**.
   
    nombre de Hola Hola servicio del archivo de configuración se cambia en hello proyecto de Azure en el Explorador de soluciones.

### <a name="toochange-a-service-configuration"></a>toochange una configuración del servicio
* Si desea toochange una configuración de servicio, abra Hola acceso directo rol específico de Hola que desee toochange Hola proyecto de Azure y, a continuación, seleccione **propiedades**. Vea [Cómo: configurar Roles de Hola para un servicio de nube de Azure con Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) para obtener más información.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Uso de los perfiles para realizar diferentes combinaciones de valores
Mediante el uso de un perfil, puede rellenar automáticamente en hello **Asistente para publicación** con diferentes combinaciones de valores para propósitos diferentes. Por ejemplo, puede tener un perfil para depuración y otro para de compilaciones de versión. En ese caso, el **depurar** tendría perfil **IntelliTrace** habilitado y Hola **depurar** configuración seleccionada y su **versión** perfil tendría **IntelliTrace** hello y deshabilitado **versión** configuración seleccionada. También puede usar varios perfiles toodeploy un servicio mediante una cuenta de almacenamiento diferente.

Al ejecutar Asistente de Hola para hello primera vez, se crea un perfil predeterminado. Visual Studio almacena el perfil de hello en un archivo que tiene una extensión .azurePubXml, que se agrega el proyecto de Azure bajo hello tooyour **perfiles** carpeta. Si especifica manualmente diferentes opciones al ejecutar el Asistente de hello más tarde, archivo hello se actualiza automáticamente. Antes de ejecutar Hola siguiendo el procedimiento, se debe haber publicado ya su servicio en la nube al menos una vez.

### <a name="tooadd-a-profile"></a>tooadd un perfil
1. Abra el menú contextual de hello para el proyecto de Azure y, a continuación, seleccione **publicar**.
2. Siguiente toohello **elegir como destino profile** lista, seleccione hello **Guardar perfil** botón como Hola siguiente ilustración se muestra. Con esto se crea un perfil.
   
    ![Crear un nuevo perfil](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Una vez creado el perfil de hello, seleccione **< administrar... >** en hello **elegir como destino profile** lista.
   
    Hola **administrar perfiles** aparece el cuadro de diálogo, como Hola siguiente ilustración se muestra.
   
    ![Administrar diálogo de perfiles](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. Hola **nombre** lista, elija un perfil y, a continuación, seleccione **crear copia**.
5. Elija hello **cerrar** botón.
   
    Hola nuevo perfil aparece en la lista de perfiles de destino de Hola.
6. Hola **elegir como destino profile** lista perfil Hola select que acaba de crear. configuración del Asistente para publicación de Hola se rellena con las opciones de Hola de perfil de hello seleccionado.
7. Seleccione hello **anterior** y **siguiente** botones toodisplay cada página del Asistente para publicación de hello y, a continuación, personalizar la configuración de Hola para este perfil. Para más información vea [Asistente para publicar aplicación de Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
8. Cuando termine de personalizar la configuración de hello, seleccione **siguiente** página de configuración de toogo toohello atrás. Hola perfil se guarda cuando se publica el servicio de hello utilizando estos valores o si selecciona **guardar** siguiente lista toohello de perfiles.

### <a name="toorename-or-delete-a-profile"></a>toorename o eliminar un perfil
1. Abra el menú contextual de hello para el proyecto de Azure y, a continuación, seleccione **publicar**.
2. Hola **elegir como destino profile** lista, seleccione **administrar**.
3. Hola **administrar perfiles** cuadro de diálogo, el perfil de hello select que desee toodelete y, a continuación, seleccione **quitar**.
4. En hello cuadro de diálogo de confirmación que aparece, seleccione **Aceptar**.
5. Seleccione **Cerrar**.

### <a name="toochange-a-profile"></a>toochange un perfil
1. Abra el menú contextual de hello para el proyecto de Azure y, a continuación, seleccione **publicar**.
2. Hola **elegir como destino profile** lista perfil Hola select que desea toochange.
3. Seleccione hello **anterior** y **siguiente** botones toodisplay Hola de cada página del Asistente para publicación y, a continuación, cambiar la configuración de Hola que desee. Para más información vea [Asistente para publicar aplicación de Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
4. Cuando termine de cambiar la configuración de hello, seleccione **siguiente** toogo atrás toohello **configuración** página.
5. (Opcional) seleccione **publicar** servicio en la nube hello toopublish utilizando una nueva configuración de Hola. Si no desea que toopublish su servicio en la nube en este momento y cerrar Hola Asistente para publicación, Visual Studio le pregunta si desea toosave Hola cambios toohello perfil.

## <a name="next-steps"></a>Pasos siguientes
toolearn sobre la configuración de otras partes de su proyecto de Azure desde Visual Studio, vea [configurar un proyecto de Azure](http://go.microsoft.com/fwlink/p/?LinkID=623075)

