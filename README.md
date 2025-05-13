# ExamenFinalRedes_GabrielHernanz_153982

**Autor**: Gabriel Hernanz  
**Examen Final de Redes II – Cisco Packet Tracer**

Link con acceso al respositorio --> https://github.com/GabriHR/ExamenFinalRedes_GabrielHernanz_153982.git

# Parte I - Misiones de Conocimiento Teórico

## 🛰️ Misión 1: Reconexión en la Base Eco (Hoth) – Direccionamiento IP y Subredes

## 📖 Situación
La Base Eco en Hoth ha quedado incomunicada tras un bombardeo imperial. La General Leia Organa te encomienda diseñar un nuevo esquema de red para restablecer la comunicación interna y con la flota rebelde. Hoth alberga varios departamentos (mando, defensa, médico, hangar) y cada uno necesita su propia subred IP debido a requisitos de seguridad y cantidad de dispositivos. Disponéis de un bloque de direcciones limitado y es crucial usarlo eficientemente.

**Narrativa:** Bajo la tormenta helada de Hoth, los generadores de energía zumban mientras instalas nuevos equipos de red. Leia, con su atuendo invernal, te explica: "Necesitamos reorganizar las comunicaciones de la base. Cada sector debe tener su red, y todas deben poder conectarse con la antena principal. El rango de direcciones del que disponemos es limitado, joven padawan. Debes dividir la red sabiamente, como un Jedi dividiría sus esfuerzos.".

**Objetivo de la misión:** Diseña un plan de direccionamiento IP para la Base Eco utilizando subnetting. Parte de una red asignada (por ejemplo, 172.16.0.0/24) y subdivide en subredes adecuadas para cada departamento, cumpliendo estos requisitos (ficticios):

- Comando Central: ~50 hosts (dispositivos)

- Defensa Perimetral: ~30 hosts

- Centro Médico: ~20 hosts

- Hangar y Taller: ~14 hosts

Además, reserva una subred adicional para el enlace troncal con la antena de comunicaciones que conecta Hoth con el resto de la galaxia. Debes detallar la dirección de red, máscara y rango de hosts de cada subred resultante.

**Pregunta:** ¿Cómo dividirías la red 172.16.0.0/24 en subredes para satisfacer las necesidades anteriores, asignando direcciones IP a cada segmento de la base? Indica las subredes obtenidas (con su notación de máscara /xx), la cantidad de hosts útiles en cada una, y especifica qué subred se destinaría al enlace troncal interplanetario.
## 🛠️ Plan de direccionamiento IP
Partimos de la red **172.16.0.0/24** y la dividimos en subredes adecuadas para cada departamento.

### Asignación de subredes

| Departamento         | Dirección de Red     | Máscara de Subred       | Rango de Hosts Utilizables     | Total de Hosts |
|----------------------|---------------------|-------------------------|-------------------------------|--------------|
| **Comando Central** | `172.16.0.0/26`     | `255.255.255.192`       | `172.16.0.1 - 172.16.0.62`    | 62          |
| **Defensa Perimetral** | `172.16.0.64/27`   | `255.255.255.224`       | `172.16.0.65 - 172.16.0.94`   | 30          |
| **Centro Médico**   | `172.16.0.96/27`    | `255.255.255.224`       | `172.16.0.97 - 172.16.0.126`  | 30          |
| **Hangar y Taller** | `172.16.0.128/28`   | `255.255.255.240`       | `172.16.0.129 - 172.16.0.142` | 14          |
| **Enlace Troncal**  | `172.16.0.144/28`   | `255.255.255.240`       | `172.16.0.145 - 172.16.0.158` | 14          |

### Conclusión
Cada departamento de la Base Eco cuenta ahora con una subred optimizada, maximizando el uso del espacio disponible y asegurando la comunicación interna y con la antena de comunicaciones. ¡Misión cumplida, padawan! Que la Fuerza del subnetting te acompañe. 

---

# 🌌 Misión 2: Sabiduría de Yoda – Algoritmos de Enrutamiento y Rutas
## 📖 Situación 
La flota rebelde ha interceptado transmisiones imperiales que mencionan distintos códigos de planeta y nombres en clave. Para coordinar un contraataque, la Alianza necesita entender cómo los nombres de dominio galácticos se traducen en localizaciones reales. En otras palabras, requieren restablecer un servicio DNS rebelde que asocie nombres de sistemas estelares con direcciones de la red. Sin DNS, comunicarse es tan difícil como encontrar un Ewok en la noche de Endor.

## Narrativa: 
A bordo de la nave de mando Home One, los técnicos rebelde te muestran un panel donde parpadea la petición “Unknown host”. El Almirante Ackbar frunce el ceño mientras exclaims: "¡Es una trampa... de nombres! Nuestros sistemas no reconocen las direcciones de destino." Mon Mothma asiente con gravedad: "Debemos reconstruir nuestro directorio de comunicaciones. Aprendiz, ¿cómo funciona este Sistema de Nombres de Dominio nuestro? ¿Por qué es tan importante?".

Tú recuerdas tus lecciones sobre cómo en la Red (o la HoloRed) se gestionan las direcciones simbólicas. Un nombre como “echo.base” debe traducirse a una dirección IP para establecer conexión. Ha llegado el momento de explicarlo claramente.

**Pregunta: Explica el funcionamiento básico del sistema DNS** y su importancia en la comunicación en redes. ¿Cómo realiza la red rebelde (o cualquier red TCP/IP) la resolución de nombres de dominio a direcciones IP? Incluye en tu explicación qué es un servidor DNS y un registro (por ejemplo, un registro A), ilustrando con un ejemplo simple (por ejemplo: traducir holonet.rebelion.org a una dirección IP)


Además, menciona brevemente qué sucede si el servidor DNS no está disponible y cómo eso afectaría a las comunicaciones de la Alianza.

## Solución:
### Comparación: Enrutamiento Estático vs. Dinámico

| Tipo de Enrutamiento | Ventajas | Inconvenientes |
|----------------------|----------|---------------|
| **Estático** | - Control total sobre las rutas.<br>- Menor consumo de recursos.<br>- Mayor seguridad al evitar cambios automáticos. | - No se adapta a cambios en la red.<br>- Difícil de gestionar en redes grandes.<br>- Requiere configuración manual en cada nodo. |
| **Dinámico** | - Se ajusta automáticamente a cambios en la topología.<br>- Escalable para redes grandes.<br>- Optimiza el uso del ancho de banda. | - Mayor consumo de CPU y memoria.<br>- Puede tardar en converger tras una falla.<br>- Más complejo de configurar. |

### Protocolos de Enrutamiento Dinámico
Uno de los protocolos más utilizados en enrutamiento dinámico es **OSPF (Open Shortest Path First)**. Este protocolo de estado de enlace permite que los routers intercambien información sobre la topología de la red y calculen la mejor ruta de manera eficiente.

Por otro lado, los protocolos de **vector de distancia**, como **RIP (Routing Information Protocol)**, funcionan enviando información sobre las rutas a sus vecinos, pero tienen limitaciones en redes grandes debido a su tiempo de convergencia y la métrica basada en el número de saltos.

### Diferencias entre Vector de Distancia y Estado de Enlace
- **Vector de distancia**: Los routers solo conocen información de sus vecinos y envían actualizaciones periódicas. Es más simple pero menos eficiente en redes grandes.
- **Estado de enlace**: Cada router tiene una visión completa de la red y calcula rutas óptimas. Es más rápido y preciso, pero requiere más recursos.

### Respuesta ante fallos y escalabilidad
Si un nodo cae repentinamente:
- **Enrutamiento estático**: La ruta se rompe y debe ser corregida manualmente.
- **Enrutamiento dinámico**: Los routers detectan el fallo y recalculan automáticamente nuevas rutas.

Si la red debe expandirse a más planetas:
- **Enrutamiento estático**: Se vuelve inmanejable debido a la cantidad de rutas manuales.
- **Enrutamiento dinámico**: Se adapta automáticamente, permitiendo una expansión fluida.

### Conclusión
El enrutamiento estático es ideal para redes pequeñas y controladas, mientras que el dinámico es esencial para redes grandes y cambiantes. ¡Misión cumplida, padawan! Que la Fuerza del enrutamiento te guíe en tu camino. 

---

# 🌌 Misión 3: Los Nombres del Holonet – DNS y Resolución de Nombres

## 📖 Situación
La flota rebelde ha interceptado transmisiones imperiales que mencionan distintos códigos de planeta y nombres en clave. Para coordinar un contraataque, la Alianza necesita entender cómo los nombres de dominio galácticos se traducen en localizaciones reales. En otras palabras, requieren restablecer un servicio DNS rebelde que asocie nombres de sistemas estelares con direcciones de la red. Sin DNS, comunicarse es tan difícil como encontrar un Ewok en la noche de Endor.

**Narrativa:** A bordo de la nave de mando Home One, los técnicos rebelde te muestran un panel donde parpadea la petición “Unknown host”. El Almirante Ackbar frunce el ceño mientras exclaims: "¡Es una trampa... de nombres! Nuestros sistemas no reconocen las direcciones de destino." Mon Mothma asiente con gravedad: "Debemos reconstruir nuestro directorio de comunicaciones. Aprendiz, ¿cómo funciona este Sistema de Nombres de Dominio nuestro? ¿Por qué es tan importante?".

Tú recuerdas tus lecciones sobre cómo en la Red (o la HoloRed) se gestionan las direcciones simbólicas. Un nombre como “echo.base” debe traducirse a una dirección IP para establecer conexión. Ha llegado el momento de explicarlo claramente.

**Pregunta:** Explica el funcionamiento básico del sistema DNS y su importancia en la comunicación en redes. ¿Cómo realiza la red rebelde (o cualquier red TCP/IP) la resolución de nombres de dominio a direcciones IP? Incluye en tu explicación qué es un servidor DNS y un registro (por ejemplo, un registro A), ilustrando con un ejemplo simple (por ejemplo: traducir holonet.rebelion.org a una dirección IP)​

Además, menciona brevemente qué sucede si el servidor DNS no está disponible y cómo eso afectaría a las comunicaciones de la Alianza.
###  ¿Qué es el DNS y por qué es importante?
El **Sistema de Nombres de Dominio (DNS)** traduce nombres de dominio legibles por humanos en direcciones IP comprensibles por las máquinas. Sin DNS, tendríamos que recordar largas secuencias numéricas en lugar de nombres intuitivos como `holonet.rebelion.org`.

### ¿Cómo funciona la resolución de nombres?
Cuando un dispositivo intenta acceder a un dominio, sigue estos pasos:
1. **Consulta al servidor DNS local**: El dispositivo pregunta a su servidor DNS si conoce la dirección IP del dominio.
2. **Búsqueda en caché**: Si el servidor DNS ya tiene la dirección almacenada, la devuelve inmediatamente.
3. **Consulta a servidores superiores**: Si no tiene la respuesta, pregunta a los servidores raíz, que dirigen la consulta a los servidores de dominio adecuados.
4. **Respuesta final**: Una vez encontrada la dirección IP, el servidor DNS la envía al dispositivo, permitiendo la conexión.

### Elementos clave del DNS
- **Servidor DNS**: Un sistema que almacena y gestiona la traducción de nombres de dominio a direcciones IP.
- **Registro A**: Un tipo de registro DNS que asocia un nombre de dominio con una dirección IPv4. Ejemplo:

---
# 🚀 Misión 4: “Es una trampa… de protocolos!” – TCP vs UDP en las transmisiones

## 📖 Situación
Durante la batalla espacial sobre Endor, los ingenieros de comunicación rebelde notan comportamientos distintos en las transmisiones de datos. Algunas comunicaciones deben ser rápidas aunque ocasionalmente se pierda información (por ejemplo, un stream de vídeo de una cámara X-Wing), mientras que otras deben llegar íntegras y en orden aunque tarden un poco más (por ejemplo, la transferencia de los planos de la Estrella de la Muerte). Estas diferencias corresponden al uso de distintos protocolos de transporte: UDP y TCP. Luke Skywalker, ahora piloteando su X-Wing y ejerciendo de líder en el ataque, te pregunta por qué percibe lagos de datos en unas transmisiones y retrasos en otras.

**Narrativa:** En medio del fragor de la batalla, ves cómo R2-D2 proyecta diagramas de paquetes dentro del X-Wing de Luke. "Algunas de estas tramas van rápidas como el Halcón Milenario, pero otras llegan seguras como Yoda al Consejo," comenta Luke por el comunicador, intentando comprender. Tú, desde la sala de control, le explicas que siente la diferencia entre los dos grandes protocolos de la capa de transporte.

**Pregunta:** Compara los protocolos TCP y UDP y sus características en contexto de la transmisión de datos. ¿Por qué TCP se considera un protocolo confiable y orientado a conexión, y qué implica eso en cuanto a rendimiento? ¿Por qué UDP es no confiable y sin conexión, y en qué casos su rapidez resulta ventajosa?

En tu respuesta, menciona ejemplos de aplicaciones o situaciones galácticas para cada protocolo: por ejemplo, qué tipo de datos enviarías mediante UDP durante una misión crítica, y cuál vía TCP en comunicaciones rutinarias. (Pista: TCP garantiza la entrega de datos completa y ordenada – ideal para transmitir planes estratégicos; UDP minimiza retrasos – útil para enviar coordenadas de combate en tiempo real, aunque alguna pueda perderse.).

## Solución
###  Comparación entre TCP y UDP

| Protocolo | Características | Ventajas | Inconvenientes |
|-----------|---------------|----------|---------------|
| **TCP (Transmission Control Protocol)** | - Orientado a conexión.<br>- Garantiza entrega completa y ordenada.<br>- Usa control de flujo y congestión. | - Fiabilidad total.<br>- Corrección de errores.<br>- Ideal para datos críticos. | - Mayor latencia.<br>- Consumo de recursos más alto.<br>- No apto para transmisiones en tiempo real. |
| **UDP (User Datagram Protocol)** | - No orientado a conexión.<br>- No garantiza entrega ni orden.<br>- Sin control de flujo ni congestión. | - Baja latencia.<br>- Menor consumo de recursos.<br>- Ideal para transmisiones en tiempo real. | - Posible pérdida de paquetes.<br>- No garantiza integridad de datos.<br>- No apto para información crítica. |

###  Funcionamiento de TCP
TCP establece una conexión entre el remitente y el receptor antes de enviar datos. Usa un **handshake de tres vías** para garantizar que ambas partes están listas. Además:
- **Corrige errores** mediante retransmisión de paquetes perdidos.
- **Ordena los datos** para que lleguen en la secuencia correcta.
- **Controla el flujo** para evitar sobrecargar al receptor.

 **Ejemplo galáctico:** La transmisión de los **planos de la Estrella de la Muerte** debe ser precisa y completa. **TCP** asegura que cada bit de información llegue sin errores.

###  Funcionamiento de UDP
UDP no establece conexión previa ni verifica la entrega de paquetes. Es ideal para aplicaciones donde la velocidad es más importante que la precisión:
- **No retransmite paquetes perdidos**, lo que reduce la latencia.
- **No ordena los datos**, lo que lo hace más rápido.
- **No tiene control de congestión**, permitiendo transmisiones fluidas.

 **Ejemplo galáctico:** Durante una batalla, los **streams de vídeo de las cámaras X-Wing** y las **coordenadas de combate** deben enviarse en tiempo real. **UDP** permite que los datos lleguen rápido, aunque algunos paquetes se pierdan.

###  ¿Cuándo usar cada protocolo?
- **TCP**: Para información crítica que debe llegar completa y en orden (**mensajes estratégicos**, **transferencia de datos**).
- **UDP**: Para transmisiones en tiempo real donde la velocidad es clave (**comunicaciones de combate**, **streaming de sensores**).

###  Conclusión
**TCP es como Yoda: sabio, preciso y confiable**, mientras que **UDP es como el Halcón Milenario: veloz, pero con riesgos**. ¡Que la Fuerza de los protocolos te guíe en cada misión! 🚀🔥

---
# 🔐 Misión 5: Comunicación Segura o Lado Oscuro – Criptografía y Seguridad de la Red

## 📖Situación: 
La victoria rebelde depende de que sus comunicaciones permanezcan secretas. Se rumorea que espías imperiales (e incluso usuarios del lado oscuro) intentan interceptar los mensajes de la Alianza. La líder Mon Mothma te encomienda diseñar un protocolo de comunicación cifrado para que los mensajes entre bases rebeldes no puedan ser leídos por el Imperio aunque sean capturados.

**Narrativa:** En la sala de guerra de la base rebelde, Mon Mothma se dirige a ti con semblante serio: "Hemos logrado infiltrar agentes en Coruscant, pero comunicarse con ellos es arriesgado. El Imperio intercepta cualquier señal. Aprendiz, necesitamos que nuestras transmisiones sean indescifrables para el enemigo." A tu lado, C-3PO comenta nerviosamente en más de seis millones de formas de comunicación: "Si caemos en manos imperiales, prefiero que apaguen mis circuitos a revelar nuestros mensajes."

**Recuerda que cifrar es esencial:** usar claves secretas para que sólo los rebeldes autorizados puedan leer un mensaje. También piensas en las dos formas en que esto se puede lograr: con clave simétrica (una misma clave secreta compartida) o con claves públicas/privadas (criptografía asimétrica). Es hora de demostrar tu conocimiento en seguridad.

**Pregunta:** Explica brevemente la diferencia entre cifrado simétrico y cifrado asimétrico en el contexto de las comunicaciones de la Alianza. ¿Cómo funciona cada esquema y qué ventajas ofrece?​

Por ejemplo, si Leia y Luke comparten una frase clave secreta para cifrar sus holomensajes, ¿qué tipo de cifrado es ese? En cambio, si la Alianza quiere enviar un mensaje a un nuevo aliado sin haber intercambiado una clave secreta previamente, ¿cómo podría ayudar el cifrado asimétrico (claves pública/privada) en ese caso? Comenta también sobre la importancia de autenticación y no repudio en los mensajes (cómo podemos estar seguros de que el mensaje no ha sido alterado y proviene realmente de quien dice ser). Finalmente, menciona por qué utilizar un protocolo seguro (como SSH en lugar de Telnet) es crucial al administrar remotamente los equipos de la red rebelde.

## Solución

### Cifrado Simétrico vs. Cifrado Asimétrico

| Tipo de Cifrado | Funcionamiento | Ventajas | Inconvenientes |
|----------------|---------------|----------|---------------|
| **Simétrico** | Usa una única clave secreta compartida para cifrar y descifrar datos. | - Rápido y eficiente.<br>- Menos consumo de recursos.<br>- Ideal para grandes volúmenes de datos. | - La clave debe compartirse de forma segura.<br>- Si la clave es comprometida, toda la comunicación queda expuesta. |
| **Asimétrico** | Usa un par de claves: una pública para cifrar y una privada para descifrar. | - No requiere compartir una clave secreta.<br>- Permite autenticación y no repudio.<br>- Más seguro para comunicaciones abiertas. | - Más lento que el cifrado simétrico.<br>- Mayor consumo de recursos.<br>- No ideal para grandes volúmenes de datos. |

###  Ejemplos Galácticos
- **Cifrado Simétrico:** Si **Leia y Luke** comparten una frase clave secreta para cifrar sus holomensajes, están usando **cifrado simétrico**.
- **Cifrado Asimétrico:** Si la **Alianza Rebelde** quiere enviar un mensaje a un nuevo aliado sin haber intercambiado una clave secreta previamente, pueden usar **cifrado asimétrico** con claves pública/privada.

### Autenticación y No Repudio
Para garantizar que un mensaje no ha sido alterado y proviene realmente de quien dice ser:
- **Autenticación:** Se usa una firma digital para verificar la identidad del remitente.
- **No repudio:** Evita que el remitente niegue haber enviado el mensaje, asegurando su origen legítimo.

### Importancia de Protocolos Seguros
El uso de protocolos seguros es crucial para la administración remota de los equipos de la red rebelde:
- **SSH (Secure Shell)**: Proporciona una conexión cifrada y segura para administrar servidores.
- **Telnet (inseguro)**: Transmite datos en texto plano, permitiendo que sean interceptados por el Imperio.

### Conclusión
La criptografía es esencial para proteger las comunicaciones de la Alianza Rebelde. **El cifrado simétrico es rápido y eficiente**, mientras que **el cifrado asimétrico es más seguro para intercambios abiertos**. Además, la autenticación y el uso de protocolos seguros como **SSH** garantizan que los mensajes no sean interceptados ni alterados. ¡Que la Fuerza de la seguridad te acompañe! 🔥🚀
