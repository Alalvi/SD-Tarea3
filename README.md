# SD-Tarea3
1. Explique la arquitectura que Cassandra maneja. Cuando se crea el clúster ¿C´omo los nodos se conectan? ¿Qu´e
ocurre cuando un cliente realiza una petici´on a uno de los nodos? ¿Qu´e ocurre cuando uno de los nodos se desconecta?
¿La red generada entre los nodos siempre es eficiente? ¿Existe balanceo de carga?

R:
-Los nodos se conectan en el cluster como peer to peer.
-El nodo al que se conecta el cliente actúa como coordinardor entre este y el resto de los nodos buscando los datos relacionados con la petición.
-Cuando un nodo se desconecta un nodo, en el caso de que exista un factor de replica mayor a uno, otro nodo funcionaría en su lugar con una replica de la información del nodo desconectado.
-La red generada no necesariamente puede ser eficiente, debido a que se requiere el conocer las queries se van a ejecutar, debido que se puede perjudicar las queries con SELECT dependiendo de la política con que se generan las replicas.
-Dependiendo de como son implementadas las particiones, si son implementadas como partición aleatoria, si existe balanceo de carga. Por otro lado si es implementada una partición con preservación del orden las claves similiares se ubican muy cerca entre ellas, por lo que no existe una distribución regular entre los nodos.


2. Cassandra posee principalmente dos estrategias para mantener redundancia en la replicaci´on de datos. ¿Cu´ales son
estos? ¿Cu´al es la ventaja de uno sobre otro? ¿Cu´al utilizar´ıa usted para en el caso actual y por qu´e? Justifique
apropiadamente su respuesta.

-Las dos estrategias principalmente usadas son SimpleStrategy u NetworkTopologyStrategy. |LocalStrategy
-NetworkTopologyStrategy permite distribuir las replicas de noods en distintos centros de datos, por otro lado, SimpleStrategy permite hacerlo dentro de un solo centro de datos.
-Utilizaría SimpleStrategy para el caso actual debido a que se requiere implementar un cluster con tres nodos, implementadas de manera local. 

Existe una tercera estrategia para aplicar ne Cassandra, LocalStrategy  es utilizada de manera interna por cassandra, por lo cual las keyspaces son definidas implicitamente. Debido a que en la tarea se requiere tener dos tablas, una maestra y una esclava lo que requiere una keyspace.

Fuente: https://www.geeksforgeeks.org/replication-strategy-in-cassandra/

3. Teniendo en cuenta el contexto del problema ¿Usted cree que la soluci´on propuesta es la correcta? ¿Qu´e ocurre
cuando se quiere escalar en la soluci´on? ¿Qu´e mejoras implementar´ıa? Oriente su respuesta hacia el Sharding (la
replicaci´on/distribuci´on de los datos) y comente una estrategia que podr´ıa seguir para ordenar los datos.

R:
-En el contexto actual del problema, si la solución propuesta es correcta.
-En el caso de que se requiera escalar la solución, esta empezaría a ser menos eficiente.
-Cambiaría la estrategia a NetworkTopologyStrategy, debido a que a medida que deben adicionarse nodos, mantener todos los nodos dentro de el mismo centro de datos lo haría propenso a caerse al perder este centro. Por otro lado una vez elegida esta estrategia, dependiendo del tamaño de infomración administrada, la fragmentación de datos sería necesaria, para lo cual implementaría una partición tipo Murmur3partitioner el cual es 3 a 5 veces más veloz que RandomPartitioner, y a diferencia de la partición ByteOrderedPartitioner
la cual posee grandes problemas como el balanceo de carga debe ser manual, o la escritura secuancial de filas en un intervalo es asignado a un solo nodo.

Fuente:https://docs.datastax.com/en/archived/cassandra/3.0/cassandra/architecture/archTOC.html

