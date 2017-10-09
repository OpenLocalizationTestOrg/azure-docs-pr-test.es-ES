# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regiones y disponibilidad de máquinas virtuales en Azure
Azure funciona en varios centros de datos alrededor de Hola a todos. Los centros de datos se agrupan en las regiones de toogeographic, lo que le proporciona flexibilidad al elegir dónde toobuild sus aplicaciones. Es importante toounderstand cómo y donde las máquinas virtuales (VM) operan en Azure, junto con el rendimiento de toomaximize de opciones, disponibilidad y redundancia. Este artículo proporciona información general sobre la disponibilidad de Hola y las características de redundancia de Azure.

## <a name="what-are-azure-regions"></a>¿Cuáles son las regiones de Azure?
Los recursos de Azure se crean en regiones geográficas definidas como 'Oeste de EE. UU.', 'Europa del Norte' o 'Sudeste Asiático'. Puede revisar hello [lista de regiones y sus ubicaciones](https://azure.microsoft.com/regions/). Dentro de cada región, varios centros de datos existen tooprovide para ofrecer redundancia y disponibilidad. Este enfoque le proporciona flexibilidad al diseñar toomeet y toocreate máquinas virtuales más cercano tooyour usuarios de aplicaciones de cualquier legal, cumplimiento de normas, o fiscales.

## <a name="special-azure-regions"></a>Regiones de Azure especiales
Azure tiene algunas regiones especial que puede ser conveniente toouse al crear las aplicaciones para fines legales o de cumplimiento de normas. Entre dichas regiones se incluyen:

* **Virginia Gob. EE. UU.** e **Iowa Gob. EE. UU.**
  * Una instancia física y lógica con aislamiento de red de Azure para asociados y agencias de la administración pública de EE. UU., operada por personal estadounidense seleccionado con rigor. Incluye certificaciones de cumplimiento adicionales como [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) y [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Más información sobre [Azure Government](https://azure.microsoft.com/features/gov/).
* **China (Este)** y **China (Norte)**
  * Estas regiones están disponibles a través de un perfil único entre Microsoft y 21Vianet, por la que Microsoft no mantiene directamente Hola centros de datos. Obtenga más información sobre [Microsoft Azure en China](http://www.windowsazure.cn/).
* **Centro de Alemania** y **Noreste de Alemania**
  * Estas regiones están disponibles a través de un modelo de usuario de confianza de datos mediante el cual los datos de cliente permanecen en Alemania bajo el control de sistemas de T, una compañía Deutsche Telekom, que actúa como usuario de confianza de hello datos alemán.

## <a name="region-pairs"></a>Pares de región
Cada región de Azure se empareja con otra región dentro de hello geography mismo (por ejemplo, EE. UU., Europa y Asia). Este enfoque permite replicación Hola de recursos, como almacenamiento de máquina virtual, en una ubicación geográfica que se debe reducir la probabilidad de Hola de desastres naturales, disturbios civiles, cortes del suministro eléctrico o interrupciones de red física a la vez que afectan a ambas regiones. Entre las ventajas adicionales de los pares de región se incluyen:

* En caso de hello de una interrupción de Azure más amplia, una región se establece una prioridad de cada par toohelp reducir hello toorestore de tiempo para las aplicaciones. 
* Las actualizaciones planeadas de Azure se implementan regiones toopaired uno en un tiempo de inactividad de toominimize de tiempo y el riesgo de interrupción de la aplicación.
* Los datos continúan tooreside dentro de hello geography mismo como su par (excepto el sur de Brasil) para fines de jurisdicción de cumplimiento de impuestos y derecho.

Entre los ejemplos de pares de región se incluyen:

| Principal | Secundario |
|:--- |:--- |
| Oeste de EE. UU. |Este de EE. UU. |
| Europa del Norte |Europa occidental |
| Sudeste asiático |Asia oriental |

Puede ver Hola completa [lista de configuración regional pares aquí](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Disponibilidad de características
Algunos servicios o características de las máquinas virtuales solo están disponibles en determinadas regiones, como, por ejemplo, tipos de almacenamiento o tamaños de VM específicos. También hay algunos servicios de Azure globales que no requieren tooselect una región determinada, como [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md), o [DNS de Azure](../articles/dns/dns-overview.md). tooassist se diseña el entorno de aplicación, puede comprobar hello [disponibilidad de los servicios de Azure a través de cada región](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Disponibilidad de almacenamiento
Descripción de regiones geográficas y regiones de Azure es importante al considerar Hola opciones de replicación de almacenamiento disponibles. Según el tipo de almacenamiento de hello, tiene opciones de replicación diferentes.

**Azure Managed Disks**
* Almacenamiento con redundancia local (LRS)
  * Replica los datos tres veces dentro de región de hello en el que creó la cuenta de almacenamiento.

**Discos basados en cuentas de almacenamiento**
* Almacenamiento con redundancia local (LRS)
  * Replica los datos tres veces dentro de región de hello en el que creó la cuenta de almacenamiento.
* Almacenamiento con redundancia de zona (ZRS)
  * Replica los datos tres veces entre dos instalaciones de toothree, en una única región o entre dos regiones.
* Almacenamiento con redundancia geográfica (GRS)
  * Replica la región secundaria de tooa de datos que se encuentra a cientos de millas fuera de la región principal de Hola.
* Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS).
  * Replica la región secundaria tooa de datos, al igual que con GRS, pero también, a continuación, proporciona datos de toohello de acceso de solo lectura en la ubicación secundaria Hola.

Hello tabla siguiente proporciona una introducción rápida de diferencias de hello entre tipos de replicación de almacenamiento de hello:

| Estrategia de replicación | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Los datos se replican entre varias instalaciones |No |Sí |Sí |Sí |
| Datos se pueden leer desde la ubicación secundaria de Hola y de ubicación principal Hola. |No |No |No |Sí |
| Cantidad de copias de datos mantenidas en nodos independientes |3 |3 |6 |6 |

Puede obtener más información sobre las [opciones de replicación de Almacenamiento de Azure aquí](../articles/storage/common/storage-redundancy.md). Para más información acerca de los discos administrados, consulte [Azure Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md) (Introducción a los discos administrados de Azure).

### <a name="storage-costs"></a>Costos de almacenamiento
Los precios varían según el tipo de almacenamiento de Hola y disponibilidad que seleccione.

**Azure Managed Disks**
* Las copias de seguridad de Managed Disks premium se realizan en unidades de estado sólido (SSD) y las de Managed Disks estándar en discos de rotación normales. Premium y estándar de discos administrados se cobran en función de la capacidad de hello aprovisionado para el disco de Hola.

**Discos no administrados**
* Almacenamiento Premium está respaldado por Solid-State unidades (SSD) y se cobra a la capacidad de hello del disco de Hola.
* Almacenamiento estándar está respaldado por los discos de rotación normal y se cobra a la capacidad de hello en uso y deseado de la disponibilidad de almacenamiento.
  * Para RA-GRS, hay un costo adicional de transferencia de datos de replicación geográfica para ancho de banda de Hola de replicación de ese tooanother datos región de Azure.

Vea [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) para obtener más información sobre Hola diferentes tipos de almacenamiento y opciones de disponibilidad.

## <a name="availability-sets"></a>Conjuntos de disponibilidad
Un conjunto de disponibilidad es una agrupación lógica de máquinas virtuales que permite a Azure toounderstand modo en que la aplicación se compila tooprovide para ofrecer redundancia y disponibilidad. Se recomienda que se crean dos o más máquinas virtuales dentro de un tooprovide de conjunto de disponibilidad para una alta disponibilidad Hola de aplicación y toomeet [99,95% SLA de Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Cuando se usa una sola máquina virtual [almacenamiento de Azure Premium](../articles/storage/common/storage-premium-storage.md), Hola SLA de Azure se aplica para los eventos de mantenimiento no planeado. 

Un conjunto de disponibilidad se compone de dos grupos adicionales que proteger frente a errores de hardware y permiten las actualizaciones pueden toosafely aplica - error de dominios (FD) y actualizar dominios (ud).

![Dibujo conceptual de configuración del dominio de error y de dominio de actualización Hola](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Más información sobre cómo toomanage Hola disponibilidad de [máquinas virtuales de Linux](../articles/virtual-machines/linux/manage-availability.md) o [máquinas virtuales de Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Dominios de error
Un dominio de error es un grupo lógico de hardware subyacente que comparten una fuente de energía y conmutador de red, similar bastidor tooa dentro de un centro de datos local. A medida que cree las máquinas virtuales dentro de un conjunto de disponibilidad, Hola plataforma Windows Azure distribuye automáticamente las máquinas virtuales entre estos dominios de error. Este enfoque limita el impacto de Hola de posibles errores de hardware físico, las interrupciones de red o las interrupciones de energía.

### <a name="update-domains"></a>Dominios de actualización
Un dominio de actualización es un grupo lógico de hardware subyacente que puede pasar por mantenimiento o reiniciarse en hello mismo tiempo. A medida que cree las máquinas virtuales dentro de un conjunto de disponibilidad, hello plataforma Windows Azure distribuye automáticamente las máquinas virtuales entre estos dominios de actualización. Este enfoque garantiza que al menos una instancia de la aplicación siempre es la ejecución como plataforma de Azure hello sufre mantenimiento periódico. orden de Hola de dominios de actualización que se está reiniciando no se puede continuar secuencialmente durante el mantenimiento planeado, pero solo una actualización de dominio se reinicia cada vez.

### <a name="managed-disk-fault-domains"></a>Dominios de error de Managed Disks
Para las máquinas virtuales que usen [Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md), las máquinas virtuales se alinean con los dominios de error de disco administrado cuando se usa un conjunto de disponibilidad administrada. Esta alineación garantiza que todos los discos administrados tooa adjunto VM están dentro de Hola Hola mismo dominio de error de disco administrado. Solo se pueden crear máquinas virtuales con discos administrados en un conjunto de disponibilidad administrada. número de Hola de dominios de error de disco administrado varía según la región - dos o tres dominios de error de disco administrado por región.

![Dominios de error de disco administrado](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> número de Hola de dominios de error para los conjuntos de disponibilidad administrada varía según la región - dos o tres por región. Hello tabla siguiente muestran el número de Hola por región

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Pasos siguientes
Ahora puede empezar a toouse estos disponibilidad y redundancia características toobuild el entorno de Azure. Para información sobre los procedimientos recomendados, consulte [Lista de comprobación de disponibilidad](../articles/best-practices-availability-checklist.md).

