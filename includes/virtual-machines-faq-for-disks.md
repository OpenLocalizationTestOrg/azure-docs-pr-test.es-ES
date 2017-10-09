# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Preguntas más frecuentes sobre los discos de máquina virtual de IaaS de Azure y los discos premium administrados y no administrados

En este artículo se responden algunas de las preguntas más frecuentes acerca de Azure Managed Disks y Azure Premium Storage.

## <a name="managed-disks"></a>Managed Disks

**¿Qué es Azure Managed Disks?**

Managed Disks es una característica que simplifica la administración de discos para máquinas virtuales de IaaS de Azure al controlar automáticamente la administración de la cuenta de almacenamiento. Para obtener más información, vea hello [información general de discos administrados](../articles/virtual-machines/windows/managed-disks-overview.md).

**Si creo un disco administrado estándar a partir un disco duro virtual existente con 80 GB de tamaño, ¿cuánto me costará?**

Un disco administrado estándar creado a partir de un VHD de 80 GB se trata como el tamaño de disco estándar disponible siguiente hello, que es un disco S10. Se le cobrará correspondiente toohello S10 disco precios. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).

**¿Existen costes de transacción para los discos administrados estándar?**

Sí. Sí, se le cobrará por cada transacción. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).

**¿Para un disco administrado estándar, se me cobrarán de tamaño real de Hola de datos de hello en el disco de Hola o de hello aprovisionar capacidad de hello disco?**

Se le cobrará en función de la capacidad de hello aprovisionado del disco de Hola. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).

**¿En qué se diferencian los precios de los discos administrados premium de los de los discos no administrados?**

Hola precios de discos premium administrado es Hola igual que los discos premium no administrado.

**¿Puedo cambiar Hola almacenamiento tipo de cuenta (Standard o Premium) de Mis discos administrados?**

Sí. Puede cambiar el tipo de cuenta de almacenamiento de Hola de los discos administrados mediante Hola portal de Azure, PowerShell u Hola CLI de Azure.

**¿Hay alguna manera que puedo copiar o exportar una cuenta de almacenamiento privado de disco administrado tooa?**

Sí. Puede exportar los discos administrados mediante Hola portal de Azure, PowerShell u Hola CLI de Azure.

**¿Puedo usar un archivo de disco duro virtual en un toocreate de cuenta de almacenamiento de Azure un disco administrado con una suscripción diferente?**

No.

**¿Puedo usar un archivo de disco duro virtual en un toocreate de cuenta de almacenamiento de Azure un disco administrado en una región distinta?**

No.

**¿Hay alguna limitación de escala para los clientes que usen discos administrados?**

Discos administrados elimina los límites de hello asociados con las cuentas de almacenamiento. Sin embargo, el número de Hola de discos administrados por suscripción es limitado too2, 000 de forma predeterminada. Puede llamar a tooincrease de compatibilidad con este número.

**¿Puedo tomar una instantánea incremental de un disco administrado?**

No. capacidad de Hello corriente instantánea realiza una copia completa de un disco administrado. Sin embargo, tenemos previsto toosupport instantáneas incrementales en hello futuras.

**¿Pueden las máquinas virtuales de un conjunto de disponibilidad estar compuestas de una combinación de discos administrados y no administrados?**

No. Hola máquinas virtuales en un conjunto de disponibilidad debe usar discos todo administrados o todos los discos no administrados. Cuando se crea un conjunto de disponibilidad, puede elegir qué tipo de discos que desea toouse.

**¿Está opción predeterminada de discos administrados Hola Hola portal de Azure?**

No actualmente, pero dejará de estar predeterminado Hola Hola futuras.

**¿Puedo crear un disco administrado vacío?**

Sí. Puede crear un disco vacío. Un disco administrado puede crearse independientemente de una máquina virtual, por ejemplo, sin asociar tooa máquina virtual.

**¿Qué es el número de dominios de error de hello compatibles para un conjunto de disponibilidad que utiliza discos administrados?**

Función de la región Hola donde se encuentra conjunto de disponibilidad de Hola que utiliza discos administrados, número de dominios de error de hello admitida es 2 ó 3.

**¿Es la cuenta de almacenamiento estándar de Hola para diagnósticos configurar?**

Se configura una cuenta de almacenamiento privada para el diagnóstico de máquinas virtuales. Hola futura, tenemos previsto tooswitch diagnósticos tooManaged discos también.

**¿Qué tipo de compatibilidad con el Control de acceso basado en roles está disponible para Managed Disks?**

Managed Disks admite tres roles predeterminados fundamentales:

* Propietario: puede administrar todo, incluido el acceso.
* Colaborador: puede administrar todo, excepto el acceso.
* Lector: puede ver todo, pero no realizar cambios.

**¿Hay alguna manera que puedo copiar o exportar una cuenta de almacenamiento privado de disco administrado tooa?**

Puede obtener una firma de acceso compartido de solo lectura URI para hello administrado en disco y usarlo toocopy Hola contenido tooa almacenamiento privado local o cuenta de almacenamiento.

**¿Puedo crear una copia de mi disco administrado?**

Los clientes pueden crear una instantánea de sus discos administrados y, a continuación, usar Hola instantánea toocreate otro disco administrado.

**¿Siguen siendo compatibles los discos no administrados?**

Sí. Admitimos discos administrados y no administrados. Se recomienda que utilice discos administrados para nuevas cargas de trabajo y migrar los discos de toomanaged de las cargas de trabajo actual.


**¿Si crear un disco de 128 GB y, a continuación, aumentar Hola tamaño too130 GB, se me cobrarán para el tamaño de disco siguiente hello (512 GB)?**

Sí.

**¿Puedo crear discos administrados para el almacenamiento con redundancia local, almacenamiento con redundancia geográfica y almacenamiento con redundancia de zona?**

Actualmente, Azure Managed Disks solo admite discos administrados de almacenamiento con redundancia local.

**¿Puedo reducir mis discos administrados?**

No. En la actualidad no se admite esta característica. 

**¿Puedo cambiar propiedad de nombre de equipo de hello cuando especializada (no creados mediante la herramienta de preparación del sistema de Hola o generalizado) operativo disco del sistema es tooprovision usa una máquina virtual?**

No. No se puede actualizar la propiedad de nombre de equipo de Hola. Hello nueva máquina virtual hereda, de hello primario VM, que era el disco del sistema operativo utilizado toocreate Hola. 

**¿Dónde puedo encontrar toocreate de plantillas de Azure Resource Manager muestra las máquinas virtuales con discos administrados?**
* [Lista de plantillas mediante discos administrados](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Managed Disks y Storage Service Encryption 

**¿Está habilitado el servicio Storage Service Encryption de forma predeterminada al crear un disco administrado?**

Sí.

**¿Que administra las claves de cifrado de hello?**

Microsoft administra las claves de cifrado de Hola.

**¿Puedo deshabilitar Storage Service Encryption para Managed Disks?**

No.

**¿Storage Service Encryption está solo disponible en determinadas regiones?**

No. Está disponible en todas las regiones de Hola donde hay discos administrados. Managed Disks está disponible en todas las regiones públicas y Alemania.

**¿Cómo averiguo si mi disco administrado está cifrado?**

Puede averiguar el tiempo de hello cuando se creó un disco administrado de hello portal de Azure, hello Azure CLI y PowerShell. Si es hora de hello después del 9 de junio de 2017, se cifra el disco. 

**¿Cómo puedo cifrar mis discos existentes que se crearon antes del 10 de junio de 2017?**

A partir del 10 de junio de 2017 escritos tooexisting administrar discos nuevos datos se cifran automáticamente. También planeamos tooencrypt los datos existentes y cifrado de Hola se realizará de forma asincrónica en segundo plano de Hola. Si debe cifrar ahora los datos existentes, cree una copia del disco. Los discos nuevos se cifrarán.

* [Copiar discos administrados mediante Hola CLI de Azure](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [Copia de discos administrados mediante PowerShell](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

**¿Están cifradas las imágenes e instantáneas administradas?**

Sí. Todas las instantáneas e imágenes administradas creadas después del 9 de junio de 2017 se cifran automáticamente. 

**¿Puedo convertir máquinas virtuales con discos no administrados que se encuentran en las cuentas de almacenamiento que son o fueran discos toomanaged cifrados anteriormente?**

Sí

**¿Se cifrará también un VHD exportado de un disco administrado o de una instantánea?**

No. Pero si se exporta un disco duro virtual tooan cifra cuenta de almacenamiento de un disco administrado cifrado o una instantánea, a continuación, se cifra. 

## <a name="premium-disks-managed-and-unmanaged"></a>Discos premium: tanto administrados como no administrados

**Si una máquina virtual usa una serie de tamaño que admite Premium Storage, como DSv2, ¿puedo conectar discos de datos tanto premium como estándar?** 

Sí.

**¿Puedo conectar premium y series de tamaño de tooa de discos de datos estándar que no es compatible con almacenamiento Premium, por ejemplo, la serie D, Dv2, G o F?**

No. Puede adjuntar solo tooVMs de discos de datos estándar que no usan una serie de tamaño que admite el almacenamiento Premium.

**Si creo un disco de datos premium a partir un disco duro virtual existente con 80 GB, ¿cuánto me costará?**

Un disco de datos premium, creado a partir de un VHD de 80 GB se trata como el tamaño del disco premium disponibles para el siguiente hello, que es un disco P10. Se le cobrará correspondiente toohello P10 disco precios.

**¿Hay toouse de costos de transacción almacenamiento Premium?**

Existe un costo fijo para cada tamaño de disco que esté aprovisionado con límites específicos de IOPS y rendimiento. Hello otros costes son ancho de banda saliente y la capacidad de instantánea, si procede. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/storage).

**¿Cuáles son los límites de Hola para IOPS y el rendimiento que puedo recibo de caché de disco de hello?**

Hola combinados límites de memoria caché y SSD local para una serie DS son 4.000 IOPS por núcleo y 33 MB por segundo por núcleo. Hola serie GS ofrece 5.000 e/s por segundo por núcleo y 50 MB por segundo por núcleo.

**¿Es hello que SSD local compatibles para una máquina virtual administrado discos?**

Hello SSD local es el almacenamiento temporal que se incluye con una máquina virtual administrada de discos. No existe ningún costo extra para este almacenamiento temporal. Se recomienda que no utilice este toostore SSD local los datos de la aplicación porque no se conservan en almacenamiento de blobs de Azure.

**¿Se produce las repercusiones de hello usar de RECORTE en discos premium?**

No hay ningún uso de toohello inconveniente de RECORTE en discos de Azure en marcas premium o estándar.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Nuevos tamaños de discos: tanto administrados como no administrados

**¿Cuál es el tamaño de disco más grande de Hola compatible con discos de datos y sistema operativo?**

tipo de partición de Hola que es compatible con Azure para un disco del sistema operativo es registro de arranque maestro (MBR) de Hola. formato MBR Hello es compatible con un tamaño de disco hasta too2 TB. tamaño máximo de Hola que es compatible con Azure para un disco del sistema operativo es de 2 TB. Azure admite hasta too4 TB para discos de datos. 

**¿Qué es Hola mayor blob tamaño de página que sea compatible?**

Hola página blob tamaño máximo que admite Azure es 8 TB (8.191 GB). No se admiten blobs en páginas mayores de 4 TB (4.095 GB) adjuntada tooa VM como datos o discos del sistema operativo.

**¿Necesito toouse una nueva versión de toocreate de herramientas de Azure, conectar, cambiar el tamaño y cargar discos de más de 1 TB?**

No es necesario tooupgrade su toocreate herramientas de Azure existente, adjuntar o cambiar el tamaño de los discos de más de 1 TB. tooupload de archivos desde el disco duro virtual local directamente tooAzure como un blob de página o un disco no administrado, es necesario conjuntos de herramientas más recientes de toouse hello:

|Herramientas de Azure      | Versiones compatibles                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Número de versión 4.1.0: versión de junio de 2017 o posterior|
|CLI de Azure v1     | Número de versión 0.10.13: versión de mayo de 2017 o posterior|
|AzCopy           | Número de versión 6.1.0: versión de junio de 2017 o posterior|

compatibilidad con Hello v2 de CLI de Azure y Azure Storage Explorer estará disponible próximamente. 

**¿Se admiten los tamaños de disco P4 y P6 para blobs en páginas o discos no administrados?**

No. Los tamaños de disco P4 (32 GB) y P6 (64 GB) solo son compatibles con discos administrados. La compatibilidad para blobs en páginas y discos no administrados estará disponible próximamente.

**Si mi premium existente administrado del disco de menos de 64 GB se creó antes de habilita la disco pequeño hello (alrededor de 15 de junio de 2017), ¿cómo se se factura?**

Los discos premium pequeño existentes menor que 64 GB continuar toobe facturada correspondiente toohello P10 tarifa. 

**¿Cómo puedo cambiar nivel de disco Hola de discos pequeños premium menor que 64 GB de tooP4 P10 o P6?**

Puede tomar una instantánea de los discos pequeños y, a continuación, crear un Hola de conmutador de tooautomatically disco tooP4 de nivel de precios o P6 según el tamaño de hello aprovisionado. 


## <a name="what-if-my-question-isnt-answered-here"></a>Mi pregunta no está respondida aquí. ¿Qué debo hacer?

Si su pregunta no aparece aquí, háganoslo saber y lo ayudaremos a encontrar una respuesta. Puede publicar una pregunta final Hola de este artículo en los comentarios de Hola. tooengage con el equipo de almacenamiento de Azure de Hola y otros miembros de la Comunidad sobre este artículo, use Hola MSDN [foro de almacenamiento de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

características de toorequest, enviar su solicitudes e ideas toohello [foro de comentarios de almacenamiento de Azure](https://feedback.azure.com/forums/217298-storage).
