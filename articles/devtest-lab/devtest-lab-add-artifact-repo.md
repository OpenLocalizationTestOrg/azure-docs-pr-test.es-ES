---
title: aaaAdd un laboratorio de tooa del repositorio de Git en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Adición de un repositorio Git de GitHub o Visual Studio Team Services para el origen de artefactos personalizados en Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Agregar un artefactos de Git repositorio toostore personalizados y plantillas del Administrador de recursos de Azure

Si desea demasiado[crear artefactos personalizados](devtest-lab-artifact-author.md) para hello las máquinas virtuales en el laboratorio, o [usar plantillas de Azure Resource Manager toocreate un entorno de prueba personalizada](devtest-lab-create-environment-from-arm.md), también debe agregar una privada tooinclude repositorio de Git artefactos de Hola o plantillas del Administrador de recursos de Azure que crea el equipo. repositorio de Hola se puede hospedar en [GitHub](https://github.com) o en [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Hemos preparado un [repositorio de Github de artefactos](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) que puede implementar como está o personalizarlo para sus laboratorios. Al personalizar o crear un artefacto, no puede almacenar en el repositorio público de hello: debe crear su propio repositorio privado. 

Cuando se crea una máquina virtual, puede guardar la plantilla de Azure Resource Manager hello, personalizarla si desee y, a continuación, utilizarlo más adelante tooeasily crear más máquinas virtuales. Debe crear su propio repositorio privado toostore sus plantillas personalizadas de Azure Resource Manager.  

* toolearn toocreate un repositorio de GitHub, vea [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toolearn toocreate un proyecto de Team Services con un repositorio Git, vea [conectar tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Hello captura de pantalla siguiente muestra un ejemplo de cómo podría quedar un repositorio que contienen artefactos en GitHub:  
![Repositorio de artefactos de GitHub de ejemplo](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Obtener las credenciales y la información del repositorio Hola
tooadd un laboratorio de tooyour repositorio, primero debe obtener cierta información desde el repositorio. Hola las secciones siguientes le guiarán por obtener esta información para repositorios alojado en GitHub y Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Obtener el token de dirección URL de clonación del repositorio de GitHub de Hola y de acceso personal
URL de clonación del repositorio de GitHub de tooget Hola y el token de acceso personal, siga estos pasos:

1. Explorar la página de inicio de toohello del repositorio de GitHub de Hola que contiene el artefacto de Hola o definiciones de plantilla de Azure Resource Manager.
2. Seleccione **Clone or download**(Clonar o descargar).
3. Hola de hello seleccione botón toocopy **url de clonación de HTTPS** toohello Portapapeles y guarde la dirección URL de Hola para su uso posterior.
4. Seleccione la imagen de perfil de hello en la esquina superior derecha de Hola de GitHub y seleccione **configuración**.
5. Hola **configuración Personal** menú Hola hacia la izquierda, seleccione **tokens de acceso Personal**.
6. Seleccione **Generar nuevo token**.
7. En hello **nuevo token de acceso personal** página, escriba un **símbolo (token) descripción**, aceptar elementos predeterminados de Hola Hola **seleccione ámbitos**y, a continuación, elija **generar Símbolo (token)**.
8. Guardar el token de hello generado según sea necesario más adelante.
9. Ahora puede cerrar GitHub.   
10. Continuar toohello [conectar el repositorio de toohello lab](#connect-your-lab-to-the-repository) sección.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Obtener el token de acceso personal y dirección URL de clonación de repositorio de hello Visual Studio Team Services
dirección URL de clonación de repositorio de Visual Studio Team Services del hello tooget y token de acceso personal, siga estos pasos:

1. Página principal de hello abiertos de la colección de equipo (por ejemplo, `https://contoso-web-team.visualstudio.com`) y, a continuación, seleccione el proyecto.
2. En la página de inicio del proyecto de hello, seleccione **código**.
3. dirección URL de clonación del Hola de tooview, en el proyecto de hello **código** página, seleccione **clon**.
4. Guardar la dirección URL de hello según sea necesario más adelante en este tutorial.
5. Seleccione un Token de acceso Personal, toocreate **mi perfil** desde el menú de lista desplegable de cuenta de usuario de Hola.
6. En la página de información de perfil de hello, seleccione **seguridad**.
7. En hello **seguridad** ficha, seleccione **agregar**.
8. Hola **crear un token de acceso personal** página:

   * Escriba un **descripción** de token de Hola.
   * Seleccione **180 días** de hello **expira en** lista.
   * Elija **todas las cuentas de acceso** de hello **cuentas** lista.
   * Elija hello **todos los ámbitos** opción.
   * Elija **Crear token**.
9. Cuando termine, aparece nuevo token de Hola Hola **Tokens de acceso Personal** lista. Seleccione **copiar Token**y, a continuación, guarde el valor del token de Hola para su uso posterior.
10. Continuar toohello [conectar el repositorio de toohello lab](#connect-your-lab-to-the-repository) sección.

## <a name="connect-your-lab-toohello-repository"></a>Conectar el repositorio de toohello de laboratorio
1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.   
4. En el panel izquierdo de hello, seleccione **directivas y configuración**.
5. En el laboratorio de hello **directivas y configuración** área, seleccione **repositorios**.
6. En hello **repositorios** área, seleccione **+ agregar**.

    ![Adición del botón de repositorio](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. En hello segundo **repositorios** página, especifique Hola siguiente información:

   * **Nombre de** -escriba un nombre para el repositorio de Hola.
   * **Dirección Url de clonación de GIT** -escriba Hola Git clone dirección URL HTTPS que copió anteriormente desde GitHub o Visual Studio Team Services.
   * **Rama** -escriba Hola bifurcación tooget sus definiciones.
   * **Token de acceso personal** -escriba el token de acceso personal Hola obtenido anteriormente de GitHub o Visual Studio Team Services.
   * **Las rutas de acceso de carpeta** -escriba al menos una carpeta ruta de acceso relativa toohello dirección URL de clonación que contiene el artefacto o definiciones de plantilla de Azure Resource Manager. Cuando se especifica un subdirectorio, asegúrese de seguro tooinclude Hola barra diagonal en la ruta de acceso de carpeta Hola.

     ![Área Repositorios](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Seleccione **Guardar**.

## <a name="next-steps"></a>Pasos siguientes
Después de haber creado el repositorio Git privado, podrá realizar una o dos procedimientos siguientes de hello, dependiendo de sus necesidades:
* Almacén de la [artefactos personalizados](devtest-lab-artifact-author.md), que puede usar más adelante toocreate nuevas máquinas virtuales.
* [Crear entornos de varias VM y recursos de PaaS con plantillas de Azure Resource Manager](devtest-lab-create-environment-from-arm.md) y, a continuación, almacenar plantillas de hello en el repositorio privado.

Cuando se crea una máquina virtual, puede comprobar que se agregan los artefactos de Hola o plantillas tooyour repositorio de Git. Están disponibles inmediatamente en la lista de Hola de artefactos o plantillas, con el nombre de Hola de repositorio privado que se muestra en la columna de Hola que especifica el origen de Hola. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Entradas blogs relacionadas
* [¿Cómo tootroubleshoot errores artefactos en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-troubleshoot-artifact-failure.md)
* [Unirse a un dominio de Active Directory mediante una plantilla de administrador de recursos en los laboratorios de desarrollo y pruebas de Azure tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
