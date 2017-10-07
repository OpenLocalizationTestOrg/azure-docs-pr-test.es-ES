---
title: aaaPublish un contenedor de Docker mediante el uso de hello Azure Toolkit for Eclipse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toopublish una tooMicrosoft de aplicación web Azure como un contenedor de Docker mediante el uso de hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publicar una aplicación web como un contenedor de Docker mediante Hola Kit de herramientas de Azure para Eclipse

Los contenedores de Docker son un método muy utilizado para implementar aplicaciones web. Mediante el uso de contenedores de Docker, los desarrolladores pueden consolidar todos sus archivos de proyecto y las dependencias en un único paquete para el servidor de implementación tooa. Hello Azure Toolkit for Eclipse simplifica este proceso para los desarrolladores de Java agregando *publicar como contenedor de Docker* características de implementación tooMicrosoft Azure. Este artículo le guiará a través de hello pasos necesarios toopublish su tooAzure de aplicaciones como contenedores de Docker.

> [!NOTE]
> Para obtener más información sobre Docker está disponible en hello [sitio Web de Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker

1. Abra el proyecto de aplicación web en Eclipse.

2. Hola toostart **publicar como contenedor de Docker** asistente, realice una de las siguientes de hello:

   * Hola **navegador** ver, haga clic en el proyecto, haga clic en **Azure**y, a continuación, haga clic en **publicar como contenedor de Docker**.

      ![Vista de navegador del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB01]

   * En la barra de herramientas de Eclipse hello, haga clic en hello **publicar** botón y, a continuación, haga clic en **publicar como contenedor de Docker**.

      ![Barra de herramientas de Eclipse del comando Publish as Docker Container (Publicar como contenedor de Docker)][PUB02]
      
    Hola **implementar contenedor de Docker en Azure** abre el asistente.

    ![Hola implementar contenedor de Docker en el Asistente de Azure][PUB03]

3. Hola **escriba un nombre de imagen, seleccione la ruta de acceso del artefacto de Hola y comprobar una toobe de host de Docker usan** ventana, Hola siguientes:

    a. Hola **nombre de la imagen de Docker** cuadro, escriba un nombre único para el host Docker. (Asistente de hello crea automáticamente un nombre, pero se puede modificar.)

    b. Hola **Hosts** área muestra todos los hosts de Docker que ya haya creado. Realice una de las siguientes de hello:

    * Si tiene un host Docker existente, puede implementar su tooit de aplicación web.
    * Haga clic en un nuevo host Docker, toocreate **agregar**.  
      
    Hola **crear un Host Docker** abre el cuadro de diálogo.

    ![Asistente Deploy Docker Container on Azure (Implementar contenedor de Docker en Azure)][PUB04a]

4. Hola **configurar la máquina virtual nueva de hello** ventana, especifique Hola siguientes opciones para el host de Docker. (Asistente de hello genera automáticamente la mayoría de las opciones de Hola para usted, pero puede modificar cualquiera de ellos).

   a. **Nombre**: escriba un nombre único para el host de Docker Hola. (Es no Hola igual Hola nombre de la imagen de Docker que especificó anteriormente).

   b. **Suscripción**: escriba Hola suscripción de Azure que usa para el host.

   c. **Región**: ENTRAR Hola región geográfica donde se encuentra el host.

   d. En hello **SO Host y el tamaño** ficha:
     * **Sistema operativo de host**: escriba el sistema operativo de hello para la máquina virtual de Hola que contiene el host.
     * **Tamaño**: especifique el tamaño de la máquina virtual de hello para el host.

   e. En hello **grupo de recursos** ficha:
     * **New resource group** (Nuevo grupo de recursos): cree un grupo de recursos para el host.
     * **Existing resource group** (Grupo de recursos existente): especifique un grupo de recursos existente desde su cuenta de Azure.

   f. En hello **red** ficha:
     * **New virtual network** (Nueva red virtual): cree una red virtual para el host.
     * **Existing virtual network** (Red virtual existente): especifique una red virtual existente desde su cuenta de Azure.

   g. En hello **almacenamiento** ficha:
     * **New storage account** (Nueva cuenta de almacenamiento): cree una cuenta de almacenamiento para el host.
     * **Existing storage account** (Cuenta de almacenamiento existente): especifique una cuenta de almacenamiento existente desde su cuenta de Azure.

5. Haga clic en **Siguiente**.

6. Hola **configurar registro en las credenciales y configuración de puerto** ventana, seleccione una de las siguientes opciones de hello:

    * **Import credentials from Azure Key Vault** (Importar credenciales de Azure Key Vault): especifique un conjunto de credenciales previamente guardadas que están almacenadas en la suscripción de Azure.

      >[!NOTE]
      >Un almacén de claves de Azure que se crea con una cuenta específica o una entidad de servicio no es automáticamente accesible por otra cuenta o entidad de servicio que comparte suscripción Hola. tooallow toouse de entidad de seguridad otra cuenta o servicio Hola el almacén de claves, debe utilizar cuenta de Azure tooadd portal Hola Hola o entidad de servicio.

    * **New log in credentials** (Nuevas credenciales de inicio de sesión): crea un conjunto de credenciales de inicio de sesión. Si selecciona esta opción, Hola siguientes:
    
      * En hello **las credenciales de la máquina virtual** ficha, elija una de hello siguientes opciones para las credenciales de inicio de sesión de máquina virtual de hello del host Docker:

          * **Nombre de usuario**: escriba el nombre de usuario de hello las credenciales de inicio de sesión de máquina virtual.
          * **Contraseña** y **confirmar**: escriba la contraseña de hello las credenciales de inicio de sesión de máquina virtual.
          * **SSH**: especifique la configuración de Shell seguro (SSH) de hello para el host de Docker. Puede elegir entre Hola siguientes opciones:
            * **None** (Ninguna): especifica que la máquina virtual no permitirá conexiones SSH.
            * **Generar automáticamente**: automáticamente crea Hola la configuración necesaria para conectarse a través de SSH.
            * **Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de SSH previamente guardadas. directorio de Hello debe contener Hola después de dos archivos:
                * *id_rsa*: contiene la identificación de RSA de Hola para un usuario.
                * *id_rsa.pub*: contiene la clave pública de hello RSA que se utiliza para la autenticación.
        
        ![Create Docker Host (Crear host de Docker)][PUB05]

      * En hello **Docker Daemon credenciales** ficha, especifique Hola siguientes opciones:

          * **Puerto de demonio de docker**: escriba el puerto TCP único hello para el host Docker.
          * **Seguridad de TLS**: especifique la configuración de seguridad de la capa de transporte de Hola de su host de Docker. Puede elegir entre Hola siguientes opciones:
            * **None** (Ninguna): especifica que su máquina virtual no permitirá conexiones TLS.
            * **Generar automáticamente**: automáticamente crea Hola la configuración necesaria para conectarse a través de TLS.
            * **Import from directory** (Importar desde directorio): especifica un directorio que contiene un conjunto de configuraciones de TLS previamente guardadas. Más concretamente, el directorio de hello debe contener Hola siguientes seis archivos:
                * *CA.PEM* y *key.pem ca*: contienen el certificado de hello y una clave pública para hello entidad emisora de certificados de TLS.
                * *CERT.PEM* y *key.pem*: contienen el certificado de cliente de hello y una clave pública que se utiliza para la autenticación TLS.
                * *Server.PEM* y *key.pem server*: contienen el certificado de servidor de Hola y de clave pública para el host de Hola.

        ![Create Docker Host (Crear host de Docker)][PUB06]

7. Después de haber escrito todos Hola información anterior, haga clic en **finalizar**.

8. Hola **implementar contenedor de Docker en Azure** asistente, haga clic en **siguiente**.

   ![Hola implementar contenedor de Docker en el Asistente de Azure][PUB07]

9. Hola **configurar hello Docker contenedor toobe crea** ventana, Hola siguientes:

   a. Hola **nombre del contenedor de Docker** cuadro, escriba un nombre único para el contenedor de Docker.

   b. Elija uno de hello después de imágenes de Docker:
     * **Predefined Docker image** (Imagen de Docker predefinida): especifica una imagen de Docker preexistente de Azure.

       >[!NOTE]
       >Hola lista de imágenes de Docker en este cuadro está formada por varias imágenes que hello Azure Toolkit ha sido configurado toopatch para que el artefacto se implementa automáticamente.

     * **Custom Dockerfile** (Dockerfile personalizado): especifica un Dockerfile guardado antes desde el equipo local.

       >[!NOTE]
       >Se trata de una característica más avanzada para los desarrolladores que deseen toodeploy su propios Dockerfile. Sin embargo, resulta una toodevelopers que usan este tooensure opción que sus Dockerfile se ha creado correctamente. Hola Kit de herramientas de Azure no validar el contenido de hello en un archivo Dockerfile personalizado, por lo que puede producir un error en la implementación de Hola si hello Dockerfile tiene problemas. Además, hello Azure Toolkit espera Hola personalizado Dockerfile toocontain un artefacto de la aplicación web y tratará de tooopen una conexión HTTP. Si los desarrolladores publican un tipo diferente de artefacto, podrían recibir errores inofensivos después de la implementación.

   c. **Configuración de puertos**: especifique el enlace de puerto TCP único de hello para el contenedor de Docker.

     ![ventana de Hello configurar hello Docker contenedor toobe creado][PUB08]

10. Después de haber completado todos los pasos anteriores de Hola, haga clic en **finalizar**.

Hello Azure Toolkit comienza implementar su tooAzure de aplicación web en un contenedor de Docker. 

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

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].

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

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png