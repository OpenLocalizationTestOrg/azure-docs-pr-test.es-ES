---
title: "Explorador de almacenamiento de aaaConnect tooan suscripción de la pila de Azure"
description: "Obtenga información acerca de cómo tooconnect Exporer de almacenamiento tooan suscripción de la pila de Azure"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a>Conectar Explorador de almacenamiento tooan Azure pila suscripción

Explorador de almacenamiento de Azure (vista previa) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de la pila de Azure en Windows, Mac OS y Linux. Hay varias herramientas permiten toomove datos tooand pila del almacenamiento de Azure. Para más información, consulte [Herramientas de transferencia de datos de Azure Stack Storage](azure-stack-storage-transfer.md).

En este artículo, aprenderá cómo tooconnect tooyour almacenamiento de Azure pila cuentas con el Explorador de almacenamiento. 

Si no ha instalado todavía el Explorador de Storage, [descárguelo](http://www.storageexplorer.com/) y hágalo.

Después de conectar tooyour suscripción de pila de Azure, puede usar hello [artículos Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork con los datos de la pila de Azure. 

## <a name="prepare-an-azure-stack-subscription"></a>Preparación de una suscripción de Azure Stack

Necesitará tener acceso de escritorio de la máquina de host de toohello pila de Azure o una conexión VPN para la suscripción de Azure pila de explorador de almacenamiento tooaccess Hola. toolearn tooset seguridad un tooAzure de conexión VPN pila, vea [conectar tooAzure pila con VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).

Para hello Kit de desarrollo de pila de Azure, necesita certificado de raíz de entidad emisora de tooexport Hola pila de Azure.

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a>tooexport y, a continuación, importar hello Azure pila certificado

1. Abra `mmc.exe` en un equipo de host de la pila de Azure, o en un equipo local con una tooAzure de conexión VPN pila. 

2. En **archivo**, seleccione **agregar o quitar complemento**y, a continuación, agregue **certificados** toomanage **cuenta de equipo** de **Local Equipo**.



3. En **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates** busque **AzureStackSelfSignedRootCert**.

    ![Cargar certificado de raíz de hello Azure pila mediante mmc.exe][25]

4. El certificado de Hola de menú contextual, seleccione **todas las tareas** > **exportar**y, a continuación, siga el certificado de Hola Hola instrucciones tooexport con **codificado en Base 64 X.509 (. CER)**.  

    se usará en el paso siguiente de Hola Hola de certificado exportado.
5. Inicie el Explorador de almacenamiento (versión preliminar), y si ve hello **conectar tooAzure almacenamiento** diálogo cuadro, cancele el proceso.

6. En hello **editar** menú, seleccione demasiado**certificados SSL**y, a continuación, haga clic en **importar certificados**. Utilice toofind del cuadro de diálogo de hello archivo selector y el certificado de hello abierto que exportó en el paso anterior de Hola.

    Después de importar, son toorestart solicitada Explorador de almacenamiento.

    ![Importar el certificado de hello en el Explorador de almacenamiento (versión preliminar)][27]

Ahora está listo tooconnect suscripción de Azure pila tooan de explorador de almacenamiento.

### <a name="tooconnect-an-azure-stack-subscription"></a>tooconnect una suscripción de la pila de Azure


1. Una vez reiniciado el Explorador de almacenamiento (versión preliminar), seleccione hello **editar** menú y, a continuación, asegúrese de que **pila de Azure de destino** está seleccionada. Si no está seleccionada, selecciónela y, a continuación, reinicie el Explorador de almacenamiento para cambiar tootake efecto de Hola. Esta configuración es necesaria para obtener compatibilidad con el entorno de Azure Stack.

    ![Comprobación de que Azure Stack de destino está activada][28]

7. En el panel izquierdo de hello, seleccione **administrar cuentas de**.  
    Que ha iniciado sesión tooare muestra todas las cuentas de Microsoft de Hola.

8. tooconnect toohello cuenta de la pila de Azure, seleccione **agregar una cuenta**.

    ![Adición de una cuenta de Azure Stack][29]

9. Hola **conectar tooAzure almacenamiento** cuadro de diálogo **entorno de Azure**, seleccione **entorno de pila de usar Azure**y, a continuación, haga clic en **siguiente**.

10. toosign con hello cuenta de pila de Azure que está asociado con al menos una suscripción activa de la pila de Azure, rellene hello **iniciar sesión en el entorno de pila tooAzure** cuadro de diálogo.  

    detalles de Hola para cada campo son los siguientes:

    * **Nombre del entorno**: campo de hello puede personalizarse por usuario.
    * **Punto de conexión de recurso ARM**: Hola ejemplos de puntos de conexión de recursos de Azure Resource Manager:

        * Para operadores en la nube:<br> https://adminmanagement.local.azurestack.external   
        * Para el inquilino:<br> https://management.local.azurestack.external
 
    * **Identificador de inquilino**: opcional. se asigna un valor de Hello solo cuando se debe especificar el directorio de Hola.

12. Una vez que inicie sesión correctamente con una cuenta de la pila de Azure, panel izquierdo de Hola se rellena con las suscripciones de Azure pila Hola asociadas con esa cuenta. Seleccione las suscripciones de la pila de Azure de Hola que desee toowork con y, a continuación, seleccione **aplicar**. (Activando o desactivando hello **todas las suscripciones** alterna de casilla de verificación Seleccionar todos o ninguno de Hola muestran las suscripciones de la pila de Azure.)

    ![Seleccione las suscripciones de Azure pila Hola después de rellenar el cuadro de diálogo del entorno de nube personalizada hello][30]  
    panel izquierdo de Hello muestra las cuentas de almacenamiento de hello asociadas con suscripciones de Azure pila Hola seleccionado.

    ![Lista de cuentas de almacenamiento, incluidas las cuentas de suscripción de Azure Stack][31]

## <a name="next-steps"></a>Pasos siguientes
* [Introducción al Explorador de Storage (versión preliminar)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Azure Stack Storage: Diferencias y consideraciones](azure-stack-acs-differences.md)


* toolearn más sobre el almacenamiento de Azure, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md)

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
