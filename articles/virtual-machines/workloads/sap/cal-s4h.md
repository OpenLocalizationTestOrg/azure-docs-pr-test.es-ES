---
title: "aaaDeploy 4HANA/S de SAP o BW/4HANA en una máquina virtual de Azure | Documentos de Microsoft"
description: "Implementación de SAP S/4HANA o BW/4HANA en una máquina virtual de Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Implementación de SAP S/4HANA o BW/4HANA en Azure
Este artículo describe cómo toodeploy S/4HANA en Azure mediante el uso de Hola biblioteca de dispositivo de nube de SAP (SAP CAL) 3.0. toodeploy otras soluciones basadas en SAP HANA, por ejemplo, BW/4HANA, siguen Hola mismos pasos.

> [!NOTE]
Para obtener más información acerca de hello CAL de SAP, visite toohello [biblioteca de dispositivo de nube de SAP](https://cal.sap.com/) sitio Web. SAP tiene también un blog sobre hello [SAP en la nube Appliance biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Tal y como del 29 de mayo de 2017, puede usar el modelo de implementación de Azure Resource Manager hello además preferido menor toohello de implementación clásica modelo toodeploy Hola CAL de SAP. Se recomienda que use el nuevo modelo de implementación de administrador de recursos hello y pasar por alto el modelo de implementación clásica de Hola.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Solución de hello toodeploy proceso paso a paso

Hola sigue la secuencia de capturas de pantalla muestra cómo toodeploy S/4HANA en Azure mediante el uso de Hola CAL de SAP. proceso de Hello funciona Hola igual en otras soluciones, como BW/4HANA.

Hola **soluciones** página muestra algunas de hello soluciones basadas en SAP HANA de CAL disponibles en Azure. **SAP S/4HANA 1610 FPS01, dispositivo Fully-Activated** está en la fila de hello central:

![Soluciones de SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Crear una cuenta de hello CAL de SAP
1. toosign en toohello CAL de SAP para hello primera vez, utilice el usuario S SAP u otro usuario registrado con SAP. A continuación, defina una cuenta de CAL de SAP que se usa por dispositivos de toodeploy Hola CAL de SAP en Azure. En la definición de la cuenta de hello, necesitará:

    a. Seleccione el modelo de implementación de hello en Azure (Administrador de recursos o estándar).

    b. Especifique la suscripción a Azure. Puede asignarse a una cuenta de SAP CAL tooone suscripción solo. Si necesita más de una suscripción, deberá toocreate otra cuenta de CAL de SAP.

    c. Dar permiso toodeploy de hello CAL de SAP en su suscripción de Azure.

    > [!NOTE]
    pasos siguientes Hola muestran cómo cuenta toocreate una CAL de SAP para las implementaciones del Administrador de recursos. Si ya tiene una cuenta de CAL de SAP que sea el modelo de implementación clásica toohello vinculado, se *necesita* toofollow estos toocreate pasos una nueva cuenta de CAL de SAP. nueva cuenta de CAL de SAP Hola debe toodeploy en el modelo de administrador de recursos de Hola.

2. Cree una nueva cuenta de SAP CAL. Hola **cuentas** página muestra tres opciones de Azure: 

    a. **Microsoft Azure (clásica)** es el modelo de implementación clásica de Hola y ya no se prefiere.

    b. **Microsoft Azure** es Hola nuevo modelo de implementación de administrador de recursos.

    c. **Windows Azure operado por 21Vianet** es una opción en China que usa el modelo de implementación clásica de Hola.

    Seleccione toodeploy en el modelo del Administrador de recursos de hello, **Microsoft Azure**.

    ![Detalles de la cuenta de SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. Escriba hello Azure **Id. de suscripción** que pueden encontrarse en hello portal de Azure.

   ![Cuentas de SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. tooauthorize Hola SAP CAL toodeploy en hello suscripción de Azure ha definido, haga clic en **Authorize**. Hola después de la página aparece en la pestaña de explorador hello:

   ![Inicio de sesión de servicios en la nube de Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Si aparece más de un usuario, elija la cuenta de Microsoft de Hola que está vinculado toobe hello coadministrator de hello Azure suscripción que ha seleccionado. Hola después de la página aparece en la pestaña de explorador hello:

   ![Confirmación de servicios en la nube de Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Haga clic en **Aceptar**. Si es correcta la autorización de hello, vuelve a mostrar hello definición de la cuenta de CAL de SAP. Después de unos minutos, un mensaje confirmará que el proceso de autorización de hello fue correcta.

7. Hola tooassign recién creado tooyour de cuenta SAP CAL de usuario, escriba su **Id. de usuario** en Hola Hola derecho cuadro de texto y haga clic en **agregar**.

   ![Asociación de cuenta toouser](./media/cal-s4h/s4h-pic8a.png)

8. tooassociate su cuenta con usuario Hola que usas toosign en toohello CAL de SAP, haga clic en **revisión**. 
 
9. asociación de hello toocreate entre el usuario y la cuenta de CAL de SAP de hello recién creado, haga clic en **crear**.

   ![Asociación de cuenta de usuario tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

Ha creado correctamente una cuenta de SAP CAL que puede:

- Utilice el modelo de implementación del Administrador de recursos de Hola.
- Implementar sistemas de SAP en su suscripción a Azure.

Ahora puede iniciar toodeploy S/4HANA en su suscripción de usuario en Azure.

> [!NOTE]
Antes de continuar, determine si dispone de cuotas de núcleos de Azure para máquinas virtuales de la serie H de Azure. En el momento de hello, Hola CAL de SAP usa H-Series máquinas virtuales de Azure toodeploy algunas de las soluciones basadas en SAP HANA de Hola. Su suscripción de Azure podría no tener ninguna cuota de núcleos para la serie H. Si es así, tendrá que tooget de soporte técnico de Azure toocontact una cuota de núcleos de al menos 16 H-Series.

> [!NOTE]
Al implementar una solución en Azure en hello CAL de SAP, es posible que puede elegir solo una región de Azure. toodeploy en regiones de Azure que no sea de hello uno sugeridos por hello CAL de SAP, deberá toopurchase una suscripción de CAL de SAP. También tendrá que tooopen un mensaje con SAP toohave su toodeliver de cuenta habilitada CAL en regiones de Azure que no sea de Hola que se sugieren inicialmente.

### <a name="deploy-a-solution"></a>Implementación de una solución

Vamos a implementar una solución de hello **soluciones** página de hello CAL de SAP. Hola CAL de SAP tiene dos toodeploy de secuencias:

- Una secuencia básica que utiliza una página toodefine Hola sistema toobe implementado
- Una secuencia avanzada que le ofrece varias opciones en relación al tamaño de las máquinas virtuales 

Se muestra aquí toodeployment de ruta de acceso básico de Hola.

1. En hello **detalles de la cuenta** página, necesita:

    a. Seleccionar una cuenta de SAP CAL. (Utilice una cuenta que sea toodeploy asociado con el modelo de implementación del Administrador de recursos de hello).

    b. Especificar en **Name** el nombre de la instancia.

    c. Seleccionar una **región** de Azure. Hola CAL de SAP sugiere una región. Si necesita otra región de Azure y no tiene una suscripción de CAL de SAP, deberá tooorder una CAL de suscripción con SAP.

    d. Escriba un patrón **contraseña** para la solución de Hola de ocho o nueve caracteres. Hola contraseña se usa para los administradores de Hola de diferentes componentes de Hola.

   ![SAP CAL, Modo básico: crear instancia](./media/cal-s4h/s4h-pic10a.png)

2. Haga clic en **crear**y en el cuadro de mensaje de Hola que aparece, haga clic en **Aceptar**.

   ![Tamaños de máquinas virtuales que admite SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. Hola **clave privada** cuadro de diálogo, haga clic en **almacén** clave privada de toostore Hola Hola CAL de SAP. Haga clic en protección con contraseña de clave privada de hello, toouse **descargar**. 

   ![Clave privada de SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. Hola de lectura SAP CAL **advertencia** el mensaje y haga clic en **Aceptar**.

   ![Advertencia de SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    Ahora la implementación de hello tiene lugar. Más tarde, según el tamaño de Hola y la complejidad de solución de hello (Hola CAL de SAP proporciona una estimación), Hola estado se muestra como activo y preparado para su uso.

5. recopilados con las máquinas virtuales de toofind Hola Hola otros recursos asociados en un grupo de recursos, vaya toohello portal de Azure: 

   ![Objetos de CAL de SAP implementados en el nuevo portal de Hola](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. En el portal de SAP CAL hello, estado de hello aparece como **Active**. solución de toohello tooconnect, haga clic en **conectar**. Se implementan diferentes componentes de diferentes opciones tooconnect toohello dentro de esta solución.

   ![Instancias de SAP CAL](./media/cal-s4h/active_solution.png)

7. Para poder usar uno de hello opciones tooconnect toohello implementado sistemas, haga clic en **Getting Started Guide**. 

   ![Conectar toohello instancia](./media/cal-s4h/connect_to_solution.png)

    nombres de la documentación de Hola Hola a los usuarios para cada uno de los métodos de conectividad de Hola. las contraseñas de Hola para los usuarios se establecen toohello contraseña maestra que ha definido al principio de Hola Hola del proceso de implementación. En la documentación de hello, otros usuarios más funcionales se muestran con sus contraseñas, que se pueden usar toosign en toohello implementa el sistema. 

    Por ejemplo, si usas Hola GUI de SAP está preinstalado en la máquina de escritorio remoto de Windows hello, Hola sistema S/4 podría ser similar al siguiente:

   ![SM50 Hola preinstalado GUI de SAP](./media/cal-s4h/gui_sm50.png)

    O bien, si usas hello DBACockpit, instancia Hola podría ser similar al siguiente:

   ![SM50 Hola DBACockpit GUI de SAP](./media/cal-s4h/dbacockpit.png)

En unas horas, una aplicación SAP S/4 correcta se implementa en Azure.

Si ha adquirido una suscripción de CAL de SAP, SAP admite totalmente las implementaciones a través de hello CAL de SAP en Azure. cola de soporte técnico de Hello es BC-VCM-CAL.







