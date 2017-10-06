---
title: aaaPublish un contenedor de Docker mediante el uso de hello Azure Toolkit para IntelliJ | Documentos de Microsoft
description: "Obtenga información acerca de cómo toopublish una tooMicrosoft de aplicación web Azure como un contenedor de Docker mediante el uso de Hola Kit de herramientas de Azure para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publicar una aplicación web como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ

Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web. Mediante el uso de contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y las dependencias en un único paquete para el servidor de implementación tooa. Hello Azure Toolkit for IntelliJ simplifica este proceso para los desarrolladores de Java agregando *publicar como contenedor de Docker* características de implementación tooMicrosoft Azure. Este artículo le guiará a través de hello pasos necesarios toopublish su tooAzure de aplicaciones como contenedores de Docker.

> [!NOTE]
>
> Para obtener más información sobre Docker está disponible en hello [sitio Web de Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker

> [!NOTE]
> * toopublish la aplicación web, debe crear un artefacto preparada para la implementación. toolearn más información, vea hello [información adicional acerca de cómo crear artefactos](#artifacts) sección.
>
> * Después de haber completado al Asistente para implementación de hello al menos una vez, la mayor parte de la configuración se utiliza como predeterminada cuando vuelva a ejecutar el Asistente de Hola.
>

1. Abra el proyecto de aplicación web en IntelliJ.

2. Hola toostart **publicar como contenedor de Docker** asistente, realice una de las siguientes de hello:

   * Hola **proyecto** ventana de herramientas, haga clic en el proyecto, haga clic en **Azure**y, a continuación, haga clic en **publicar como contenedor de Docker**:

      ![Hola publicar como comando de contenedor de Docker][PUB01]

   * En la barra de herramientas de hello IntelliJ, haga clic en hello **grupo publicación** botón y, a continuación, haga clic en **publicar como contenedor de Docker**:

      ![Hola publicar como comando de contenedor de Docker][PUB02]  
    Hola **implementar contenedor de Docker en Azure** abre el asistente.

   ![Hola implementar contenedor de Docker en el Asistente de Azure][PUB03]

3. Hola **escriba un nombre de imagen, seleccione la ruta de acceso del artefacto de Hola y comprobar una toobe de host de Docker usan** ventana, Hola siguientes: 

   a. Hola **nombre de la imagen de Docker** cuadro, escriba un nombre único para el host Docker. (Asistente de hello crea automáticamente un nombre, pero se puede modificar.) 

   b. Hola **Hosts** área muestra todos los hosts de Docker que ya haya creado. Realice una de las siguientes de hello: 
      * Si tiene un host Docker existente, puede implementar su tooit de aplicación web.
      * toocreate un host Docker, haga clic en verde hello más el signo (**+**).  
       Hola **crear un Host Docker** abre el cuadro de diálogo. 

      ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. Hola **configurar la máquina virtual nueva de hello** ventana, proporcionar Hola después de obtener información sobre el host Docker. (Asistente de hello genera automáticamente la mayoría de hello información automáticamente, pero puede modificar cualquiera de ellos). 

   a. Hola **nombre** cuadro, escriba un nombre único para el host de Docker Hola. (Es no Hola igual Hola nombre de la imagen de Docker que especificó anteriormente). 
    
   b. Hola **suscripción** cuadro, escriba Hola suscripción de Azure que usa para el host. 
      
   c. Hola **región** cuadro, escriba Hola región geográfica donde se encuentra el host.
      
   d. En hello **OS y tamaño** ficha, Hola siguientes:      
      * **Sistema operativo de host**: escriba el sistema operativo de hello para la máquina virtual de Hola que contiene el host. 
      * **Tamaño**: especifique el tamaño de la máquina virtual de hello para el host.   
       
   e. En hello **grupo de recursos** ficha, seleccione cualquiera de hello siguientes:      
      * **New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.
      * **Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure. 
       
   f. En hello **red** ficha, seleccione cualquiera de hello siguientes:      
      * **New virtual network** (Nueva red virtual): cree una red virtual para el host.
      * **Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure. 
       
   g. En hello **almacenamiento** ficha, seleccione cualquiera de hello siguientes:      
      * **New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.
      * **Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.
       
5. Haga clic en **Siguiente**.  
     Hola **configurar registro en las credenciales y configuración de puerto** se abre la ventana.

      ![registro de Hello configurar en las credenciales y la ventana de configuración de puerto][PUB05]

6. Seleccione una de las siguientes opciones de hello:

      * **Import credentials from Azure Key Vault**  (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.

          > [!NOTE]
          > Un almacén de claves de Azure que se crea con una cuenta específica o una entidad de servicio no es automáticamente accesible por otra cuenta o entidad de servicio que comparte suscripción Hola. tooallow otra clave de hello toouse principal cuenta o servicio de almacén, debe usar la cuenta de Azure tooadd portal Hola Hola o entidad de servicio.

      * **New log in credentials** (Nuevas credenciales de inicio de sesión): cree un conjunto de credenciales de inicio de sesión. Si selecciona esta opción, Hola siguientes:

        a. En hello **las credenciales de la máquina virtual** ficha, proporcione Hola siguiendo la información de credenciales de inicio de sesión de máquina virtual de hello del host Docker: * **nombre de usuario**: escriba el nombre de usuario de hello para el inicio de sesión de máquina virtual credenciales.
             * **Contraseña** y **confirmar**: escriba la contraseña de hello las credenciales de inicio de sesión de máquina virtual.
             * **SSH**: especifique la configuración de Shell seguro (SSH) de hello para el host de Docker. Puede seleccionar una de las siguientes opciones de hello: * **ninguno**: Especifica que la máquina virtual no se permiten las conexiones SSH.
                * **Generar automáticamente**: automáticamente crea Hola la configuración necesaria para conectarse a través de SSH.
                * **Importar desde el directorio**: permite toospecify un directorio que contiene un conjunto de configuración de SSH guardada anteriormente. directorio de Hello debe contener Hola después de dos archivos:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. En hello **Docker Daemon acceso** ficha, proporcione Hola siguiente información:

          ![Create Docker Host (Crear host de Docker)][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Después de escribir información de hello necesario, haga clic en **finalizar**.  
    Hola **implementar contenedor de Docker en Azure** Asistente vuelve a aparecer.

   ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB07]

8. Haga clic en **Siguiente**.  
    Hola **configurar hello Docker contenedor toobe crea** abre la ventana.

   ![ventana de Hello configurar hello Docker contenedor toobe creado][PUB08]

9. Hola **configurar hello Docker contenedor toobe crea** ventana, proporcionar Hola siguiente información: 

   a. Hola **nombre del contenedor de Docker** cuadro, escriba un nombre único para el contenedor de Docker.

   b. Elija uno de hello después de imágenes de Docker: 

      * **Predefined Docker image** (Imagen de Docker predefinida): especifique una imagen de Docker preexistente de Azure. 

        > [!NOTE]
        > Hola lista de imágenes de Docker en este cuadro está formada por varias imágenes que hello Azure Toolkit ha sido configurado toopatch para que el artefacto se implementa automáticamente. 

      * **Custom Dockerfile** (Dockerfile personalizado): especifique un Dockerfile guardado antes desde el equipo local.

        > [!NOTE]
        > Se trata de una característica más avanzada para los desarrolladores que deseen toodeploy su propios Dockerfile. Sin embargo, resulta una toodevelopers que usan este tooensure opción que sus Dockerfile se ha creado correctamente. Porque hello Azure Toolkit validan el contenido de hello en un archivo Dockerfile personalizado, implementación de hello podría producir errores si hello Dockerfile tiene problemas. Además, dado que hello Azure Toolkit espera Hola personalizado Dockerfile toocontain un artefacto de la aplicación web, intenta tooopen una conexión HTTP. Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.

   c. Hola **configuración de puertos** cuadro, escriba Hola único puerto el enlace TCP para el contenedor de Docker. 

10. Después de haber completado los pasos anteriores de hello, haga clic en **finalizar**. 

Hello Azure Toolkit comienza implementar su tooAzure de aplicación web en un contenedor de Docker. A menos que haya configurado toobe IntelliJ implementado en segundo plano de hello, un **implementar tooAzure** aparece la barra de progreso. 

![barra de progreso de implementación de Hola][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Información adicional sobre la creación de artefactos

toocreate un artefacto preparada para la implementación, Hola siguientes:

1. Abra el proyecto de aplicación web en IntelliJ.

2. Haga clic en **Archivo** y después en **Estructura del proyecto**.

   ![Hola comandos de la estructura del proyecto][ART01]

3. tooadd un artefacto, haga clic en verde hello más el signo (**+**) y, a continuación, haga clic en **aplicación Web: archivo**.

   ![Hola comando "Archivo de: aplicación Web"][ART02]

4. Hola **nombre** cuadro, escriba un nombre para el artefacto (no incluya hello *.war* extensión) y, a continuación, haga clic en **Aceptar**.

   ![cuadro de nombre de artefacto de Hola][ART03]

Para obtener más información sobre cómo crear artefactos en IntelliJ, consulte [configurar artefactos] en el sitio Web de JetBrains Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:

* [Kit de herramientas de Azure para Eclipse]
  * [Novedades de hello Azure Toolkit for Eclipse]
  * [Instalar hello Azure Toolkit for Eclipse]
  * [Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Novedades de hello Azure Toolkit for IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * [Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

Para obtener recursos adicionales de Docker, consulte oficial de hello [sitio Web de Docker].

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[sitio Web de Docker]: https://www.docker.com/
[configurar artefactos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuración de artefactos)

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
