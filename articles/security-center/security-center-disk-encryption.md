---
title: "aaaEncrypt máquinas virtuales de Azure | Documentos de Microsoft"
description: "Este documento le ayuda a tooencrypt máquinas virtuales de Azure después de recibir una alerta desde el centro de seguridad de Azure."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Cifrado de una máquina virtual de Azure
Azure Security Center le avisará si tiene máquinas virtuales que no estén cifradas. Estas alertas se mostrarán como recomendación hello y gravedad alta es tooencrypt estas máquinas virtuales.

![Recomendación de cifrado de disco](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> información de Hello en este documento aplica a las máquinas virtuales tooencrypting sin usar una clave de cifrado de clave (que es necesario para realizar una copia de seguridad de máquinas virtuales mediante copia de seguridad de Azure). Consulte el artículo de hello [cifrado de disco de Azure para Windows y máquinas virtuales de Linux Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) para obtener información acerca de cómo toouse un toosupport de clave de cifrado de clave cifrada máquinas virtuales de Azure de copia de seguridad de Azure.
>
>

tooencrypt máquinas virtuales de Azure que se han identificado por el centro de seguridad de Azure como la necesidad de cifrado, se recomienda Hola pasos:

* Instale y configure Azure PowerShell. Esto le permitirá toorun Hola PowerShell comandos necesario tooset seguridad Hola requisitos previos necesarios tooencrypt máquinas virtuales de Azure.
* Obtener y ejecutar el script de PowerShell de Azure de requisitos previos de cifrado de disco de Azure Hola
* Cifre las máquinas virtuales.

objetivo de Hola de este documento es tooenable tooencrypt las máquinas virtuales, incluso si tienen poca o ninguna fondo en PowerShell de Azure.
Este documento se supone que usa Windows 10 como equipo de cliente de Hola desde el que va a configurar el cifrado del disco de Azure.

Existen muchos enfoques que pueden ser requisitos previos de hello toosetup utilizado y cifrado tooconfigure máquinas virtuales de Azure. Si ya están muy versado en Azure PowerShell o CLI de Azure, quizás prefiera toouse los métodos alternativos.

> [!NOTE]
> toolearn más información acerca del cifrado de tooconfiguring de métodos alternativos para máquinas virtuales de Azure, visite [cifrado de disco de Azure para Windows y máquinas virtuales de Linux Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Instale y configure Azure PowerShell.
Debe tener Azure PowerShell versión 1.2.1 o superior instalado en el equipo. artículo de Hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) contiene todos los pasos de hello necesita tooprovision su toowork equipo con Azure PowerShell. enfoque más sencillo de Hello es el enfoque de instalación de Web PI toouse Hola mencionado en dicho artículo. Incluso si ya tiene instalado PowerShell de Azure, instale utilizando de nuevo enfoque de hello Web PI para que tenga la versión más reciente de Hola de PowerShell de Azure.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Obtener y ejecutar script de configuración de requisitos previos de cifrado de disco de Azure Hola
Hola Script de configuración de requisitos previos de cifrado de disco de Azure a configurar todos los requisitos previos de hello necesarios para el cifrado de las máquinas virtuales de Azure.

1. Página de GitHub de toohello vaya con hello [Script requisitos previos de instalación de Azure disco cifrado](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. En la página de GibHub hello, haga clic en hello **Raw** botón.
3. Usar **CTRL+a** tooselect todos los Hola texto en la página de hello y, a continuación, usar **CTRL-C** toocopy todos Hola texto hello página toohello Portapapeles.
4. Abra **el Bloc de notas** y pegue el texto hello copiado en el Bloc de notas.
5. Cree una nueva carpeta en la unidad C: denominada **AzureADEScript**.
6. Guardar archivo de Bloc de notas de hello: haga clic en **archivo**, a continuación, haga clic en **Guardar como**. En el cuadro de texto de nombre de archivo hello, escriba **"ADEPrereqScript.ps1"** y haga clic en **guardar**. (asegúrese de que se ponga comillas de hello en nombre de hello, en caso contrario, guardará el archivo hello con una extensión de archivo .txt).

Ahora que se guarda el contenido del script de Hola, abra el script de Hola Hola PowerShell ISE:

1. Hola menú Inicio, haga clic en **Cortana**. Pida **Cortana** "PowerShell" escribiendo **PowerShell** en el cuadro de texto de búsqueda de hello Cortana.
2. Haga clic con el botón derecho en **Windows PowerShell ISE** y haga clic en **Ejecutar como administrador**.
3. Hola **administrador: Windows PowerShell ISE** ventana, haga clic en **vista** y, a continuación, haga clic en **Mostrar panel de scripts**.
4. Si ve hello **comandos** panel de hello derecha de la ventana de hello, haga clic en hello **"x"** en hello superior derecho de hello panel tooclose se. Si es demasiado pequeño para toosee texto hello, use **CTRL + agregar** ("Agregar" Hola "+" iniciar sesión). Si el texto hello es demasiado grande, use **CTRL + restar** (restar es hello "-" inicio de sesión).
5. Haga clic en **Archivo** y, a continuación, en **Abrir**. Navegue toohello **C:\AzureADEScript** hello y carpeta, haga doble clic en hello **ADEPrereqScript**.
6. Hola **ADEPrereqScript** contenido debería aparecer ahora en PowerShell ISE hello y está codificada por colores toohelp vea varios componentes, como comandos, parámetros y variables más fácilmente.

Ahora debería ver algo parecido a Hola figura a continuación.

![Ventana de PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

panel superior de Hello es que se hace referencia tooas hello "panel de scripts" y panel inferior de hello es que se hace referencia tooas hello "consola". Estos términos se utilizarán más adelante en este artículo.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Ejecutar comando de PowerShell de requisitos previos de cifrado de disco de Azure de Hola
Hello secuencia de comandos de requisitos previos de cifrado de disco de Azure le pedirá Hola siguiente información después de iniciar la secuencia de comandos de hello:

* **Nombre del grupo de recursos de** : el nombre de grupo de recursos que desea tooput hello hello en el almacén de claves.  Si no hay ya uno con ese nombre creado, se creará un nuevo grupo de recursos con nombre de Hola que especifique. Si ya tiene un grupo de recursos que desea toouse en esta suscripción, a continuación, escriba el nombre de Hola de ese grupo de recursos.
* **Nombre del almacén de claves** -nombre del almacén de claves de hello en que el cifrado de claves son toobe colocado. Si aún no hay ninguno, se creará un Almacén de claves con este nombre. Si ya tiene un almacén de claves que desee toouse, escriba el nombre de Hola de hello existente en el almacén de claves.
* **Ubicación** -ubicación de almacén de claves de Hola. Asegurarse de que toobe de almacén de claves y las máquinas virtuales de hello cifra Hola misma ubicación. Si no conoce la ubicación de hello, hay pasos más adelante en este artículo que le mostrará cómo toofind out.
* **Azure Active Directory NombreAplicación** -nombre del programa Hola a aplicaciones de Azure Active Directory que serán usado toowrite secretos toohello el almacén de claves. Si no existe, se creará una aplicación con este nombre. Si ya tiene una aplicación de Azure Active Directory que desea que toouse, escriba el nombre de Hola de esa aplicación de Azure Active Directory.

> [!NOTE]
> Si tiene curiosidad como toowhy necesita toocreate una aplicación de Azure Active Directory, vea *registrar una aplicación con Azure Active Directory* sección en el artículo hello [Introducción al almacén de claves de Azure](../key-vault/key-vault-get-started.md).
>
>

Lleve a cabo Hola siguiendo los pasos tooencrypt máquinas virtuales de Azure:

1. Si ha cerrado Hola PowerShell ISE, abra una instancia con privilegios elevados de hello PowerShell ISE. Siga las instrucciones de hello anteriormente en este artículo si abre Hola que PowerShell ISE ya no está. Si lo ha cerrado la secuencia de comandos de hello, a continuación, abra hello **ADEPrereqScript.ps1** al hacer clic en **archivo**, a continuación, **abrir** y selecciona la secuencia de comandos de hello en hello **c:\ AzureADEScript** carpeta. Si ha seguido en este artículo de inicio de hello, a continuación, mover en toohello siguiente paso.
2. En la consola de Hola de hello (Hola inferior de hello PowerShell ISE) de PowerShell ISE, cambiar Hola foco toohello local del script de Hola escribiendo **cd c:\AzureADEScript** y presione **ENTRAR**.
3. Configurar directiva de ejecución de hello en el equipo para que pueda ejecutar script de Hola. Tipo de **Set-ExecutionPolicy Unrestricted** Hola consola y, a continuación, presione ENTRAR. Si ve un cuadro de diálogo informar acerca de los efectos de Hola de directiva de tooexecution de cambio de hello, haga clic en **sí tooall** o **Sí** (si ve **sí tooall**, seleccione esta opción: si no se ve **sí tooall**, a continuación, haga clic en **Sí**).
4. Inicie sesión en la cuenta de Azure. En la consola de hello, escriba **AzureRmAccount de inicio de sesión** y presione **ENTRAR**. Aparecerá un cuadro de diálogo en el que escriba sus credenciales (asegúrese de que tiene derechos toochange Hola máquinas virtuales si no tiene derechos, no será capaz de tooencrypt ellos. Si no está seguro, pregunte al administrador o propietario de la suscripción). Debería ver la información de los valores **Environment**, **Account**, **TenantId**, **SubscriptionId** y **CurrentStorageAccount**. Hola copia **SubscriptionId** tooNotepad. Deberá toouse esto en el paso 6 de #.
5. Buscar qué suscripción de la máquina virtual pertenece tooand su ubicación. Vaya demasiado[https://portal.azure.com](ttps://portal.azure.com) e inicie sesión.  En la parte izquierda de la página de Hola de hello, haga clic en **máquinas virtuales**. Verá una lista de las máquinas virtuales y las suscripciones de Hola que pertenecen.

   ![Máquinas virtuales](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Devolver toohello PowerShell ISE. Establecer el contexto de la suscripción de hello en el que se ejecutará el script de Hola. En la consola de hello, escriba **seleccione AzureRmSubscription: Id. de suscripción < your_subscription_Id >** (reemplace **< your_subscription_Id >** con su identificador de suscripción real) y presione  **Escriba**. Verá información sobre el entorno, Hola **cuenta**, **TenantId**, **SubscriptionId** y **CurrentStorageAccount**.
7. Ya estás listo toorun script de Hola. Haga clic en hello **ejecutar Script** o presionen **F5** teclado Hola.

   ![Ejecución del script de PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. script de Hola pide **resourceGroupName:** -escriba nombre Hola de *grupo de recursos* desea toouse, a continuación, presione **ENTRAR**. Si no tiene uno, escriba un nombre que desee toouse para una nueva. Si ya tiene un *grupo de recursos* que desea toouse (por ejemplo, Hola uno que la máquina virtual se encuentra en), escriba Hola nombre del programa Hola a grupo de recursos existente.
9. script de Hola pide **keyVaultName:** -escriba nombre Hola de hello *el almacén de claves* que desee toouse, y después presione ENTRAR. Si no tiene uno, escriba un nombre que desee toouse para una nueva. Si ya tiene un almacén de claves que desee toouse, escriba el nombre de Hola de hello existente *el almacén de claves*.
10. script de Hola pide **ubicación:** : escriba nombre de Hola de ubicación de hello en qué Hola se encuentra máquina virtual que desee tooencrypt, a continuación, presione **ENTRAR**. Si no recuerda la ubicación de hello, volver atrás toostep #5.
11. script de Hola pide **aadAppName:** -escriba nombre Hola de hello *Azure Active Directory* aplicación desea toouse, a continuación, presione **ENTRAR**. Si no tiene uno, escriba un nombre que desee toouse para una nueva. Si ya tiene un *aplicación de Azure Active Directory* que desea toouse, escriba nombre Hola de hello existente *aplicación de Azure Active Directory*.
12. Aparece un cuadro de diálogo de inicio de sesión. Proporcione sus credenciales (Sí, iniciar sesión una vez, pero ahora necesita toodo vuelva a).
13. Hola script se ejecuta y cuando haya finalizado, le pedirá que los valores de hello toocopy de hello **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**y **keyVaultResourceId**. Copiar cada uno de estos Portapapeles toohello de valores y péguelos en el Bloc de notas.
14. Devolver toohello PowerShell ISE y coloque el cursor de hello final hello de la última línea de hello y presione **ENTRAR**.

salida de Hello de script de Hola debe tener un aspecto como pantalla de bienvenida a continuación:

![Salida de PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Cifrar Hola máquina virtual de Azure
Se está ahora listo tooencrypt la máquina virtual. Si la máquina virtual se encuentra en Hola mismo grupo de recursos como su almacén de claves, puede mover en la sección de pasos de cifrado de toohello. Sin embargo, si la máquina virtual no está en hello mismo grupo de recursos como su almacén de claves, necesitará tooenter siguiente de hello en la consola de hello en hello PowerShell ISE:

**$resourceGroupName = &lt;’Virtual_Machine_RG’&gt;**

Reemplace **< Virtual_Machine_RG >** con nombre de Hola Hola del grupo de recursos en el que se encuentran las máquinas virtuales, flanqueado por comillas simples. A continuación, presione **ENTRAR**.
tooconfirm que Hola correcta de escribir el nombre de grupo de recursos, escriba el siguiente de Hola Hola consola de PowerShell ISE:

**$resourceGroupName**

Presione **ENTRAR**. Debería ver el nombre de hello del grupo de recursos que se encuentran las máquinas virtuales en. Por ejemplo:

![Salida de PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Pasos de cifrado
En primer lugar, necesita nombre de tootell PowerShell Hola de máquina virtual de hello desea tooencrypt. En la consola de hello, escriba:

**$vmName = &lt;’your_vm_name’&gt;**

Reemplace **<'your_vm_name ' >** con el nombre de saludo de la máquina virtual (asegúrese de que nombre Hola se incluye entre comillas simples) y, a continuación, presione **ENTRAR**.

tooconfirm que Hola correcta de escribir el nombre de máquina virtual, escriba:

**$vmName**

Presione **ENTRAR**. Debería ver Hola nombre de máquina virtual de hello desea tooencrypt. Por ejemplo:

![Salida de PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Hay dos métodos toorun Hola cifrado comando tooencrypt todas las unidades en la máquina virtual de Hola. Hola primer método es hello tootype siguiente comando en la consola de PowerShell ISE hello:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Después de escribir este comando, presione **ENTRAR**.

Hola segundo método es tooclick en panel de scripts de hello (panel superior de Hola de hello PowerShell ISE) y desplácese hacia abajo de la parte inferior de toohello de script de Hola. Resalte comando hello mencionado anteriormente y, a continuación, haga clic y, a continuación, haga clic en **Ejecutar selección** o presione **F8** teclado Hola.

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Independientemente del método hello usas, aparecerá un cuadro de diálogo que le informa de que tarda 10 y 15 minutos para hello operación toocomplete. Haga clic en **Sí**.

Mientras lleva a cabo el proceso de cifrado de hello, puede devolver toohello Portal de Azure y ver estado de saludo de la máquina virtual de Hola. En la parte izquierda de la página de Hola de hello, haga clic en **máquinas virtuales**, a continuación, en hello **máquinas virtuales** hoja, haga clic en nombre de Hola de máquina virtual de hello está cifrado. En la hoja de Hola que aparece, observará que hello **estado** dice que es **actualizar**. Esto demuestra que el cifrado está en proceso.

![Obtener más detalles sobre Hola VM](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Devolver toohello PowerShell ISE. Cuando se completa el script de Hola, podrá ver lo que aparece en la siguiente ilustración de Hola.

![Salida de PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

Ahora se cifra toodemonstrate que Hola máquina virtual, devolver toohello Portal de Azure y haga clic en **máquinas virtuales** en la parte izquierda de la página de Hola de Hola. Haga clic en el nombre de Hola de máquina virtual de Hola que se ha cifrado. Hola **configuración** hoja, haga clic en **discos**.

![Opciones de configuración](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

En hello **discos** hoja, verá que **cifrado** es **habilitado**.

![Propiedades de discos](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Pasos siguientes
En este documento, se habrá aprendido cómo tooencrypt máquinas virtuales de Azure. toolearn más información acerca del centro de seguridad de Azure, vea Hola recursos siguientes:

* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) -Obtenga información acerca de cómo toomanage y que responden las alertas de toosecurity
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : Encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
