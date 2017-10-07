---
title: aaaGet Hola misma experiencia de Office 365 en cualquier dispositivo con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooshare cualquier aplicación de Office 365 con los usuarios mediante el uso de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get Hola misma experiencia de Office 365 en cualquier dispositivo con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

En este artículo se explicará cómo toodeploy Office 365 en cualquier dispositivo de su empresa. Los usuarios pueden obtener hello las mismas capacidades y experiencia de interfaz de usuario en Windows, Apple y Android.

Para conseguirlo, usaremos Azure RemoteApp hospedando Office 365 en máquinas virtuales escalables de Azure a las que pueden conectarse los usuarios. A este conjunto de máquinas virtuales lo denominamos "colección en la nube".

## <a name="create-a-cloud-collection"></a>Creación de una colección en la nube
En primer lugar una vez haya creado una cuenta de Azure, navegue demasiado**RemoteApp** haciendo clic en el vínculo de hello en el lado izquierdo de Hola.
![Mostrar Azure RemoteApp en hello Portal de Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

A continuación, continuar, haga clic en **nueva** en la parte inferior de Hola y "Creación rápida" una colección. Proporcione un nombre, región de hello, suscripción hello, plan de Hola e imagen Hola "Proffesional de Office 2013" que se proporciona.
![Cuadro de diálogo Crear](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Después de finalizar la debe comenzar el proceso de creación de colección de hello formulario Hola. Esto puede tardar horas tooan más o menos.

![En espera](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Una vez que se realiza el proceso de hello, lo tendrá un aspecto similar al siguiente. Si hacemos clic en **Publicación** , podemos ver que ya publicamos la mayoría de las aplicaciones de Office.
![Colección creada](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Aplicaciones publicadas](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

En este momento también puede agregar más usuarios que tienen acceso toothis colección haciendo clic en **acceso de usuario**.
![Configurar el acceso del usuario](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Ahora vamos a probar conexión tooOffice 365!

## <a name="connect-toooffice-365"></a>Conectar tooOffice 365
Se le diríjase demasiado[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), desplácese hacia abajo y haga clic en **descargar clientes** tooinstall cliente de Azure RemoteApp hello en dispositivo Hola se encuentra en. Hola de capturas de pantalla siguientes son para Windows.

Una vez que inicia la aplicación hello se le preguntará toosign con su cuenta de Microsoft (anteriormente denominado "Live ID"), use Hola mismo como su cuenta de Azure por ahora. Tras iniciar sesión, debe ver una notificación sobre nuevas invitaciones, haga clic en ella y verá una lista como la siguiente. Aceptar la invitación de Hola que coincida con el correo electrónico de propietario de cuenta de Azure.

![Nueva invitación](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Este es lo que aparece cuando hay invitaciones nuevas.

![Aceptar una aplicación](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Una vez que acepta la invitación de hello debería ver todas las aplicaciones de Office de hello en el cliente de Azure RemoteApp Hola.

![Lista de aplicaciones](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Al hacer clic en cualquiera de estas aplicaciones Hola debe iniciarse en hello máquina virtual de Azure y debe tener establecidos. ¡Disfrute!

![iniciando](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

