### <a name="record-names"></a>Nombres de registro

En DNS de Azure, los registros se especifican mediante el uso de nombres relativos. A *completo* nombre de dominio (FQDN) incluye el nombre de la zona de hello, mientras que un *relativa* nombre no lo hace. Por ejemplo, nombre de registro relativo de Hola "www" en la zona de hello 'contoso.com' da nombre de registro completo de hello 'www.contoso.com'.

Un *vértice* registro es un registro DNS en la raíz de hello (o *vértice*) de una zona DNS. Por ejemplo, en la zona DNS de Hola "contoso.com", un registro de vértice tiene también nombre completo de hello 'contoso.com' (Esto se denomina a veces un *naked* dominio).  Por convención, Hola nombre relativo ' @' es toorepresent usa registros de vértice.

### <a name="record-types"></a>Tipos de registro

Cada registro DNS tiene un nombre y un tipo. Los registros se organizan en diferentes tipos según datos toohello que contienen. tipo más común de Hello es un registro "A", que se asigna una dirección IPv4 de tooan de nombre. Otro tipo común es un registro de 'MX', que se asigna un servidor de correo electrónico de tooa de nombres.

DNS de Azure es compatible con todos los tipos de registro DNS comunes: A, AAAA, CNAME, MX, NS, PTR, SOA, SRV y TXT. Tenga en cuenta que [los registros de SPF se representan mediante registros TXT](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Conjuntos de registros

En ciertas ocasiones necesitará toocreate más de un registro DNS con un nombre especificado y el tipo. Por ejemplo, suponga que se hospeda el sitio web de hello 'www.contoso.com' en dos direcciones IP. sitio Web de Hello requiere dos diferentes registros, uno para cada dirección IP. Este es un ejemplo de un conjunto de registros:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

Azure DNS administra todos los registros DNS con *conjuntos de registros*. Un conjunto de registros (también conocido como un *recursos* grabar conjunto) es Hola colección de registros DNS en una zona que han Hola mismo nombre y son de hello mismo tipo. La mayoría de conjuntos de registros contienen un único registro. Sin embargo, los ejemplos como Hola anteriormente, en que un conjunto de registros contiene más de un registro, no son habituales.

Por ejemplo, supongamos que ya ha creado un registro a "www" en la zona de hello 'contoso.com', que señala toohello IP direcciones '134.170.185.46' (Hola primer registro anterior).  toocreate Hola segundo registro agregaría que registran el registro existente toohello establecer, en lugar de crear un conjunto de registros adicional.

Hola SOA y tipos de registros CNAME son excepciones. los estándares de DNS de Hello no admiten varios registros con el mismo nombre para estos tipos de Hola, por lo tanto, estos conjuntos de registros solo pueden contener un único registro.
