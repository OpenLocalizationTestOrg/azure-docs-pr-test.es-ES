---
title: aaaConfigure CHAP para el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo tooconfigure Hola protocolo de autenticación por desafío mutuo (CHAP) en un dispositivo de StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>Configurar CHAP para el dispositivo StorSimple
Este tutorial le explica cómo tooconfigure CHAP para el dispositivo StorSimple. procedimiento de Hello detallado en este artículo aplica 8000 serie de tooStorSimple, así como dispositivos de StorSimple 1200.

CHAP significa Protocolo de autenticación por desafío mutuo. Es un esquema de autenticación usado por identidad de hello toovalidate de servidores de clientes remotos. comprobación de Hola se basa en una contraseña compartida o un secreto. CHAP puede ser unidireccional o mutuo (bidireccional). CHAP unidireccional es cuando el destino de hello autentica como iniciador. CHAP bidireccional o mutuo, en hello otra parte, requiere que el destino de hello autentique el iniciador de hello y, a continuación, el iniciador de hello autenticar destino Hola. La autenticación del iniciador puede implementarse sin la autenticación del destino. Sin embargo, la autenticación del destino solo puede implementarse si también se implementa la autenticación del iniciador. 

Como práctica recomendada, se recomienda que utilice la seguridad CHAP tooenhance iSCSI.

> [!NOTE]
> Tenga en cuenta que los dispositivos StorSimple no admiten IPSEC actualmente.
> 
> 

configuración de CHAP Hello en dispositivo de StorSimple de hello puede configurarse en hello siguientes maneras:

* Autenticación unidireccional
* Autenticación bidireccional o mutua o inversa

En cada uno de estos casos, el portal de Hola para dispositivo de Hola y el software del iniciador de iSCSI de hello server necesita toobe configurado. Hello pasos detallados para esta configuración se describen en hello siguiendo el tutorial.

## <a name="unidirectional-or-one-way-authentication"></a>Autenticación unidireccional
En la autenticación unidireccional, destino Hola autentica el iniciador de Hola. Esta autenticación requiere que configure valores del iniciador de CHAP hello en dispositivo de StorSimple de Hola y Hola iSCSI software Initiator en el host de Hola. Hola procedimientos detallados para el dispositivo StorSimple y host de Windows se describen a continuación.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure el dispositivo para la autenticación unidireccional
1. En el portal de Azure clásico en Hola Hola **dispositivos** página, haga clic en hello **configurar** ficha.
   
    ![Iniciador de CHAP](./media/storsimple-configure-chap/IC740943.png)
2. Desplácese hacia abajo en esta página y en hello **iniciador CHAP** sección:
   
   1. Proporcione un nombre de usuario para su iniciador de CHAP.
   2. Proporcionar una contraseña para su iniciador de CHAP.
      
    > [!IMPORTANT]
    > nombre de usuario CHAP Hola debe contener menos de 233 caracteres. Contraseña CHAP de Hello debe tener entre 12 y 16 caracteres. Un nombre de usuario o una contraseña más larga se producirá un error de autenticación en el host de Windows hello.
   
   3. Confirmar contraseña Hola.
3. Haga clic en **Guardar**. Aparecerá un mensaje de confirmación. Haga clic en **Aceptar** cambios de hello toosave.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>servidor de host tooconfigure autenticación unidireccional en Windows hello
1. En el servidor de host de Windows hello, inicie el iniciador iSCSI de Hola.
2. Hola **propiedades del iniciador iSCSI** ventana, realizar Hola pasos:
   
   1. Haga clic en hello **detección** ficha.
      
       ![Propiedades del iniciador iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. Haga clic en **Detectar portal**.
3. Hola **detectar Portal de destino** cuadro de diálogo:
   
   1. Especifique la dirección IP de hello del dispositivo.
   2. Haga clic en **Avanzadas**.
      
       ![Detectar portal de destino](./media/storsimple-configure-chap/IC740945.png)
4. Hola **configuración avanzada** cuadro de diálogo:
   
   1. Seleccione hello **inicio de sesión habilitar CHAP** casilla de verificación.
   2. Hola **nombre** campo, nombre de usuario de Hola de fuente de alimentación que especificó para hello iniciador de CHAP en el portal clásico de Hola.
   3. Hola **secreto de destino** campo, una fuente de alimentación Hola contraseña que especificó para hello iniciador de CHAP en el portal clásico de Hola.
   4. Haga clic en **Aceptar**.
      
       ![General - Configuración avanzada](./media/storsimple-configure-chap/IC740946.png)
5. En hello **destinos** ficha de hello **propiedades del iniciador iSCSI** ventana, el estado del dispositivo Hola debe aparecer como **conectado**. Si usa un dispositivo StorSimple 1200, cada volumen se montará como un destino iSCSI como se muestra a continuación. Por lo tanto, los pasos 3 y 4 será necesario toobe repite para cada volumen.
   
    ![Volúmenes montados como destinos independientes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Si cambia el nombre de iSCSI de hello, se usará el nuevo nombre de Hola para nuevas sesiones de iSCSI. La nueva configuración no se utiliza para las sesiones existentes hasta que cierra sesión y vuelve a iniciar sesión.
   > 
   > 

Para obtener más información sobre cómo configurar CHAP en el servidor de host de Windows hello, vaya demasiado[consideraciones adicionales](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Autenticación bidireccional o mutua
En la autenticación bidireccional, destino de hello autentica el iniciador de hello y, a continuación, iniciador Hola autentica destino Hola. Esto requiere valores del iniciador CHAP de hello usuario tooconfigure hello, así como Hola invertir la configuración de CHAP en dispositivo de Hola y software en el host de hello del iniciador iSCSI. Hello procedimientos siguientes describen la autenticación mutua de hello pasos tooconfigure en el dispositivo de Hola y en el host de Windows hello.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure el dispositivo para la autenticación mutua
1. En el portal de Azure clásico en Hola Hola **dispositivos** página, haga clic en hello **configurar** ficha.
   
    ![Destino de CHAP](./media/storsimple-configure-chap/IC740948.png)
2. Desplácese hacia abajo en esta página y en hello **destino CHAP** sección:
   
   1. Proporcione un **Nombre de usuario de CHAP inverso** para su dispositivo.
   2. Proporcione una **Contraseña de CHAP inverso** para su dispositivo.
   3. Confirmar contraseña Hola.
3. Hola **iniciador CHAP** sección:
   
   1. Proporcione un **nombre de usuario** para su dispositivo.
   2. Proporcione una **contraseña** para su dispositivo.
   3. Confirmar contraseña Hola.
4. Haga clic en **Guardar**. Aparecerá un mensaje de confirmación. Haga clic en **Aceptar** cambios de hello toosave.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>servidor de host de la autenticación bidireccional tooconfigure en Windows hello
1. En el servidor de host de Windows hello, inicie el iniciador iSCSI de Hola.
2. Hola **propiedades del iniciador iSCSI** ventana, haga clic en hello **configuración** ficha.
3. Haga clic en **CHAP**.
4. Hola **secreto CHAP mutuo del iniciador iSCSI** cuadro de diálogo:
   
   1. Hola de tipo **contraseña de CHAP inverso** que configuró en hello portal de Azure clásico.
   2. Haga clic en **Aceptar**.
      
       ![Secreto CHAP mutuo del iniciador iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. Haga clic en hello **destinos** ficha.
6. Haga clic en hello **conectar** botón. 
7. Hola **conectar tooTarget** cuadro de diálogo, haga clic en **avanzadas**.
8. Hola **propiedades avanzadas** cuadro de diálogo:
   
   1. Seleccione hello **inicio de sesión habilitar CHAP** casilla de verificación.
   2. Hola **nombre** campo, nombre de usuario de Hola de fuente de alimentación que especificó para hello iniciador de CHAP en el portal clásico de Hola.
   3. Hola **secreto de destino** campo, una fuente de alimentación Hola contraseña que especificó para hello iniciador de CHAP en el portal clásico de Hola.
   4. Seleccione hello **realizar autenticación mutua** casilla de verificación.
      
       ![Autenticación mutua de configuración avanzada](./media/storsimple-configure-chap/IC740950.png)
   5. Haga clic en **Aceptar** configuración de CHAP hello toocomplete

Para obtener más información sobre cómo configurar CHAP en el servidor de host de Windows hello, vaya demasiado[consideraciones adicionales](#additional-considerations).

## <a name="additional-considerations"></a>Consideraciones adicionales
Hola **conexión rápida** característica no admite conexiones con CHAP habilitado. Cuando CHAP esté habilitado, asegúrese de que utiliza hello **conectar** botón que está disponible en hello **destinos** destino de tooa tooconnect de pestaña.

![Conectar tootarget](./media/storsimple-configure-chap/IC740947.png)

Hola **conectar tooTarget** cuadro de diálogo es hello presentan, seleccione **agregar esta lista de toohello de conexión de destinos favoritos** casilla de verificación. Esto garantiza que cada vez que se reinicie el equipo de hello, se realiza un intento toorestore Hola conexión toohello favoritos los destinos iSCSI.

## <a name="errors-during-configuration"></a>Errores durante la configuración
Si su configuración de CHAP es incorrecta, es probable que toosee una **error de autenticación** mensaje de error.

## <a name="verification-of-chap-configuration"></a>Verificación de la configuración de CHAP
Puede comprobar que CHAP se esté usando siguiendo los pasos de Hola.

#### <a name="tooverify-your-chap-configuration"></a>tooverify su configuración de CHAP
1. Haga clic en **Destinos favoritos**.
2. Seleccione el destino de hello para el que ha habilitado la autenticación.
3. Haga clic en **Detalles**.
   
    ![Destinos favoritos de las propiedades del iniciador iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. Hola **detalles de destino favorito** cuadro de diálogo Entrada de nota Hola Hola **autenticación** campo. Si la configuración de hello sea correcta, debe indicar **CHAP**.
   
    ![Detalles de destino favorito](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de la [Seguridad de StorSimple](storsimple-security.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

