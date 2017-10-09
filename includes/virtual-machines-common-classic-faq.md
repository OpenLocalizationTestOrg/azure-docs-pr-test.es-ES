


En este artículo se trata algunas preguntas comunes usuarios Preguntarme Azure máquinas virtuales creadas con el modelo de implementación clásica de Hola.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>¿Puedo migrar mi VM que se crean en hello implementación clásica modelo toohello nuevo administrador de recursos modelo?
Sí. Para obtener instrucciones sobre cómo toomigrate, consulte:

* [Migrar desde tooAzure clásico Administrador de recursos del uso de Azure PowerShell](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Migrar desde tooAzure clásico Administrador de recursos mediante Azure CLI](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>¿Qué puedo ejecutar en una máquina virtual de Azure?
Todos los suscriptores pueden ejecutar software de servidor en una máquina virtual de Azure. Puede ejecutar versiones recientes de Windows Server, así como varias distribuciones de Linux. Para obtener más información de soporte técnico, consulte:

• Para máquinas virtuales de Windows: [soporte de software del servidor de Microsoft para Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Para máquinas virtuales de Linux: [Linux en distribuciones aprobadas por Azure](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Para las imágenes de cliente de Windows, determinadas versiones de Windows 7 y Windows 8.1 están disponibles tooMSDN Azure benefit y suscriptores a los suscriptores de MSDN desarrollo y prueba de pago por uso para las tareas de desarrollo y pruebas. Para obtener más información, como instrucciones y limitaciones, consulte [Imágenes de cliente de Windows para los suscriptores de MSDN](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).

## <a name="why-are-affinity-groups-being-deprecated"></a>¿Por qué se han dejado de usar los grupos de afinidad?
Los grupos de afinidad son un concepto heredado que hace referencia a la agrupación geográfica de las implementaciones de servicios en la nube y las cuentas de almacenamiento de un cliente en Azure. Rendimiento de red de VM a la máquina virtual tooimprove en diseños de red de Azure temprano Hola hubieran sido proporcionados originariamente. También admite la versión inicial de Hola de redes virtuales (redes virtuales), que son tooa limitado pequeño conjunto de hardware en una región.

red de Azure actual Hola dentro de una región está diseñado para que los grupos de afinidad ya no son necesarios. Las redes virtuales también se encuentran en el ámbito regional y, por tanto, ya no es necesario usar un grupo de afinidad. Debido a mejoras toothese, ya no recomendamos que los clientes usan grupos de afinidad porque puede limitar en algunos escenarios. Uso de grupos de afinidad innecesariamente asociará el hardware de toospecific de las máquinas virtuales que limita la elección de Hola de tamaños de máquinas virtuales que están disponible tooyou. También podría provocar errores relacionados con el toocapacity cuando intente tooadd nuevas máquinas virtuales si el hardware específico de hello asociados con el grupo de afinidad de hello esté cerca de la capacidad.

Características de grupo de afinidad ya están en desuso en el modelo de implementación de Azure Resource Manager Hola y Hola portal de Azure. Para el portal de Azure clásico de hello, nos estamos dejando de compatibilidad para crear grupos de afinidad y creación de recursos de almacenamiento que están anclados tooan grupo de afinidad. No es necesario toomodify existente servicios en la nube que están usando un grupo de afinidad. los grupos de afinidad no deben usarse en los nuevos servicios en la nube, a menos que lo recomiende uno de los profesionales de soporte técnico de Azure.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>¿Cuánto almacenamiento puedo usar con una máquina virtual?
Cada disco de datos puede ser hasta too1 TB. número de Hola de discos de datos que puede usar depende de tamaño de Hola de máquina virtual de Hola. Para obtener más información, consulte [Tamaños de máquinas virtuales](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Una cuenta de almacenamiento de Azure proporciona almacenamiento para el disco del sistema operativo de Hola y los discos de datos. Cada disco es un archivo .vhd almacenado como un blob en páginas. Para obtener información detallada sobre los precios, consulte [Detalles de precios de almacenamiento](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>¿Qué tipos de disco duro virtual se puede usar?
Azure solo admite discos duros virtuales fijos con formato VHD. Si tiene un VHDX que desea toouse en Azure, necesita toofirst convertir mediante el Administrador de Hyper-V o hello [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet. Después de hacerlo, use [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) Hola de cmdlet (en modo de administración de servicios) tooupload cuenta de almacenamiento de tooa de disco duro virtual en Azure, por lo que puede usar con máquinas virtuales.

* Para obtener instrucciones de Linux, consulte [crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Para obtener instrucciones de Windows, consulte [crear y cargar un VHD de Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>¿Son que estas máquinas virtuales Hola igual que las máquinas virtuales de Hyper-V?
En muchos aspectos que son similares máquinas virtuales de Hyper-V de "Generación 1", pero no exactamente está Hola mismo. Ambos tipos proporcionan hardware virtualizado y los discos duros con formato VHD virtuales Hola son compatibles. Esto significa que puede moverlos entre Hyper-V y Azure. Tres diferencias claves que a veces sorprenden a los usuarios de Hyper-V son:

* Azure no proporciona la máquina virtual de consola acceso tooa. No hay ningún tooaccess forma una máquina virtual hasta que termine arranque.
* Las máquinas virtuales de Azure de la mayoría de [tamaños](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) solo tienen un adaptador de red virtual, lo que significa que solo pueden tener una dirección IP externa. (Hola A8 y A9 tamaños emplean un segundo adaptador de red para la comunicación de aplicaciones entre instancias en escenarios limitados).
* Las máquinas virtuales de Azure no admiten funciones de máquina virtual de Hyper-V de generación 2. Para más información sobre estas características, consulte [Especificaciones de máquina virtual para Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) e [Introducción a las máquinas virtuales de generación 2](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>¿Pueden estas máquinas virtuales usar mi infraestructura de red local existente?
Para las máquinas virtuales creadas en el modelo de implementación clásica de hello, puede utilizar la infraestructura existente de tooextend de red Virtual de Azure. enfoque de Hello es como si configurara una sucursal. Se puede aprovisionar y administrar redes privadas virtuales (VPN) en Azure, así como conectarse de forma segura ellos tooon local infraestructura de TI. Para obtener más información, consulte [Información general de la red virtual](../articles/virtual-network/virtual-networks-overview.md).

Necesitará toospecify red de Hola que desee Hola toowhen toobelong de máquina virtual se crea la máquina virtual de Hola. No puede unirse a una red virtual de tooa de máquina virtual existente. Sin embargo, puede solucionarlo desconectando Hola disco virtual (VHD) de la máquina virtual existente de hello y, a continuación, utilizarlo toocreate una nueva máquina virtual con configuración de red de Hola que desee.

## <a name="how-can-i-access--my-virtual-machine"></a>¿Cómo puedo acceder a mi máquina virtual?
Debe tooestablish una toolog de conexión remota en la máquina virtual de toohello mediante conexión a Escritorio remoto para una VM de Windows o un Shell seguro (SSH) para una VM de Linux. Para obtener instrucciones, consulte:

* [¿Cómo tooLog en tooa Máquina Virtual que ejecuta Windows Server](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Se admite un máximo de 2 conexiones simultáneas, a menos que el servidor de hello está configurado como un host de sesión de servicios de escritorio remoto.  
* [¿Cómo tooLog en la máquina Virtual que ejecuta Linux tooa](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). De forma predeterminada, SSH permite un máximo de 10 conexiones simultáneas. Puede aumentar este número editando el archivo de configuración de Hola.

Si tiene problemas con Escritorio remoto o SSH, instalar y usar hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extensión toohelp corregir Hola problema.

En las máquinas virtuales de Windows, entre las opciones adicionales se incluyen:

* En Hola portal de Azure clásico, encontrar Hola VM y luego haga clic en **restablecer el acceso remoto** de barra de comandos de Hola.
* Revisión [tooa de conexiones de escritorio remoto solucionar problemas de máquina Virtual de Azure basado en Windows](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Usar acceso remoto a Windows PowerShell tooconnect toohello VM, o crear extremos adicionales en otro toohello de tooconnect recursos máquina virtual. Para obtener más información, consulte [cómo tooSet extremos tooa Máquina Virtual](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Si está familiarizado con Hyper-V, puede que esté buscando un tooVMConnect similar de la herramienta. Azure no ofrece una herramienta similar porque no se admite la máquina virtual de consola acceso tooa.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>¿Puedo usar datos de toostore de hello disco temporal (Hola unidad D: para Windows o/dev/sdb1 para Linux)?
No debe usar datos de toostore de hello disco temporal (Hola unidad D: de forma predeterminada para Windows o/dev/sdb1 para Linux). Estos discos solamente proporcionan almacenamiento de forma temporal, por lo que se arriesgaría a perder datos que no se pueden recuperar. Esto puede ocurrir cuando se mueve de máquina virtual de hello tooa otro host. Cambiar el tamaño de una máquina virtual, actualizar host hello, o un error de hardware en el host de hello es algunos de los motivos de hello que puede mover una máquina virtual.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>¿Cómo se puede cambiar la letra de unidad de Hola de disco temporal de hello?
En una máquina virtual de Windows, puede cambiar la letra de unidad de hello al mover el archivo de página hello y reasignar letras de unidad, pero necesitará toomake seguro que Hola pasos en un orden específico. Para obtener instrucciones, consulte [cambiar la letra de unidad Hola de disco temporal de Windows hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>¿Cómo se puede actualizar el sistema operativo de hello?
Hello actualización término generalmente significa tooa móvil más reciente versión del sistema operativo, mientras permanece en Hola mismo hardware. Para las máquinas virtuales de Azure, Hola proceso para mover tooa difiere de la versión más reciente para Windows y Linux:

* Para máquinas virtuales de Linux, use herramientas de administración de paquetes de saludo y los procedimientos adecuados para la distribución de Hola.
* Para una máquina virtual de Windows, necesita toomigrate Hola servidor con algo parecido a Hola herramientas de migración de Windows Server. No intente a SO invitado de Hola de tooupgrade mientras reside en Azure. No se admite debido a riesgo de Hola de perder la máquina virtual de toohello de acceso. Si se producen problemas durante la actualización de hello, podría perder Hola capacidad toostart un escritorio remoto sesión y podría no es capaz de tootroubleshoot problemas de Hola.

Para obtener más información general sobre las herramientas de Hola y procesos para migrar un servidor de Windows, vea [tooWindows migrar Roles y características de servidor](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>¿Cuál es el nombre de usuario predeterminado de hello y una contraseña en la máquina virtual de hello?
imágenes de Hello proporcionadas por Azure no tienen un nombre de usuario configuradas previamente y una contraseña. Cuando se crea la máquina virtual mediante una de esas imágenes, deberá tooprovide un nombre de usuario y la contraseña que se va a utilizar toolog en la máquina virtual de toohello.

Si ha olvidado el nombre de usuario de Hola o la contraseña y ha instalado Hola agente de máquina virtual, puede instalar y usar hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problema con hello toofix la extensión.

Detalles adicionales:

* Para las imágenes de Linux de hello, si usas Hola portal de Azure clásico, 'azureuser' se proporciona como un nombre de usuario de manera predeterminada, pero puede cambiarlo mediante 'de la Galería"en lugar de"Creación rápida"como máquina virtual de hello forma toocreate Hola. El uso "De la Galería" también le permite decidir si toouse una contraseña, una clave SSH o ambas toolog en. Hola cuenta de usuario es un usuario sin privilegios que tiene acceso de "sudo" toorun privilegiado de comandos. Hola 'raíz' cuenta está deshabilitada.
* Para las imágenes de Windows, necesitará tooprovide un nombre de usuario y una contraseña al crear Hola máquina virtual. cuenta de Hello se agrega el grupo de administradores de toohello.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>¿Puede Azure ejecutar antivirus en las máquinas virtuales?
Azure ofrece varias opciones para las soluciones antivirus, pero depende tooyou toomanage. Por ejemplo, podría necesitar una suscripción independiente para software antimalware y necesitará toodecide al toorun examina e instalar las actualizaciones. Puede agregar soporte antivirus con una extensión de máquina virtual de Microsoft Antimalware, Symantec Endpoint Protection o TrendMicro Deep Security Agent al crear una máquina virtual de Windows o en un momento posterior. Hola Symantec y TrendMicro extensiones permiten utilizar una suscripción de prueba gratuita de tiempo limitado o una enterprise subscription existente. Microsoft Antimalware es gratuito. Para obtener información, consulte:

* [¿Cómo tooinstall y configurar Symantec Endpoint Protection en una VM de Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [¿Cómo tooinstall y configurar trendmicro Deep Security como un servicio en una máquina virtual de Azure](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Implementación de soluciones antimalware en Azure Virtual Machines](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>¿Qué opciones tengo para la copia de seguridad y la recuperación?
Azure Backup está disponible como una vista previa en determinadas regiones. Para obtener más información, consulte [Copia de seguridad de máquinas virtuales de Azure](../articles/backup/backup-azure-vms.md). Hay otras soluciones disponibles de socios certificados. toofind cuál es actualmente disponible, busque hello Azure Marketplace.

Otra opción es funciones de instantánea de hello toouse del almacenamiento de blobs. toodo esto, necesitará tooshut hacia abajo Hola VM antes de cualquier operación que requiera una instantánea de blob. Esto ahorra las escrituras de datos y coloca el sistema de archivos de hello en un estado coherente.

## <a name="how-does-azure-charge-for-my-vm"></a>¿Cómo cobra Azure mi máquina virtual?
Azure cobra un precio por hora según el tamaño y el sistema operativo de la máquina virtual de Hola. Para las fracciones de hora, Azure cargos por solo de minutos de Hola de uso. Si creas Hola VM con una imagen de máquina virtual que contiene determinado software preinstalado, pueden aplicar cargos adicionales de software por hora. Azure cobra por separado el almacenamiento para los discos de datos y sistema operativo de la máquina virtual de Hola. El almacenamiento en disco temporal es gratuito.

Se le cobrará cuando Hola estado de la VM sea en ejecución o detenido, pero no se le cobrará cuando Hola estado de la máquina virtual se ha detenido (desasignado). tooput una máquina virtual en hello había detenido (desasignado) de estado, siga uno de los procedimientos de hello:

* Apague o elimine Hola VM de hello portal de Azure clásico.
* Utilice cmdlet Stop-AzureVM hello, disponible en el módulo de PowerShell de Azure Hola.
* Usar operación de cerrar rol Hola Hola API de REST de administración de servicios y especifique StoppedDeallocated para el elemento PostShutdownAction de Hola.

Para obtener más información, consulte [Precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>¿Reiniciará Azure mi máquina virtual para efectuar tareas de mantenimiento?
A veces, Azure reinicia la máquina virtual como parte de las actualizaciones de mantenimiento regular, no planeada en hello centros de datos de Azure.

Es posible que se produzcan eventos de mantenimiento no planeados cuando Azure detecte un problema grave de hardware que afecte a la máquina virtual. Para los eventos no planeados, Azure automáticamente migra Hola VM tooa correcto host y reinicia Hola máquina virtual.

Para cualquier máquina virtual independiente (es decir, Hola VM no forma parte de un conjunto de disponibilidad), Azure notifica al administrador de servicios de la suscripción de Hola por correo electrónico al menos una semana antes del mantenimiento planeado porque Hola máquinas virtuales podría reiniciarse durante la actualización de Hola. Aplicaciones que se ejecutan en máquinas virtuales de hello pudieron experimentar un tiempo de inactividad.

También puede utilizar Hola portal de Azure clásico o registros de Azure PowerShell tooview Hola reinicio cuando se ha producido un reinicio de hello debido a mantenimiento tooplanned. Para obtener más información, consulte [Visualización de registros de reinicio de máquina virtual](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

redundancia de tooprovide, coloque dos o más del mismo modo configurado máquinas virtuales en hello mismo conjunto de disponibilidad. Esto ayuda a asegurarse de que haya al menos una máquina virtual esté disponible durante el mantenimiento, sea este planeado o no. Azure garantiza determinados niveles de disponibilidad de la máquina virtual para esta configuración. Para obtener más información, consulte [administrar Hola disponibilidad de máquinas virtuales](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Recursos adicionales
[Acerca de Azure Virtual Machines](../articles/virtual-machines/virtual-machines-linux-about.md)

[Crear y administrar máquinas virtuales de Linux con Hola CLI de Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Creación y administración de máquinas virtuales Windows con el módulo de Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

