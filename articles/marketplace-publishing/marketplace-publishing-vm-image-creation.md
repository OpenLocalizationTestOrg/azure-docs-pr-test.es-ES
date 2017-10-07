---
title: "aaaCreating una imagen de máquina virtual para hello Azure Marketplace | Documentos de Microsoft"
description: "Instrucciones detalladas sobre cómo toocreate una máquina virtual de la imagen para hello Azure Marketplace para que otros lo toopurchase."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Guía toocreate una imagen de máquina virtual para hello Azure Marketplace
En este artículo, **paso 2**, le guía a través de preparar los discos duros virtuales (VHD) que se implementará toohello Azure Marketplace de Hola. Los discos duros virtuales son la base de hello del SKU. proceso de Hello varía según si va a proporcionar una SKU basado en Windows o Linux. En este artículo se tratan ambos escenarios. Este proceso puede realizarse en paralelo con la [creación y registro de cuentas][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Definición de ofertas y SKU
En esta sección, aprenderá toodefine Hola ofertas y sus SKU asociado.

Una oferta es un tooall "primario" de su SKU. Puede tener varias ofertas. Cómo decidir toostructure sus ofertas está tooyou. Cuando una oferta se inserta toostaging, se inserta junto con todas sus SKU. Considere cuidadosamente los identificadores SKU, dado que serán visibles en la dirección URL de hello:

* Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}
* Portal de vista previa de Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}  

Un SKU es nombre comercial de Hola para una imagen de máquina virtual. Una imagen de máquina virtual contiene un disco del sistema operativo y cero o más discos de datos. Es básicamente Hola perfil de almacenamiento completo para una máquina virtual. Es necesario un VHD por disco. Los discos de datos incluso en blanco requieren un toobe de disco duro virtual creado.

Independientemente de qué sistema operativo que use, agregue solo Hola número mínimo de discos de datos necesita Hola SKU. Los clientes no pueden quitar los discos que forman parte de una imagen en el momento de saludo de la implementación, pero siempre pueden agregar discos durante o después de la implementación si se necesitan.

> [!IMPORTANT]
> **No cambie el número de discos en una nueva versión de imagen.** Si debe volver a configurar los discos de datos en la imagen de hello, defina una SKU nuevo. Publicar una nueva versión de imagen con recuentos de otro disco tendrá potencial de Hola de nueva implementación basada en la nueva versión de imagen hello en el caso de implementaciones de escalado automático, automático de soluciones a través de las plantillas ARM y otros escenarios de que se interrumpa.
>
>

### <a name="11-add-an-offer"></a>1.1 Agregar una oferta
1. Inicie sesión en toohello [Portal de publicación] [ link-pubportal] mediante el uso de tu cuenta de vendedor.
2. Seleccione hello **máquinas virtuales** ficha de hello Portal de publicación. En el campo de entrada solicitadas de hello, escriba el nombre de la oferta. nombre de la oferta de Hello suele ser el nombre de Hola de producto de Hola o servicio que piensa toosell en hello Azure Marketplace.
3. Seleccione **Crear**.

### <a name="12-define-a-sku"></a>1.2 Definir una SKU
Después de haber agregado una oferta, se necesita toodefine e identifican las SKU. Puede tener varias ofertas y cada oferta puede tener varias SKU. Cuando una oferta se inserta toostaging, se inserta junto con todas sus SKU.

1. **Agregue una SKU.** Hola SKU requiere un identificador, que se usa en la dirección URL de Hola. Hola identificador debe ser único dentro de su perfil de publicación, pero no hay ningún riesgo de colisiones entre los identificadores con otros publicadores.

   > [!NOTE]
   > oferta de Hola y los identificadores SKU se muestran en la dirección URL de la oferta de Hola Hola Marketplace.
   >
   >
2. **Agregue una descripción resumida de la SKU.** Descripciones resumidas son toocustomers visible, por lo que debería que sean fácilmente legibles. Esta información no es necesario toobe bloqueado hasta que la fase de "Inserción tooStaging" Hola. Hasta entonces, son tooedit libre se.
3. Si está utilizando SKU basados en Windows, siga los vínculos recomendados de Hola Hola tooacquire aprobado versiones de Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Creación de un VHD compatible con Azure (basado en Linux)
En esta sección se centra en los procedimientos recomendados para crear una imagen VM basadas en Linux para hello Azure Marketplace. Para ver un tutorial paso a paso, consulte toohello siguiente documentación: [crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Creación de un VHD compatible con Azure (basado en Windows)
En esta sección se centra en hello pasos toocreate una SKU basada en Windows Server para hello Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 Asegúrese de que está usando Hola corregir VHD base
Hola VHD del sistema operativo para la imagen de máquina virtual debe basarse en una imagen base aprobado de Azure que contiene Windows Server o SQL Server.

toobegin, crear una máquina virtual a partir de uno de hello después de imágenes, ubicadas en hello [portal de Microsoft Azure][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])

Estos vínculos también pueden encontrarse en hello Portal de publicación en la página SKU de Hola.

> [!TIP]
> Si utilizas el portal de Azure actual de Hola o PowerShell, se aprueban las imágenes de Windows Server publicadas en el 8 de septiembre de 2014 y versiones posteriores.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 Crear su propia máquina virtual basada en Windows
Desde el portal de Microsoft Azure hello, puede crear la máquina virtual en función de una imagen base aprobada en unos pocos pasos sencillos. Hola es una visión general del proceso de hello:

1. Desde la página de la imagen base de hello, seleccione **crear Máquina Virtual** toobe dirige toohello nueva [portal de Microsoft Azure][link-azure-portal].

    ![dibujo][img-acom-1]
2. Inicie sesión en el portal de toohello con hello cuenta Microsoft y la contraseña de hello suscripción de Azure que desee toouse.
3. Siga toocreate de mensajes de Hola una máquina virtual usando Hola imagen base que seleccionó. Debe tooprovide un nombre de host (nombre de equipo de hello), un nombre de usuario (registrado como administrador) y una contraseña para hello máquina virtual.

    ![dibujo][img-portal-vm-create]
4. Seleccione el tamaño de Hola de hello VM toodeploy:

    a.    Si tiene previsto toodevelop Hola VHD local, tamaño de hello no importa. Considere el uso de uno de hello máquinas virtuales más pequeñas.

    b.    Si tiene previsto toodevelop imagen de hello en Azure, considere la posibilidad de tamaños de máquina virtual para la imagen seleccionada de hello recomienda el uso de uno de Hola.

    c.    Para obtener más información, consulte toohello **recomienda los niveles de precios** selector que se muestra en el portal de Hola. Proporcionará Hola tres tamaños recomendados proporcionados por el Editor de Hola. (En este caso, el publicador de hello es Microsoft).

    ![dibujo][img-portal-vm-size]
5. Establezca las propiedades:

    a.    Para una implementación rápida, puede dejar Hola valores predeterminados para las propiedades de hello en **configuración opcional** y **grupo de recursos**.

    b.    En **cuenta de almacenamiento**, opcionalmente, puede seleccionar la cuenta de almacenamiento de hello en qué sistema operativo de Hola se almacenará el disco duro virtual.

    c.    En **grupo de recursos**, opcionalmente, puede seleccionar el grupo lógico de hello en qué tooplace Hola máquina virtual.
6. Seleccione hello **ubicación** para la implementación:

    a.    Si tiene previsto toodevelop Hola VHD local, ubicación de hello no importa porque se cargará Hola imagen tooAzure más tarde.

    b.    Si tiene previsto toodevelop imagen de hello en Azure, considere el uso de uno de regiones de Azure de Microsoft basado en Estados Unidos de Hola desde el principio de Hola. Esto acelera el proceso copia de hello discos duros virtuales que Microsoft lleva a cabo en su nombre al enviar la imagen para la certificación.

    ![dibujo][img-portal-vm-location]
7. Haga clic en **Crear**. Hola VM inicia toodeploy. En minutos, tendrá una implementación correcta y, a continuación, puede empezar la imagen de hello toocreate para el SKU.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 desarrollar el disco duro virtual en la nube de Hola
Se recomienda encarecidamente que desarrollar el disco duro virtual en la nube de hello mediante el protocolo de escritorio remoto (RDP). Conectar tooRDP con el nombre de usuario de Hola y la contraseña especificados durante el aprovisionamiento.

> [!IMPORTANT]
> Si está desarrollando su VHD de forma local (aunque no se recomienda), consulte [Creación de una imagen de máquina virtual de forma local](marketplace-publishing-vm-image-creation-on-premise.md). Descargar el disco duro virtual no es necesario si va a desarrollar en nube Hola.
>
>

**Conectarse a través de RDP mediante hello [portal de Microsoft Azure][link-azure-portal]**

1. Seleccione **Examinar** > **Máquinas virtuales**.
2. se abre la hoja de máquinas virtuales de Hola. Asegúrese de esa máquina virtual que desee tooconnect con hello está ejecutando y, a continuación, selecciónelo en la lista de Hola de máquinas virtuales implementadas.
3. Abre una hoja que describe Hola selecciona máquina virtual. En la parte superior de hello, haga clic en **conectar**.
4. Son nombre de usuario de hello tooenter solicitadas y la contraseña que especificó durante el aprovisionamiento.

**Conectarse mediante RDP con PowerShell**

toodownload un equipo local tooa de archivo de escritorio remoto, use hello [cmdlet Get-AzureRemoteDesktopFile][link-technet-2]. En Ordenar toouse este cmdlet, necesita nombre de hello tooknow del servicio de Hola y nombre del programa Hola a máquina virtual. Si ha creado Hola VM de hello [portal de Microsoft Azure][link-azure-portal], puede encontrar esta información en Propiedades de la máquina virtual:

1. En el portal de Microsoft Azure hello, seleccione **examinar** > **máquinas virtuales**.
2. se abre la hoja de máquinas virtuales de Hola. Seleccione Hola VM que ha implementado.
3. Abre una hoja que describe Hola selecciona máquina virtual.
4. Haga clic en **Propiedades**.
5. primera parte del nombre de dominio de Hola de Hello es el nombre del servicio de Hola. nombre de host de Hello es el nombre VM de Hola.

    ![dibujo][img-portal-vm-rdp]
6. Hola cmdlet toodownload Hola archivo RDP de escritorio local del Administrador de hello creado VM toohello es como sigue.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Se puede encontrar más información acerca de RDP en MSDN en el artículo de hello [conectar tooan máquina virtual de Azure con RDP o SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Configurar una máquina virtual y crear la SKU**

Después de disco duro virtual se descarga el sistema de operativo hello, use Hyper-v y configurar un toobegin VM crear el SKU. Encontrará pasos detallados en Hola siguiendo el vínculo de TechNet: [HyperV instalar y configurar una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 elegir tamaño de disco duro virtual correcto Hola
Hola Windows VHD del sistema operativo en la imagen de máquina virtual debe crearse como un disco duro virtual de 128 GB formato fijo.  

Si el tamaño físico de hello es inferior a 128 GB, Hola VHD debe ser disperso. Hola imágenes básicas de Windows y SQL Server proporcionadas ya cumple estos requisitos, por lo que no cambie el tamaño de formato u Hola Hola Hola obtenido de disco duro virtual.  

Los discos de datos pueden tener un tamaño de hasta 1 TB. Cuando se decida por tamaño de disco de hello, recuerde que los clientes no pueden cambiar discos duros virtuales dentro de una imagen en tiempo de Hola de implementación. Los VHD para discos de datos deben crearse como VHD de formato fijo. También deben ser dispersos. Los discos de datos pueden estar vacíos o contener datos.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 instalar revisiones de Windows más recientes de Hola
las imágenes base Hello contienen revisiones más recientes de Hola seguridad tootheir fecha de publicación. Antes de publicar el VHD del sistema operativo Hola ha creado y, a continuación, asegúrese de que Windows Update se ha ejecutado y que todos Hola crítico más reciente y que se instalaron las actualizaciones de seguridad importantes.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 Configurar opciones adicionales y programar tareas según sea necesario
Si se necesita configuración adicional, considere el uso de una tarea programada que se ejecuta en Inicio toomake cualquier toohello cambios finales VM después de que se haya implementado:

* Es una tarea de hello de mejor práctica toohave eliminar a sí mismo tras la ejecución correcta.
* Ninguna configuración debe confiarse en unidades distintas unidades C y D, porque se trata de hello solo dos unidades de disco que se garantiza que siempre tooexist. La unidad C es el disco del sistema operativo de Hola y unidad D es disco local temporal de Hola.

### <a name="37-generalize-hello-image"></a>3.7 generalizar la imagen de Hola
Todas las imágenes de hello Azure Marketplace deben ser reutilizables de forma genérica. En otras palabras, debe generalizarse Hola VHD del sistema operativo:

* Para Windows, la imagen de hello debe estar "preparada con Sysprep" y no debe realizarse ninguna configuración que no admiten hello **sysprep** comando.
* Puede ejecutar Hola siguiente comando de hello directory WINDIR%\System32\Sysprep.

        sysprep.exe /generalize /oobe /shutdown

  Instrucciones sobre cómo se proporciona el sistema operativo de toosysprep hello en el paso de hello artículo MSDN siguiente: [crear y cargar un VHD de Windows Server tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Implementación de una máquina virtual a partir de VHD
Después de haber cargado los discos duros virtuales (VHD del sistema operativo generalizado de Hola y datos de cero o más discos duros virtuales en disco) tooan cuenta de almacenamiento de Azure, puede registrarlos como una imagen de máquina virtual de usuario. A continuación, puede probar esa imagen. Tenga en cuenta que porque se ha generalizado el sistema operativo del disco duro virtual, no se puede implementar directamente Hola VM proporcionando Hola dirección URL del VHD.

toolearn más acerca de las imágenes de máquina virtual, siguiendo las entradas de blog de Hola de revisión:

* [Imagen de máquina virtual](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [Procedimientos para trabajar con imágenes de máquina virtual en PowerShell](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Acerca de las imágenes de máquina virtual en Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Configurar herramientas que necesitan hello, PowerShell y la CLI de Azure
* [¿Cómo toosetup PowerShell](/powershell/azure/overview)
* [¿Cómo toosetup CLI de Azure](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 Crear una imagen de máquina virtual de usuario
#### <a name="capture-vm"></a>Captura de máquina virtual
Lea los vínculos de hello indica a continuación para obtener instrucciones sobre cómo capturar Hola máquina virtual mediante PowerShell/API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI de Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Generalización de una imagen
Lea los vínculos de hello indica a continuación para obtener instrucciones sobre cómo capturar Hola máquina virtual mediante PowerShell/API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI de Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 Implementar una máquina virtual a partir de una imagen de máquina virtual de usuario
toodeploy una máquina virtual desde una imagen de máquina virtual de usuario, puede usar actual hello [portal de Azure](https://manage.windowsazure.com) o PowerShell.

**Implementar una máquina virtual desde el portal de Azure actual Hola**

1. Vaya demasiado**New** > **proceso** > **Máquina Virtual** > **de galería**.

    ![dibujo][img-manage-vm-new]
2. Vaya demasiado**Mis imágenes**, y, a continuación, seleccione Hola imagen de máquina virtual desde qué toodeploy una máquina virtual:

   1. Imagen de preste especial atención toowhich seleccione, porque hello **Mis imágenes** vista muestra imágenes de sistema operativo y de imágenes de máquina virtual.
   2. Examinando el número de Hola de discos puede ayudar a determinar qué tipo de imagen va a implementar, porque la mayoría de Hola de imágenes de máquina virtual tiene más de un disco. Sin embargo, es posible toohave una imagen de máquina virtual con solo un disco de sistema operativo único, que, a continuación, tendría **número de discos** establecer too1.

      ![dibujo][img-manage-vm-select]
3. Siga el Asistente para la creación de VM de Hola y especifique el nombre de la máquina virtual de hello, tamaño VM, ubicación, nombre de usuario y contraseña.

**Implementación de una máquina virtual a partir de PowerShell**

toodeploy que una máquina virtual grande de hello generalizar la imagen de máquina virtual que acaba de crear, puede usar Hola siguientes cmdlets.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Vea [Solución de problemas comunes que se encuentran durante la creación de VHD] para obtener más ayuda.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Obtención de la certificación para su imagen de máquina virtual
Hola siguiente paso en preparar la imagen VM para hello Azure Marketplace es toohave que cuando certificadas.

Este proceso incluye la ejecución de una herramienta de certificación especiales, cargar toohello de resultados de comprobación de hello Azure contenedor donde residen sus VHD, agregar una oferta, definir el SKU y enviando la máquina virtual de la imagen para la certificación.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 Descargue y ejecute hello herramienta Certification Test de Azure Certified
herramienta de certificación de Hola se ejecuta en una máquina virtual en ejecución, aprovisionada desde su imagen de máquina virtual de usuario, tooensure que Hola imagen de máquina virtual es compatible con Microsoft Azure. Comprobará que se han cumplido las instrucciones de Hola y requisitos sobre cómo preparar el disco duro virtual. salida de Hello de herramienta de hello es un informe de compatibilidad, que se debe cargar en hello Portal de publicación mientras se solicita la certificación.

herramienta de certificación de Hello puede usarse con máquinas virtuales de Linux y Windows. Se conecta a las máquinas virtuales de la basadas en tooWindows a través de PowerShell y se conecta tooLinux las máquinas virtuales a través de SSH.Net:

1. En primer lugar, descargar herramienta de certificación de hello en hello [sitio de descarga de Microsoft][link-msft-download].
2. Abrir herramienta de certificación de hello y, a continuación, haga clic en hello **Iniciar nueva prueba** botón.
3. De hello **probar información** pantalla, escriba un nombre para la ejecución de pruebas de Hola.
4. Especifique si la máquina virtual está basada en Linux o Windows. Dependiendo de cuál elegir, seleccione las opciones siguientes de Hola.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Conectar Hola certificación herramienta tooa imagen de VM de Linux**
1. Modo de autenticación de SSH seleccione hello: archivo de contraseña o clave.
2. Si utiliza la autenticación basada en contraseña, escriba el nombre de sistema de nombres de dominio (DNS) de hello, nombre de usuario y contraseña.
3. Si utiliza la autenticación de archivo de clave, escriba el nombre DNS de hello, el nombre de usuario y la ubicación de la clave privada.

   ![Autenticación de contraseña de imagen de máquina virtual de Linux][img-cert-vm-pswd-lnx]

   ![Autenticación de archivo de clave de máquina virtual de Linux][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Conectar la imagen de VM basadas en Windows de hello certificación herramienta tooa**
1. Escriba el nombre DNS de la máquina virtual de hello completo (por ejemplo, MyVMName.Cloudapp.net).
2. Escriba la contraseña y el nombre de usuario de Hola.

   ![Autenticación de contraseña de imagen de máquina virtual de Windows][img-cert-vm-pswd-win]

Después de haber seleccionado opciones correctas de hello para la imagen de Linux o máquinas virtuales basadas en Windows, seleccione **Probar conexión** tooensure que SSH.Net o PowerShell tiene una conexión válida con fines de prueba. Una vez establecida una conexión, seleccione **siguiente** prueba de hello toostart.

Una vez completada la prueba de hello, recibirá Hola resultados (paso/error/advertencia) para cada elemento de prueba.

![Casos de prueba para la imagen de máquina virtual de Linux][img-cert-vm-test-lnx]

![Casos de prueba para la imagen de máquina virtual de Windows][img-cert-vm-test-win]

Si alguna de las pruebas de hello no, no se clasifique la imagen. Si esto ocurre, revise los requisitos de Hola y realice los cambios necesarios.

Después de hello prueba automática, se le preguntará tooprovide una entrada adicional en la imagen de máquina virtual a través de una pantalla de cuestionario.  Complete preguntas de hello y, a continuación, seleccione **siguiente**.

![Cuestionario de la herramienta de certificación][img-cert-vm-questionnaire]

![Cuestionario de la herramienta de certificación][img-cert-vm-questionnaire-2]

Después de haber completado cuestionario hello, puede proporcionar información adicional, como información de acceso SSH para hello imagen de VM de Linux y una explicación para las evaluaciones error. Puede descargar los resultados de pruebas de Hola y archivos de registro de hello ejecutar casos de prueba en cuestionario toohello de suma tooyour respuestas. Guardar los resultados de Hola Hola mismo contenedor que los discos duros virtuales.

![Guardar resultados de la prueba de certificación][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 obtener el URI de la firma de acceso compartido Hola para las imágenes de máquina virtual
Durante el proceso de publicación de hello, especificar identificadores de uniforme de recursos (URI) de Hola que mejoren tooeach de hello discos duros virtuales que ha creado para el SKU. Microsoft necesita acceso toothese discos duros virtuales durante el proceso de certificación de Hola. Por lo tanto, necesitará toocreate un URI de firma de acceso compartido para cada disco duro virtual. Se trata de hello URI que se debe escribir en el **imágenes** ficha Hola Portal de publicación.

firma de acceso compartido de Hello URI creado debe respetar toohello según los requisitos:

* Para generar los URI de firma de acceso compartido para sus VHD, son suficientes los permisos de lista y lectura. No proporcione acceso de escritura o eliminación.
* duración de Hello para el acceso debe ser un mínimo de tres (3) semanas de cuando se crea el URI de la firma de acceso compartido Hola.
* toosafeguard en hora UTC, día Hola select antes de hello fecha actual. Por ejemplo, si Hola fecha actual es el 6 de octubre de 2014, seleccione 10/5/2014.

Dirección URL de SAS puede ser generado en tooshare de varias maneras el disco duro virtual de Azure Marketplace.
A continuación se Hola 3 herramientas recomendadas:

1.  Explorador de Azure Storage
2.  Explorador de almacenamiento de Microsoft
3.  CLI de Azure

**Explorador de Azure Storage (recomendado para los usuarios de Windows)**

Estos son los pasos de Hola para generar la dirección URL de SAS mediante el Explorador de almacenamiento de Azure

1. Descargue [Explorador de Azure Storage 6 versión preliminar 3](https://azurestorageexplorer.codeplex.com/) desde CodePlex. Vaya demasiado[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) y haga clic en **"Descarga"**.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Descargue [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) e instálelo después de la descompresión.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Después de instalarlo, abra la aplicación hello.
4. Haga clic en **Agregar cuenta**.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Especifique el nombre de cuenta de almacenamiento de hello, clave de la cuenta de almacenamiento y dominio de los puntos de conexión de almacenamiento. Esto es, cuenta de almacenamiento de hello en su suscripción de Azure donde ha guardado el disco duro virtual en el portal de Azure.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Una vez que se conecta a Azure Storage Explorer tooyour cuenta de almacenamiento específica, se iniciará mostrando todas hello contiene dentro de la cuenta de almacenamiento de Hola. Seleccionar contenedor Hola donde copió el archivo VHD de disco de sistema operativo hello (también discos de datos, si son aplicables para su escenario).

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Después de seleccionar el contenedor de blobs de hello, Azure Storage Explorer inicia mostrando archivos Hola contenedor Hola. Seleccione el archivo de imagen de hello (.vhd) que necesita toobe enviado.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Después de seleccionar el archivo .vhd de hello en el contenedor de hello, haga clic en hello **seguridad** ficha.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  Hola **seguridad del contenedor de Blob** cuadro de diálogo, los valores predeterminados de deje hello en hello **nivel de acceso** ficha y, a continuación, haga clic en **firmas de acceso compartido** ficha.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Siga los pasos de Hola por debajo de un URI de firma de acceso compartido para la imagen de VHD de Hola toogenerate:

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Permite el acceso:** toosafeguard en hora UTC, día Hola select antes de hello fecha actual. Por ejemplo, si Hola fecha actual es el 6 de octubre de 2014, seleccione 10/5/2014.

    b. **Permite el acceso a:** seleccione una fecha que sea al menos 3 semanas después de hello **permite el acceso** fecha.

    c. **Acciones permitidas:** Hola seleccione **lista** y **lectura** permisos.

    d. Si ha seleccionado el archivo .vhd correctamente, el archivo aparece en **tooaccess de nombre de Blob** con extensión .vhd.

    e. Haga clic en **Generar firma**.

    f. En **genera compartido acceso firma URI de este contenedor**, busque Hola siguientes como se indica anteriormente:

       - Asegúrese de que el nombre de archivo de la imagen y **".vhd"** están en hello URI.
       - Al final de Hola de firma de hello, asegúrese de que **"= rl"** aparece. Esto demuestra que el acceso de lectura y lista se ha proporcionado correctamente.
       - En el centro de firma de hello, asegúrese de que **"sr = c"** aparece. Esto demuestra que tiene acceso de nivel de contenedor.

11. tooensure Hola genera compartidos funciona URI de firma de acceso, haga clic en **pruebas en explorador**. Debe iniciar el proceso de descarga de Hola.

12. Copie el URI de la firma de acceso compartido Hola. Se trata de hello URI toopaste en hello Portal de publicación.

13. Repita los pasos 6 y 10 para cada disco duro virtual en hello SKU.

**Explorador de Microsoft Azure Storage (Windows/MAC/Linux)**

Estos son los pasos de Hola para generar la dirección URL de SAS mediante el Explorador de almacenamiento de Microsoft Azure

1.  Descargue el Explorador de Microsoft Azure Storage desde el sitio web [http://storageexplorer.com/](http://storageexplorer.com/). Vaya demasiado[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) y haga clic en **"Descargar para Windows"**.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Después de instalarlo, abra la aplicación hello.

3.  Haga clic en **Agregar cuenta**.

4.  Configurar suscripción de Microsoft Azure Storage Explorer tooyour tooyour cuenta de inicio de sesión

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Vaya toostorage cuenta y seleccione Hola contenedor

6.  Seleccione **"Get Share Access Signature"** (Obtener la firma de acceso compartido) con un clic derecho de hello **contenedor**

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Actualice la hora de inicio, la hora de expiración y los permisos según se especifica a continuación:

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Hora de inicio:** toosafeguard en hora UTC, día Hola select antes de hello fecha actual. Por ejemplo, si Hola fecha actual es el 6 de octubre de 2014, seleccione 10/5/2014.

    b.  **La hora de expiración:** seleccione una fecha que sea al menos 3 semanas después de hello **Start Time** fecha.

    c.  **Permisos:** Hola seleccione **lista** y **lectura** permisos

8.  Copie el URI de la firma de acceso compartido del contenedor.

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    Dirección URL de SAS generada es de nivel de contenedor y ahora necesitamos tooadd nombre del VHD en ella.

    Formato de la dirección URL de SAS de nivel de contenedor:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Inserte el nombre de disco duro virtual después de nombre de contenedor de hello en dirección URL de SAS como a continuación`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Ejemplo:

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd es hello nombre de disco duro virtual, será la dirección URL de SAS del disco duro virtual`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Asegúrese de que el nombre de archivo de la imagen y **".vhd"** están en hello URI.
    - En el centro de firma de hello, asegúrese de que **"sp = rl"** aparece. Esto demuestra que el acceso de lectura y lista se ha proporcionado correctamente.
    - En el centro de firma de hello, asegúrese de que **"sr = c"** aparece. Esto demuestra que tiene acceso de nivel de contenedor.

9.  tooensure que Hola funciona URI de firma de acceso compartido generada, probarlo en el explorador. Debe iniciar el proceso de descarga de Hola

10. Copie el URI de la firma de acceso compartido Hola. Se trata de hello URI toopaste en hello Portal de publicación.

11. Repita estos pasos para cada disco duro virtual en hello SKU.

**CLI de Azure (recomendado para la integración continua y distinta de Windows)**

Estos son los pasos de Hola para generar la dirección URL de SAS mediante CLI de Azure

1.  Descargue la CLI de Microsoft Azure desde [aquí](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). También puede encontrar vínculos diferentes para **[Windows](http://aka.ms/webpi-azure-cli)** y **[MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Una vez completada la descarga, instálela.

3.  Cree un archivo de PowerShell con el código siguiente y guárdelo en local.

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Actualizar siguiente Hola parámetros en anteriormente

    a. **`<StorageAccountName>`**: indique el nombre de la cuenta de almacenamiento

    b. **`<Storage Account Key>`**: indique la clave de la cuenta de almacenamiento

    c. **`<Permission Start Date>`**: toosafeguard en hora UTC, día Hola select antes de hello fecha actual. Por ejemplo, si hello fecha actual es el 26 de octubre de 2016, entonces debe ser el valor 10/25/2016

    d. **`<Permission End Date>`**: Seleccione una fecha que sea al menos 3 semanas después de hello **Start Date**. Así, el valor debería ser **11/02/2016**.

    Siguiente es un código de ejemplo de Hola después de actualizar los parámetros adecuados

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Abra el editor de Powershell con el modo de "Ejecutar como administrador" y abra el archivo del paso 3.

5.  Secuencia de comandos de ejecución hello y proporcionará que Hola URL de SAS para el acceso de nivel de contenedor

    Estos son resultado de hello de parte de hello resaltado de hello firma de SAS y copia en el Bloc de notas

    ![dibujo](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Ahora obtendrá la dirección URL de SAS de nivel de contenedor y deberá tooadd nombre del VHD en ella.

    N.º de URL de SAS de nivel de contenedor

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Inserte el nombre de disco duro virtual después de nombre de contenedor de hello en dirección URL de SAS tal y como se muestra a continuación`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Ejemplo:

    TestRGVM201631920152.vhd es hello nombre de disco duro virtual, será la dirección URL de SAS del disco duro virtual

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Asegúrese de que el nombre de archivo de imagen y ".vhd" están en hello URI.
    -   En el centro de firma de hello, compruebe que aparece "sp = rl". Esto demuestra que el acceso de lectura y lista se ha proporcionado correctamente.
    -   En el centro de firma de hello, asegúrese de que "sr = c" aparece. Esto demuestra que tiene acceso de nivel de contenedor.

8.  tooensure que Hola funciona URI de firma de acceso compartido generada, probarlo en el explorador. Debe iniciar el proceso de descarga de Hola

9.  Copie el URI de la firma de acceso compartido Hola. Se trata de hello URI toopaste en hello Portal de publicación.

10. Repita estos pasos para cada disco duro virtual en hello SKU.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 proporcionan información acerca de la imagen de máquina virtual de Hola y solicitar la certificación en hello Portal de publicación
Una vez haya creado la oferta y SKU, debe especificar detalles de la imagen de hello asociados a esa SKU:

1. Vaya toohello [Portal de publicación][link-pubportal]y, a continuación, inicie sesión con tu cuenta de vendedor.
2. Seleccione hello **imágenes de máquina virtual** ficha.
3. identificador de Hello aparece al principio de Hola de página de hello es realmente identificador de oferta de hello y no el identificador SKU Hola.
4. Rellene las propiedades de hello en hello **SKU** sección.
5. En **familia del sistema operativo**, haga clic en el tipo de sistema operativo de hello asociado Hola VHD del sistema operativo.
6. Hola **sistema operativo** cuadro, describa el sistema operativo de Hola. Considere un formato como familia de sistemas operativos, tipo, versión y actualizaciones. Por ejemplo, "Windows Server Datacenter 2014 R2".
7. Seleccione seguridad toosix recomendada tamaños de máquina virtual. Estas son las recomendaciones que obtener del cliente de toohello mostrada en la hoja de nivel de precios de Hola Hola Portal de Azure al decidir toopurchase e implementar la imagen. **Se trata únicamente de recomendaciones. el cliente de Hello es capaz de tooselect cualquier tamaño de máquina virtual que dé cabida a discos de hello especificado en la imagen.**
8. Escriba la versión de Hola. campo de la versión de Hola encapsula una versión semántica tooidentify hello y las actualizaciones:
   * Versiones deben tener formato de hello X.Y.Z, donde X, Y y Z son números enteros.
   * Imágenes de SKU diferentes pueden tener distintas versiones principales y secundarias.
   * Las versiones en una SKU sólo deberían ser los cambios incrementales que aumentar la versión de revisión de hello (Z desde X.Y.Z).
9. Hola **dirección URL del VHD OS** cuadro, escriba la firma de acceso compartido de hello URI creado para hello VHD del sistema operativo.
10. Si no hay discos de datos asociados a esta SKU, seleccione hello toowhich del (LUN) número de unidad lógica que desea que este toobe de disco de datos montado durante la implementación.
11. Hola **dirección URL del VHD de LUN X** cuadro, escriba la firma de acceso compartido de hello identificador URI creado para los datos de hello primer disco duro virtual.

    ![dibujo](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Problemas y soluciones comunes de la dirección URL de SAS

|Problema|Mensaje de error|Solución|Vínculo a documentación|
|---|---|---|---|
|Error al copiar imágenes: "?" no se encuentra en la dirección URL de SAS|Error al copiar imágenes No se puede toodownload blob mediante proporciona el Uri de SAS.|Actualización Hola Url de SAS mediante herramientas recomendadas|[https://azure.microsoft.com/es-es/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Error al copiar imágenes: los parámetros "st" y "se" no están en la dirección URL de SAS|Error al copiar imágenes No se puede toodownload blob mediante proporciona el Uri de SAS.|Actualizar Hola Url de SAS con fechas de inicio y finalización en él|[https://azure.microsoft.com/es-es/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Error al copiar imágenes: "sp=rl" no está en la dirección URL de SAS|Error al copiar imágenes No se puede toodownload blob mediante proporciona el Uri de SAS|Actualizar Hola Url de SAS con permisos establecidos como "Lectura" y "lista|[https://azure.microsoft.com/es-es/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Error al copiar imágenes: la dirección URL de SAS tiene espacios en blanco en el nombre de disco duro virtual.|Error al copiar imágenes No se puede toodownload blob mediante proporciona el Uri de SAS.|Actualizar Hola Url de SAS, sin espacios en blanco|[https://azure.microsoft.com/es-es/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Error al copiar imágenes: error de autorización de dirección Url de SAS|Error al copiar imágenes Blob no se puede toodownload debido a error de tooauthorization|Volver a generar Hola Url de SAS|[https://azure.microsoft.com/es-es/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Paso siguiente
Cuando termine con detalles SKU de hello, puede mover hacia delante toohello [Guía de contenido de marketing de Azure Marketplace][link-pushstaging]. En este paso del proceso de publicación de hello, proporcionar Hola marketing contenido, precios y otros antes es necesario obtener información demasiado**paso 3: probar la máquina virtual ofrecen en almacenamiento provisional**, en el que probar varios escenarios de casos de uso antes de implementar Hola oferta toohello Azure Marketplace para la compra y visibilidad pública.  

## <a name="see-also"></a>Otras referencias
* [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
