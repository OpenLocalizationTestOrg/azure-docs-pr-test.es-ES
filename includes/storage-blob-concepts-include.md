## <a name="what-is-blob-storage"></a>¿Qué es el almacenamiento de blobs?
Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos de objeto no estructurados, como texto o datos binarios, que pueden tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS. Puede usar datos de tooexpose de almacenamiento de Blob públicamente toohello world o datos de la aplicación toostore privada.

El almacenamiento de blobs suele usarse para realizar las siguientes tareas:

* Servicio de imágenes o documentos directamente tooa explorador
* Almacenamiento de archivos para acceso distribuido
* Streaming de audio y vídeo
* Almacenamiento de datos para copia de seguridad y restauración, recuperación ante desastres y archivado
* Almacenamiento de datos para el análisis en local o en un servicio hospedado de Azure

## <a name="blob-service-concepts"></a>Conceptos del servicio BLOB
Hola servicio Blob contiene Hola de los componentes siguientes:

![Arquitectura de blob](./media/storage-blob-concepts-include/blob1.png)

* **Cuenta de almacenamiento:** todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento. Esta cuenta de almacenamiento puede ser una **cuenta de almacenamiento de uso general** o una **cuenta de Blob Storage**, que sirve para almacenar objetos o blobs. Para más información, consulte [Acerca de las cuentas de Azure Storage](../articles/storage/common/storage-create-storage-account.md).
* **Contenedor**: un contenedor proporciona una agrupación de un conjunto de blobs. Todos los blobs deben residir en un contenedor. Además, una cuenta puede disponer de un número ilimitado de contenedores y un contenedor puede almacenar un número ilimitado de blobs. Tenga en cuenta que ese nombre de contenedor de hello debe estar en minúscula.
* **Blob:** archivo de cualquier tipo y tamaño. Almacenamiento de Azure ofrece tres tipos de blobs: blobs en bloques, blobs en páginas y blobs en anexos.
  
    *blobs en bloques* son ideales para almacenar archivos binarios o de texto, como documentos y archivos multimedia. *Blobs en anexos* son similares blobs tooblock en que se compone de bloques, pero están optimizados para las operaciones de anexión, por lo que son útiles para escenarios de registro. Un blob en bloques solo puede contener hasta too50, 000 bloques de too100 MB cada uno, hasta un tamaño total de ligeramente superior a 4,75 TB (100 MB X 50.000). Un blob en anexos solo puede contener hasta too50, 000 bloques de too4 MB cada uno, hasta un tamaño total de algo más de 195 GB (4 MB X 50.000).
  
    *Blobs de página* puede ser hasta too1 TB en tamaño y son más eficaces para las operaciones frecuentes de lectura/escritura. Máquinas virtuales de Azure usa blobs en páginas como discos de sistema operativo y de datos.
  
    Para más información sobre la nomenclatura de contenedores y blobs, consulte [Asignación de nombres y referencias a contenedores, blobs y metadatos](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

