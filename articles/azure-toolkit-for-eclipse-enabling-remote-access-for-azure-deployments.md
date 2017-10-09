---
title: aaaEnabling acceso remoto para las implementaciones de Azure en Eclipse
description: "Obtenga información acerca de cómo tener acceso tooenable remoto para las implementaciones de Azure mediante Hola Kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Habilitación del acceso remoto para implementaciones de Azure en Eclipse
toohelp solucionar problemas de las implementaciones, puede habilitar y usar acceso remoto tooconnect toohello virtual machine hospeda la implementación. Hola funcionalidad de acceso remoto se basa en hello protocolo de escritorio remoto (RDP). Puede configurar el acceso remoto para la implementación después de que haya publicado tooAzure, o si está usando Eclipse con un sistema operativo Windows, puede configurar el acceso remoto antes de publicar tooAzure. Tenga en cuenta que necesitará a un cliente de escritorio remoto que sea compatible con el sistema operativo en la máquina virtual de orden tooconnect tooyour de la implementación de Azure.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Cómo tooenable acceso remoto antes de implementar tooAzure
> [!NOTE]
> tooenable acceso remoto antes de implementar su aplicación tooAzure, deberá toobe ejecutarse Eclipse en Windows.
> 
> 

Hello siguiente imagen muestra hello **acceso remoto** cuadro de diálogo de propiedades utiliza tooenable el acceso remoto.

![][ic719494]

Hay dos Hola de toodisplay maneras **acceso remoto** cuadro de diálogo de propiedades:

* Haga clic en hello **avanzadas** vínculo Hola **acceso remoto** sección de hello **publicar tooAzure** cuadro de diálogo.

* Abra hello **propiedades** cuadro de diálogo de su proyecto de Azure.

Cuando crea un nuevo proyecto de implementación de Azure, el proyecto de hello no tendrá acceso remoto habilitado de forma predeterminada. Sin embargo, puede habilitar fácilmente acceso remoto mediante la especificación de nombre de usuario de hello y una contraseña en hello **publicar tooAzure** cuadro de diálogo. contraseña de acceso remoto de Hola se cifra mediante certificados X.509. Si no usa proporcionar su propio certificado, cifrado de Hola se basa en un certificado autofirmado acompaña Hola complemento de Azure para Eclipse. Este certificado autofirmado está en hello **cert** carpeta de su proyecto de Azure, almacenado como un archivo de certificado público (SampleRemoteAccessPublic.cer) y archivo de certificado como un intercambio de información Personal (PFX) () SampleRemoteAccessPrivate.pfx). Hola esta última contiene la clave privada de hello certificado de Hola y tiene una contraseña predeterminada, **Password1**. Sin embargo, puesto que esta contraseña es de dominio público, certificado predeterminado de hello debe usarse solo para el aprendizaje, no para una implementación de producción. Tan distinto con fines de aprendizaje, cuando desee que las sesiones remotas de tooenabled para las implementaciones, se debe hacer clic en hello **avanzadas** vínculo Hola **publicar tooAzure** diálogo toospecify su propio certificado. Tenga en cuenta que necesitará versión PFX de hello tooupload del servicio de tooyour hospedado de certificado de hello en hello Portal de administración de Azure, por lo que Azure pueda descifrar la contraseña de usuario de Hola.

resto de Hola de tutorial de hello muestra cómo tener acceso tooenable remoto para un proyecto de implementación de Azure que se creó inicialmente con acceso remoto deshabilitado. Para los fines de este tutorial, vamos a crear un certificado autofirmado y su archivo .pfx tendrá una contraseña de su elección. También tiene opción de hello del uso de un certificado emitido por una entidad de certificación.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>¿Cómo tooenable acceso remoto después de haya implementado tooAzure
tooenable acceso remoto después de haber implementado tooAzure, Hola uso pasos:

1. Inicie sesión en el portal de administración de Azure de hello con su cuenta de Azure

2. En la lista de **Servicios en la nube**, seleccione el servicio en la nube que se implementó

3. En la página web del servicio en la nube hello, haga clic en hello **configurar** vínculo

4. En hello parte inferior de la página de configuración de hello, haga clic en hello **remoto** vínculo

5. Cuando aparezca el cuadro de diálogo emergente de hello:
   
   * Especificar Hola rol, que se desea acceso remoto tooenable

   * Haga clic en hello tooselect **habilitar Escritorio remoto** casilla de verificación
   
   * Especifique un nombre de usuario y una contraseña que desee toouse para acceso remoto
   
   * Seleccione Hola certificado toouse

6. Haga clic en **Aceptar** 

Verá un mensaje que indica que el cambio de configuración está en curso, lo que puede tardar unos toocomplete minutos. Cuando haya finalizado el cambio de configuración de hello, siga los pasos de Hola Hola **toolog de forma remota** sección más adelante en este artículo.

## <a name="how-tooenable-remote-access-in-your-package"></a>El proceso tooenable de acceso remoto en el paquete
1. En el panel del explorador de proyectos de Eclipse, haga clic con el botón derecho en el proyecto y haga clic en **Properties**(Propiedades).

2. Hola **propiedades** cuadro de diálogo, expanda **Azure** en el panel izquierdo de Hola y haga clic en **acceso remoto**.

3. Hola **acceso remoto** cuadro de diálogo, asegúrese de **habilitar todos los roles tooaccept conexiones a Escritorio remoto con estas credenciales de inicio de sesión** está activada.

4. Especifique un nombre de usuario para hello conexión a Escritorio remoto.

5. Especifique y confirme la contraseña de hello para el usuario de Hola. valores de nombre y la contraseña de la usuario de Hello establecidos en este cuadro de diálogo se utilizará al realizar una conexión a Escritorio remoto. (Tenga en cuenta que se trata de una contraseña independiente de su contraseña PFX).

6. Especifique la fecha de expiración de hello para la cuenta de usuario de Hola.

7. Haga clic en **New** toocreate un nuevo certificado autofirmado. (Como alternativa, puede seleccionar un certificado desde el área de trabajo o sistema de archivos a través de hello **área de trabajo** o **FileSystem** botones, respectivamente, pero para los fines de este tutorial vamos a crear un nuevo certificado.)

   * Hola **nuevo certificado** cuadro de diálogo, especifique y confirme la contraseña de Hola que usará para el archivo PFX.

   * Acepte el valor Hola proporcionado para **nombre (CN)**, o usar un nombre personalizado.

   * Especifique Hola ruta de acceso y nombre de archivo donde se guardará el nuevo certificado de hello, en formato .cer. En este paso y el paso siguiente de hello, podría utilizar hello **cert** carpeta de su proyecto de Azure, pero está libre toochoose otra ubicación. Para los fines de este tutorial, usaremos **c:\mycert\mycert.cer**. (Crear hello **c:\mycert** tooproceeding anteriores de carpeta, o utilice una carpeta existente si lo desea.)

   * Especifique Hola ruta de acceso y nombre de archivo donde se guardará un nuevo certificado hello y su clave privada, en formato .pfx. Para los fines de este tutorial, usaremos **c:\mycert\mycert.pfx**. Su **nuevo certificado** diálogo debe tener un aspecto similar siguiente toohello (actualizar las rutas de acceso de carpeta de hello si no usó **c:\mycert**):
     
      ![][ic712275]

   * Haga clic en **Aceptar** tooclose hello **nuevo certificado** cuadro de diálogo.

8. Su **acceso remoto** cuadro de diálogo debe tener un aspecto similar siguiente toohello:</p>
   
   ![][ic719495]

9. Haga clic en **Aceptar** tooclose hello **acceso remoto** cuadro de diálogo.

Recompilar la aplicación, con hello generar el conjunto de toocloud de implementación.

## <a name="toolog-in-remotely"></a>toolog de forma remota
Una vez que la instancia de rol está lista, puede registrar de forma remota en la máquina virtual de toohello que hospeda la aplicación.

* Si está usando Eclipse en Windows y Hola seleccionado se **iniciar escritorio remoto en implementar** opción durante la tooAzure de implementación, aparecerá una pantalla de inicio de sesión de conexión a Escritorio remoto cuando se inicia la implementación. Cuando se le pida Hola nombre de usuario y contraseña, escriba los valores de hello que especificó para el usuario remoto hello y será capaz de toolog en.

* Toolog de otra manera de forma remota es a través de hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de administración de Azure</a>:
  
  * Dentro de hello **servicios en la nube** vista de hello portal de administración de Azure, haga clic en el servicio de nube, haga clic en **instancias**, haga clic en una instancia específica y, a continuación, haga clic en hello **conectar**botón. Hola **conectar** botón se muestra como siguiente de hello en la barra de comandos de hello:
    
      ![][ic659273]

  * Tras hacer clic en hello **conectar** botón, podrá tooopen solicitada un archivo RDP. Abra el archivo hello y siga las indicaciones de Hola. (Podría guardar este equipo local tooyour de archivo y, a continuación, ejecutar archivo hello haciendo doble clic en él tooremote registro en tooyour máquina virtual sin necesidad de toofirst vaya portal de administración de Hola.)

  * Cuando se le pida Hola nombre de usuario y contraseña, escriba los valores de hello que especificó para el usuario remoto hello y será capaz de toolog en.

> [!NOTE]
> Si se encuentra en un sistema operativo, es necesario toouse un cliente de escritorio remoto que sea compatible con el sistema operativo y siga Hola pasos tooconfigure que el cliente con la configuración de hello en el archivo RDP de Hola que ha descargado.
> 
> 

## <a name="see-also"></a>Otras referencias
[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]

[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
