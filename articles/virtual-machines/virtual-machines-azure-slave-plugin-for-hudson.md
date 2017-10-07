---
title: "aaaHow toouse hello Azure esclavo complemento con integración continua Hudson | Documentos de Microsoft"
description: "Describe cómo toouse hello Azure subordinado complemento con integración continua Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>¿Cómo toouse hello Azure subordinado complemento con integración continua Hudson
Hello Azure esclavo complemento para Hudson permite nodos de tooprovision esclavo en Azure cuando ejecuta distribuida compila.

## <a name="install-hello-azure-slave-plug-in"></a>Instalar hello Azure esclavo complemento
1. En el panel de Hudson hello, haga clic en **administrar Hudson**.
2. Hola **administrar Hudson** página, haga clic en **administrar complementos**.
3. Haga clic en hello **disponible** ficha.
4. Haga clic en **búsqueda** y tipo **Azure** toolimit Hola lista toorelevant complementos.
   
    Si decide tooscroll a través de la lista de Hola de complementos disponibles, encontrará hello Azure esclavo complemento en hello **administración del clúster y distribuidas compilar** sección Hola **otros** ficha.
5. Casilla de Hola de **Azure esclavo complemento**.
6. Haga clic en **Instalar**.
7. Reinicie Hudson.

Ahora se instala dicho complemento hello, pasos de Hola sería tooconfigure Hola complemento con el perfil de suscripción de Azure y toocreate una plantilla que se utilizará en la creación de hello VM para el nodo de esclavo Hola.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Configurar hello Azure esclavo complemento con el perfil de suscripción
Un perfil de suscripción, también denominados tooas configuración de publicación, es un archivo XML que contiene credenciales seguras e información adicional que necesitará toowork con Azure en el entorno de desarrollo. Hola tooconfigure Azure esclavo complemento, debe:

* Su id. de suscripción
* Un certificado de administración para la suscripción

Estos se pueden encontrar en su [perfil de suscripción]. A continuación se muestra un ejemplo de un perfil de suscripción.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Una vez que tenga su perfil de suscripción, siga estos Hola de tooconfigure pasos Azure esclavo de complemento.

1. En el panel de Hudson hello, haga clic en **administrar Hudson**.
2. Haga clic en **Configure System**(Configurar sistema).
3. Desplácese hacia abajo Hola de hello página toofind **nube** sección.
4. Haga clic en **Add new cloud > Microsoft Azure** (Agregar nueva nube > Microsoft Azure).
   
    ![agregar nube nueva][add new cloud]
   
    Esto mostrará los campos de hello en las que necesite tooenter los detalles de la suscripción.
   
    ![configurar perfil][configure profile]
5. Copie el certificado de administración y el Id. de suscripción Hola de su perfil de suscripción y péguelos en los campos correspondientes de Hola.
   
    Cuando se copian el certificado de administración y el Id. de suscripción hello, **no** incluidas Hola comillas que delimitan los valores de hello.
6. Haga clic en **Verify configuration**(Comprobar configuración).
7. Cuando se comprobó correctamente la configuración de hello, haga clic en **guardar**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Configurar una plantilla de máquina virtual para hello Azure esclavo complemento
Una plantilla de máquina virtual define parámetros Hola Hola complemento utilizará toocreate un nodo subordinado en Azure. Hola pasos se podrá crear plantilla para una VM Ubuntu.

1. En el panel de Hudson hello, haga clic en **administrar Hudson**.
2. Haga clic en **Configure System**(Configurar sistema).
3. Desplácese hacia abajo Hola de hello página toofind **nube** sección.
4. Dentro de hello **nube** sección, busque **Agregar plantilla de máquina Virtual de Azure** y haga clic en hello **agregar** botón.
   
    ![agregar plantilla de vm][add vm template]
5. Especifique un nombre de servicio de nube en hello **nombre** campo. Si se especifica el nombre de Hola hace referencia tooan existente de servicio en la nube, se aprovisionará Hola VM en ese servicio. De lo contrario, Azure creará uno nuevo.
6. Hola **descripción** , a continuación, escriba el texto que describe la plantilla de Hola que está creando. Esta información es solo para fines documentales y no se usa en el aprovisionamiento de una máquina virtual.
7. Hola **etiquetas** , escriba **linux**. Esta etiqueta es tooidentify usado Hola plantilla que está creando y es la plantilla de Hola de tooreference posteriormente usado cuando se crea un trabajo Hudson.
8. Seleccione una región donde se creará Hola máquina virtual.
9. Seleccione el tamaño de VM apropiado de Hola.
10. Especifique una cuenta de almacenamiento donde se creará Hola máquina virtual. Asegúrese de que se encuentra en hello misma región que el servicio de nube de Hola que vamos a usar. Si desea que el nuevo toobe de almacenamiento creado, puede dejar este campo en blanco.
11. Tiempo de retención especifica Hola minutos antes de Hudson elimina a un esclavo inactivo. Dejarlo en el valor predeterminado de Hola de 60.
12. En **uso**, seleccione Hola condición adecuada cuando se usará este nodo subordinado. Por ahora, seleccione **Utilize this node as much as possible**(Usar este nodo tanto como sea posible).
    
     En este momento, el formulario sería toothis similar:
    
     ![configuración de plantilla][template config]
13. En **familia de imagen o identificador** tiene toospecify qué imagen de sistema se instalará en la máquina virtual. Puede seleccionar de una lista de familias de imagen o especificar una imagen personalizada.
    
     Si desea tooselect en una lista de familias de imagen, escriba Hola primer carácter (distingue mayúsculas de minúsculas) del nombre de familia de imagen de Hola. Por ejemplo, al escribir **U** aparecerá una lista de familias de Ubuntu Server. Una vez que selecciona en la lista de Hola, Jenkins usará versión más reciente de Hola de esa imagen de sistema de esa familia al aprovisionar la máquina virtual.
    
     ![lista de familias de SO][OS family list]
    
     Si tiene una imagen personalizada que desee toouse en su lugar, escriba el nombre de Hola de esa imagen personalizada. Nombres de imagen personalizada no se muestran en una lista por lo que tendrá tooensure que Hola nombre está escrito correctamente.    
    
     Para este tutorial, escriba **U** toobring una lista de imágenes de Ubuntu y seleccione **Ubuntu Server 14.04 LTS**.
14. Para **Launch method** (Método de inicio), seleccione **SSH**.
15. Copie el siguiente script de Hola y pegue en hello **Init script** campo.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Hola **Init script** se ejecutará después de Hola se crea la máquina virtual. En este ejemplo, el script de Hola instala ant, Java y git.
16. Hola **nombre de usuario** y **contraseña** campos, escriba los valores preferidos para cuenta de administrador de Hola que se creará en la máquina virtual.
17. Haga clic en **comprobar plantilla** toocheck si los parámetros de hello especificados son válidos.
18. Haga clic en **Save**(Guardar).

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Creación de un trabajo de Hudson que se ejecuta en un nodo subordinado en Azure
En esta sección, creará una tarea de Hudson que se ejecutará en un nodo subordinado en Azure.

1. En el panel de Hudson hello, haga clic en **nuevo trabajo**.
2. Escriba un nombre para el trabajo de Hola que se va a crear.
3. Para el tipo de trabajo de hello, seleccione **crear un trabajo de estilo libre software**.
4. Haga clic en **Aceptar**.
5. En la página de configuración del trabajo de hello, seleccione **restringir donde se puede ejecutar este proyecto**.
6. Seleccione **menú de nodo y la etiqueta** y seleccione **linux** (se especifica esta etiqueta cuando se crea la plantilla de máquina virtual de hello en la sección anterior de hello).
7. Hola **generar** sección, haga clic en **agregar el paso de compilación** y seleccione **ejecutar shell**.
8. Editar Hola siguiente secuencia de comandos, reemplazando **{su nombre de cuenta de github}**, **{el nombre del proyecto}**, y **{el directorio del proyecto}** con los valores adecuados y pegue Hola Editar script Hola área de texto que aparece.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Haga clic en **Save**(Guardar).
10. En Hola panel Hudson, busque el trabajo de Hola que acaba de crear y haga clic en hello **programar una compilación** icono.

Hudson después creará un nodo subordinado con plantilla Hola creado en la sección anterior de Hola y ejecutar script de Hola que especificó en el paso de compilación de Hola para esta tarea.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].

<!-- URL List -->

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[perfil de suscripción]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

