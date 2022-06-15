# SD-Tarea3
1. Explique la arquitectura que Cassandra maneja. Cuando se crea el clúster ¿C´omo los nodos se conectan? ¿Qu´e
ocurre cuando un cliente realiza una petici´on a uno de los nodos? ¿Qu´e ocurre cuando uno de los nodos se desconecta?
¿La red generada entre los nodos siempre es eficiente? ¿Existe balanceo de carga?

R:Los nodos se conectan como peer to peer, el nodo al que se conecta el cliente actúa como coordinardor entre este y el resto de los nodos buscando los datos relacionados con la petición.


2. Cassandra posee principalmente dos estrategias para mantener redundancia en la replicaci´on de datos. ¿Cu´ales son
estos? ¿Cu´al es la ventaja de uno sobre otro? ¿Cu´al utilizar´ıa usted para en el caso actual y por qu´e? Justifique
apropiadamente su respuesta.


3. Teniendo en cuenta el contexto del problema ¿Usted cree que la soluci´on propuesta es la correcta? ¿Qu´e ocurre
cuando se quiere escalar en la soluci´on? ¿Qu´e mejoras implementar´ıa? Oriente su respuesta hacia el Sharding (la
replicaci´on/distribuci´on de los datos) y comente una estrategia que podr´ıa seguir para ordenar los datos.

