Existen dos tipos de cuentas de almacenamiento:

### <a name="general-purpose-storage-accounts"></a>Cuentas de almacenamiento de uso general
Un proporciona de cuenta de almacenamiento general acceso tooAzure servicios de almacenamiento, como tablas, colas, archivos, Blobs y Azure discos de máquina virtual en una sola cuenta. Este tipo de cuenta de almacenamiento tiene dos niveles de rendimiento:

* Un nivel de rendimiento de almacenamiento estándar que le permite toostore tablas, colas, archivos, Blobs y Azure discos de máquina virtual.
* Un nivel de rendimiento de almacenamiento premium que actualmente solo admite discos de máquina virtual de Azure. Consulte [Almacenamiento premium: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md) para una información general detallada del Almacenamiento premium.

### <a name="blob-storage-accounts"></a>Cuentas de Almacenamiento de blobs
Una cuenta de Almacenamiento de blobs es una cuenta de almacenamiento especializado para almacenar los datos no estructurados como blobs (objetos) en Almacenamiento de Azure. Las cuentas de almacenamiento de blobs son similares tooyour cuentas de almacenamiento general existente y comparten todos los Hola gran durabilidad, disponibilidad, escalabilidad y rendimiento de características que usan hoy incluida la coherencia de la API de 100% para blobs en bloques y blobs en anexos. Para las aplicaciones que requieren solo Almacenamiento de blobs en bloque o en anexos, se recomienda utilizar cuentas de Almacenamiento de blobs.

> [!NOTE]
> Las cuentas de Almacenamiento de blobs solo admiten blobs en bloques y en anexos, pero no blobs en páginas.
> 
> 

Las cuentas de almacenamiento de blobs exponen hello **nivel de acceso a** atributo que se puede especificar durante la creación de cuentas y modificar posteriormente según sea necesario. Hay dos tipos de niveles de acceso que se pueden especificar según el patrón de acceso a datos:

* A **activa** nivel de acceso que indica que los objetos de hello en la cuenta de almacenamiento de Hola se accederá con más frecuencia. Esto le permite toostore datos a un menor costo de acceso.
* A **frío** nivel de acceso que indica que los objetos de hello en la cuenta de almacenamiento de Hola se accederá con menos frecuencia. Esto le permite toostore datos a un menor costo de almacenamiento de datos.

Si hay un cambio en el patrón de uso de Hola de los datos, también puede cambiar entre estos niveles de acceso en cualquier momento. Cambiar nivel de acceso de hello puede costar dinero adicional. Para más información, consulte [Precios y facturación](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) .

Para más información acerca de las cuentas de Almacenamiento de blobs, consulte [Almacenamiento de blobs de Azure: niveles de acceso Esporádico y Frecuente](../articles/storage/blobs/storage-blob-storage-tiers.md).

Para poder crear una cuenta de almacenamiento, debe tener una suscripción de Azure, que es un plan que ofrece acceso tooa diversos servicios de Azure. Para comenzar con Azure, puede usar una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/). Una vez que decida toopurchase un plan de suscripción, puede elegir entre una variedad de [opciones de compra](https://azure.microsoft.com/pricing/purchase-options/). Si ya es [suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), obtendrá créditos mensuales gratuitos que podrá usar con los servicios de Azure, incluido Almacenamiento de Azure. Para obtener información acerca de los precios por volumen, consulte [Precios de Almacenamiento de Azure ](https://azure.microsoft.com/pricing/details/storage/) .

toolearn toocreate una cuenta de almacenamiento, vea [crear una cuenta de almacenamiento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) para obtener más detalles. Puede crear hasta too200 nombra cuentas de almacenamiento con una sola suscripción. Para más información acerca de los límites de las cuentas de almacenamiento, consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](../articles/storage/common/storage-scalability-targets.md) .

