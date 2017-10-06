---
title: "las fórmulas de aaaManage en toocreate de laboratorios de desarrollo y pruebas de Azure VM | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupdate y quite las fórmulas de laboratorios de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Administración de fórmulas de Azure DevTest Labs

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Este artículo se explica cómo toocreate una fórmula de una base (imagen personalizada, una imagen de Marketplace u otra fórmula) o en una máquina virtual existente. Este artículo también le guía a través de la administración de las fórmulas existentes.

## <a name="create-a-formula"></a>Creación de una fórmula
Cualquier persona con laboratorios de desarrollo y pruebas *usuarios* permisos es capaz de toocreate las máquinas virtuales usando una fórmula como base. Hay dos maneras de toocreate fórmulas: 

* Desde una base - utilice cuando desee toodefine todas las características de Hola de fórmula de saludo.
* En un laboratorio existente VM - Utilice esta opción cuando desee toocreate una fórmula basado en valores de hello de una máquina virtual existente.

Para obtener más información sobre cómo agregar usuarios y permisos, consulte [Adición de propietarios y usuarios en Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Creación de una fórmula desde una base
Hola pasos le guiará a través de proceso de Hola de creación de una fórmula de una imagen personalizada, una imagen de Marketplace u otra fórmula.

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.

3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  

4. En la hoja del laboratorio de hello, seleccione **fórmulas (reutilizables bases)**.
   
    ![Menú Fórmula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. En hello **fórmulas** hoja, seleccione **+ agregar**.
   
    ![Agregar una fórmula](./media/devtest-lab-create-formulas/add-formula.png)

6. En hello **elegir una base de** hoja, base de Hola seleccione (imagen personalizada, una imagen de Marketplace o fórmula) desde el que se usará de fórmula de hello toocreate.
   
    ![Lista base](./media/devtest-lab-create-formulas/base-list.png)

7. En hello **crear fórmula** hoja, especifique Hola siguientes valores:
   
    * **Nombre de fórmula** : escriba un nombre para la fórmula. Este valor se muestra en la lista de Hola de imágenes de base cuando se crea una máquina virtual. nombre de Hola se valida como escribe, y si no es válido, un mensaje indica los requisitos de Hola para un nombre válido.
    * **Descripción** : escriba una descripción significativa para la fórmula. Este valor está disponible desde el menú contextual de la fórmula de hello cuando se crea una máquina virtual.
    * **Nombre de usuario**: escriba un nombre de usuario al que se concederán privilegios de administrador.
    * **Contraseña** : escriba - o seleccione en la lista desplegable de hello - un valor que está asociado con el secreto de hello (contraseña) que quiere toouse de usuario especificado de Hola. Para obtener más información acerca de los secretos de hello, consulte [laboratorios de desarrollo y pruebas de Azure: almacén secreto Personal](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Tipo de disco de máquina virtual** : especifique cualquier unidad de disco duro (unidad de disco duro) o si se permite tooindicate SSD (unidad de estado sólido) qué almacenamiento es el tipo de disco para las máquinas virtuales de hello aprovisionadas usando esta imagen base.
    * ** Máquina Virtual de tamaño **: seleccione uno de los elementos de hello predefinido que especifiquen los núcleos de procesador de hello, el tamaño de RAM y tamaño de unidad de disco duro de Hola de hello VM toocreate. 
    * **Artefactos** -tooopen seleccione hello **agregar artefactos** hoja, en el que seleccione y configure los artefactos de Hola que desea que la imagen base de tooadd toohello. Para obtener más información sobre los artefactos, vea [Administración de artefactos de máquina virtual en Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Configuración avanzada** -tooopen seleccione hello **avanzadas** hoja donde configurar Hola después de configuración:
        * **Red virtual** -especificar Hola deseada de red virtual.
        * **Subred** -especificar la subred de hello deseado.    
        * **Configuración de dirección IP** -especificar si desea que Hola Public, Private o compartido direcciones IP. Para obtener más información sobre las direcciones IP compartidas, consulte [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md) (Direcciones IP compartidas en Azure DevTest Labs).
        * **Hacer que esta máquina claimable** -realizar una máquina "claimable" significa que se le no asignará la propiedad en tiempo de presentación de la creación. En su lugar, los usuarios del laboratorio será máquina de hello tootake capaz de propiedad ("notificaciones") en la hoja del laboratorio de Hola.     
    * **Imagen** : este campo muestra el nombre de imagen base Hola que ha seleccionado en la hoja de hello anterior. 
     
       ![Crear fórmula](./media/devtest-lab-create-formulas/create-formula.png)

8. Seleccione **crear** toocreate fórmula de saludo.

9. Cuando se ha creado la fórmula de hello, muestra en lista Hola Hola **fórmulas** hoja.

### <a name="create-a-formula-from-a-vm"></a>Creación de una fórmula desde una máquina virtual
Hello pasos siguientes guiarán a través del proceso de Hola de creación de una fórmula basada en una máquina virtual existente. 

> [!NOTE]
> toocreate una fórmula de una máquina virtual, Hola VM debe haber creado después del 30 de marzo de 2016. 
> 
> 

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  
4. En el laboratorio de hello **Introducción** hoja, VM Hola seleccione desde el que desea fórmula de hello toocreate.
   
    ![Máquinas virtuales de laboratorios](./media/devtest-lab-create-formulas/my-vms.png)
5. En la hoja de la máquina virtual de hello, seleccione **crear fórmula (base reutilizable)**.
   
    ![Crear fórmula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. En hello **crear fórmula** hoja, escriba una **nombre** y **descripción** para la nueva fórmula.
   
    ![Hoja Crear fórmula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Seleccione **Aceptar** toocreate fórmula de saludo.

## <a name="modify-a-formula"></a>Modificación de una fórmula
toomodify una fórmula, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  
4. En la hoja del laboratorio de hello, seleccione **fórmulas (reutilizables bases)**.
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. En hello **fórmulas de laboratorio** hoja, fórmula Seleccione Hola desea toomodify.
6. En hello **actualizar fórmula** hoja, edite el Hola deseado y seleccione **actualización**.

## <a name="delete-a-formula"></a>Eliminación de una fórmula
toodelete una fórmula, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  
4. En el laboratorio de hello **configuración** hoja, seleccione **fórmulas**.
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. En hello **fórmulas de laboratorio** hoja, seleccione Hola puntos suspensivos toohello derecha de la fórmula de hello desea toodelete.
   
    ![Menú Fórmula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. En el menú contextual de la fórmula de hello, seleccione **eliminar**.
   
    ![Menú contextual de fórmula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Seleccione **Sí** cuadro de diálogo de confirmación de eliminación de toohello.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Entradas blogs relacionadas
* [Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Pasos siguientes
Una vez haya creado una fórmula para usarla al crear una máquina virtual, paso siguiente hello es demasiado[agregar un laboratorio VM tooyour](devtest-lab-add-vm-with-artifacts.md).

