# Solución del Examen de Redes
### Pregunta 1
- Describe brevemente las principales diferencias entre el modelo OSI y el modelo TCP/IP (número de capas, orientación y tratamiento de la capa de aplicación).

|OSI | TCP/IP |
|-|-|
|7 capas |4 capas |
|Centrado en conexiones (TCP) |No centrado en conexiones (TCP o UDP) |
|Modelo no práctico |Modelo práctico |
|Ruteo de paquetes en capa Red |Ruteo de paquetes en capa Internet |
|Se pueden definir protocolos en cada capa |Protocolos estandarizados |

- Explica el rol de la capa de transporte en la comunicación de redes y compara los protocolos TCP y UDP en términos de:
  - Orientación a conexión
  - Fiabilidad y control de errores
  - Velocidad y aplicaciones típicas
 
La capa de transporte se encarga de transmisión de datos entre aplicaciones.

|TCP | UDP |
|-|-|
|Orientado a conexiones |No orientado a conexiones |
|Control de errores (Cada paquete necesita confirmación del recipiente) |Ningún control de errores (A veces checksum) |
|Mas lento |Mas rápido |
|Para situaciones donde no puede haber datos incorrectos (texto, archivos) |Para cuando hay que transmtir datos rápidamente (streaming) |

### Pregunta 2
- Describe el proceso completo de resolución de nombres en el Sistema de Nombres de Dominio (DNS), desde que un usuario ingresa una URL hasta que se establece la conexión con el servidor web.

El usuario ingresa la URL, el rúter busca en su tabla si corresponde a una dirección IP. Si no, hace un request a su correspondiente servidor DNS. Si todavía no se encuentra, se busca por el domain (.com, .net, .es) y el servidor correspondiente manda la dirección IP. Esto se hace usando UDP para que sea un proceso mas rápido.

- Compara el funcionamiento de HTTP y FTP, haciendo hincapié en:
  - El método de conexión (un único canal vs. dos conexiones para control y datos)
  - Las principales aplicaciones de cada uno
  
|HTTP | FTP |
|-|-|
|Solo usa un canal para datos |Dos canales para control y datos |
|Para transferir páginas web por el internet |Para transferir archivos |
|Mas rápido |Mas lento |

### Pregunta 3
- calcula la tasa de transmisión máxima para un canal con un ancho de banda de 400 MHz y una relación señal a ruido de 15 dB. (Recuerda que para convertir de dB a escala lineal.

0,4 x log2(10^(15/10)) = 1,993156857 GHz

- En un sistema en el que la primera portadora se sitúa a 1.2 GHz y cada canal ocupa 300 MHz, determina la frecuencia de la portadora inmediatamente anterior y la inmediatamente posterior. Explica la importancia de esta asignación para la eficiencia espectral.

Con espacios de 300MHz, la portadora anterior es 1,2 - 0,3 = 0,9GHz y la posterior es 1,2 + 0,3 = 1,5GHz. Esta separación evita interferencia entre canales al coste de no tener eficiencia máxima.

- Explica brevemente el funcionamiento del Algoritmo de Dijkstra para encontrar la ruta más corta en un grafo ponderado y compáralo con el método de enrutamiento por inundación (Flooding), señalando ventajas y desventajas de cada enfoque.

El Algoritmo de Dijkstra usa vértices, con los nodos no visitados teniendo un valor infinito, y el nodo fuente teniendo un valor de 0. Luego va al nodo con distancia mínima, asignándolo como nodo actual. Sigue con este método, acumulando los valores de distancia, hasta llegar al nodo objetivo de manera óptima.  
El método por Inundación manda el paquete por todas las rutas disponibles, y escoge la más corta. Sus ventajas son que es un método simple y que siempre encuentra la ruta mas corta. La desventaja es que crea mucho tráfico en la red, y el volumen de paquetes puede crear errores.

### Pregunta 4
- Para la red 192.168.10.0/24, determina:
  - La dirección de broadcast.
  - El rango de direcciones válidas (primera y última dirección de host).

Broadcast: 192.168.10.255
Rango: 192.168.10.1-254

- Explica cómo se calcula el número de hosts disponibles en una subred y, aplicándolo a una red con máscara 255.255.255.192, indica cuántos equipos (hosts) se pueden conectar.

Primero, la máscara se convierte a binario: 11111111.11111111.11111111.11000000. Hay 6 0´s disponibles, así que hay 2^6-2 hosts disponibles (quitando dirección de red y broadcast). Hay 62 hosts disponibles.

### Pregunta 5
- Describe el proceso de establecimiento de conexión en TCP (Three-Way Handshake) y, a continuación, el proceso de terminación de conexión (Four-Way Handshake). Explica la importancia de cada fase.

Establecimiento  
El emisor manda un paquete al puerto TCP del receptor pidiendo una conexión TCP (Sin esto no pueden contactar). El receptor manda un paquete reconociendo el paquete del emisor para aceptar la solicitud (Así solo hay comunicación si los dos lados lo quieren). Finalmente, El emisor manda un paquete reconociendo el paquete del emisor (Cada paquete necesita ser reconocido para asegurar que no hay errores).

Terminación  
EL emisor que quiere terminar la correspondencia manda un paquete solicitándolo (Sin esto no se puede terminar). El receptor reconoce este paquete (Para evitar errores). El receptor también manda un paquete solicitando terminación (Así los dos están de acuerdo que quieren terminar). El emisor lo reconoce, y terminan la conexión (Otra vez evitando errores).

- Para un enlace con los siguientes parámetros:
  - RTT = 40 ms
  - Ancho de banda = 50 Mbps
  - MSS = 1,460 bytes
- Utilizando la relación calcula el tamaño óptimo de la ventana en bits y en bytes, y estima aproximadamente el número de segmentos MSS que pueden estar en tránsito simultáneamente.

0.04 s * 50.000.000 bps = 2.000.000 bits / 8 = 250.000 bytes
250.000 / 1.460 bytes por segmento ~= 171 segmentos

- Compara brevemente el cifrado simétrico y asimétrico (en cuanto al número de claves, velocidad y aplicaciones).
|Simétrico | Asimétrico |
|-|-|
|Receptor y emisor usan la misma clave |Receptor y emisor tienen sus propias claves (doble) |
|Mas rápido |Mas lento |
|Menos seguro |Mas seguro |
|Cifrar muchos datos (VPN, archivos) |Cifrar con mas seguridad (Criptomonedas, correo seguro) |

- Describe el funcionamiento básico del algoritmo RSA, incluyendo la generación de claves y el proceso de cifrado/descifrado. (Puedes ilustrar el proceso con un ejemplo numérico sencillo, por ejemplo usando...

El algoritmo RSA usa números primos grandes. Luego sacas el producto de los números, y encuentras otro número que no tiene factores comunes con (p - 1) x (q - 1). Finalmente calculas el número que, cuando se multiplica con este y se resta 1, es igual a (p - 1) x (q - 1). La clave pública es el producto original con el número sin factores comunes, y la privada es el producto con el último número.

p = 3. q = 11. n = p x q = 33. (p - 1)(q - 1) = 20.  
e no puede tener factores comunes con 20. e = 7.  
e x d - 1 = 20. d = 3.  
clave pública = (n, e). clave privada (n, d).

- Explica qué es un firewall y menciona dos tipos (por ejemplo, filtrado de paquetes y firewall de estado), indicando cómo contribuyen a la protección de la red.

Un firewall es un dispositivo que separa la red externa y la interna.
Un firewall puede filtrar paquetes, observando sus IPs de fuente y destino, el protocolo, y números de puerto para decidir si pueden pasar. De esta manera, ciertos protocolos pueden ser prevenidos mientras que otros pueden pasar sin problema.
Un firewall también puede observar los estados de redes conectadas. Una versión mas tradicional de firewall. Con esto, se pueden buscar anomalías y tomar acciones.

- Menciona brevemente la función de VPN e IPSec en el aseguramiento de la comunicación.

IPSec es un conjunto de protocolos para mantener seguridad en conexiones
### **Pregunta 6. Cálculo de Direcciones de Subred**

#### a) Primera dirección de subred para `192.168.1.0/26`:
1. **Bloque**: Los primeros 26 bits definen el bloque. La primera subred es `192.168.1.0/26`.

#### b) Dirección de broadcast de la primera subred:
1. **Bits de host**: Los últimos 6 bits son para hosts.
2. **Dirección de broadcast**: Se llenan los bits de host con `1`. La dirección de broadcast es `192.168.1.63`.

---

### **Pregunta 7. División de Redes en Subredes**

#### a) División de la red `10.0.0.0/24` en 8 subredes:
1. **Bits prestados**: Se necesitan 3 bits para crear 8 subredes (\(2^3 = 8\)).
2. **Nueva máscara**: La nueva máscara es `/27`.

#### b) Rango de direcciones de la primera subred:
1. **Primera dirección**: `10.0.0.0`.
2. **Última dirección válida**: `10.0.0.30`.
3. **Dirección de broadcast**: `10.0.0.31`.

---

### **Pregunta 8. Cálculo de Direcciones Válidas**

#### a) Dirección válida para la subred `172.16.0.0/20`:
1. **Rango de direcciones**: Desde `172.16.0.1` hasta `172.16.15.254`.
2. **Dirección de broadcast**: `172.16.15.255`.

#### b) Número de hosts válidos:
1. **Bits de host**: 12 bits.
2. **Hosts válidos**: \(2^{12} - 2 = 4,094\).

---
## Parte III: Capa de Red

### **Pregunta 9. Cálculo de Ruta Más Corta**

#### a) Funcionamiento del Algoritmo de Dijkstra:
El algoritmo de Dijkstra encuentra la ruta más corta en un grafo ponderado siguiendo estos pasos:
1. Inicializa la distancia desde el nodo origen a todos los demás nodos como infinita, excepto el origen, que tiene distancia 0.
2. Marca todos los nodos como no visitados.
3. Selecciona el nodo no visitado con la menor distancia y actualiza las distancias de sus vecinos.
4. Repite el proceso hasta que todos los nodos hayan sido visitados o se alcance el destino.

#### b) Comparación con el enrutamiento por inundación (Flooding):
| **Aspecto**              | **Dijkstra**                          | **Flooding**                          |
|--------------------------|---------------------------------------|---------------------------------------|
| **Ventajas**             | Encuentra la ruta más corta de manera eficiente. | No requiere conocimiento previo de la red. |
| **Desventajas**          | Requiere información completa del grafo. | Genera un alto tráfico en la red. |

---

### **Pregunta 10. Cálculo de Direcciones de Broadcast y Rango de Hosts**

#### a) Dirección de broadcast para la subred `172.29.152.0` con máscara `255.255.248.0`:
1. **Máscara en binario**: `11111111.11111111.11111000.00000000`.
2. **Bits de host**: Los últimos 11 bits son para hosts.
3. **Dirección de broadcast**: Se llenan los bits de host con `1`.
   - Dirección en binario: `10101100.00011101.10011111.11111111`.
   - Dirección en decimal: `172.29.159.255`.

#### b) Rango de direcciones válidas para el host `172.22.53.199` con máscara `255.255.252.0`:
1. **Máscara en binario**: `11111111.11111111.11111100.00000000`.
2. **Bits de host**: Los últimos 10 bits son para hosts.
3. **Primera dirección válida**: `172.22.52.1`.
4. **Última dirección válida**: `172.22.55.254`.

---

### **Pregunta 11. Última Dirección Válida y Cálculo de Hosts**

#### a) Última dirección válida para la subred `172.30.67.192` con máscara `255.255.255.192`:
1. **Máscara en binario**: `11111111.11111111.11111111.11000000`.
2. **Bits de host**: Los últimos 6 bits son para hosts.
3. **Dirección de broadcast**: `172.30.67.255`.
4. **Última dirección válida**: `172.30.67.254`.

#### b) Número total de direcciones y hosts para la red `172.26.0.0` con máscara `255.255.255.192`:
1. **Bits de host**: 6 bits.
2. **Total de direcciones**: \(2^6 = 64\).
3. **Hosts válidos**: \(64 - 2 = 62\).

---

### **Pregunta 12. Segmentación en Subredes**

#### a) Determinar el bloque de una subred para `172.18.171.190/23`:
1. **Máscara en binario**: `11111111.11111111.11111110.00000000`.
2. **Bloque**: Los primeros 23 bits definen el bloque. La subred es `172.18.170.0/23`.

#### b) Uso de la fórmula para calcular subredes:
\[
\text{Número de subredes} = 2^s
\]
Donde \(s\) es el número de bits prestados. Si se requieren al menos 4 subredes:
1. \(s = 2\) (porque \(2^2 = 4\)).
2. Se toman 2 bits de los bits de host para definir las subredes.

---

## Parte IV: Capa de Transporte

### **Pregunta 13. Establecimiento y Terminación de Conexión en TCP**

#### a) Establecimiento de conexión (Three-Way Handshake):
El proceso consta de tres pasos:
1. **SYN**: El cliente envía un segmento con el flag `SYN` activado para iniciar la conexión.
2. **SYN-ACK**: El servidor responde con un segmento que tiene los flags `SYN` y `ACK` activados.
3. **ACK**: El cliente envía un segmento con el flag `ACK` activado, confirmando la conexión.

**Importancia**: Este proceso asegura que ambas partes estén listas para comunicarse y sincroniza los números de secuencia.

#### b) Terminación de conexión (Four-Way Handshake):
El proceso consta de cuatro pasos:
1. **FIN**: Una de las partes (cliente o servidor) envía un segmento con el flag `FIN` activado para indicar que desea terminar la conexión.
2. **ACK**: La otra parte responde con un segmento `ACK`, confirmando la recepción del `FIN`.
3. **FIN**: La segunda parte envía su propio segmento `FIN`.
4. **ACK**: La primera parte responde con un segmento `ACK`, confirmando la terminación.

**Importancia**: Este proceso asegura que ambas partes cierren la conexión de manera ordenada, evitando pérdida de datos.

---

### **Pregunta 14. Multiplexación y Demultiplexación en TCP**

#### a) Multiplexación descendente:
La multiplexación descendente permite que múltiples aplicaciones en un dispositivo envíen datos a través de una única conexión de red. TCP utiliza números de puerto para identificar cada aplicación.

**Ejemplo**: Un servidor web puede atender múltiples solicitudes HTTP simultáneamente, asignando un puerto único a cada conexión.

#### b) Multiplexación ascendente:
La multiplexación ascendente permite que los datos recibidos en una conexión de red se distribuyan a las aplicaciones correspondientes en el dispositivo receptor, utilizando los números de puerto.

**Relevancia**: Es esencial para que múltiples aplicaciones puedan recibir datos simultáneamente sin interferencias.

## Parte IV: Cálculo del Tamaño de Ventana y Congestión

### **Pregunta 15. Cálculo del Tamaño de Ventana y Congestión**

#### a) Conversión de unidades:
- **RTT**: 50 ms = \(50 \times 10^{-3}\) segundos = 0.05 segundos.
- **Ancho de banda**: 100 Mbps = \(100 \times 10^6\) bits por segundo.
- **MSS**: 1,500 bytes = \(1,500 \times 8 = 12,000\) bits.

#### b) Tamaño óptimo de la ventana:
\[
\text{Ventana óptima} = \text{Ancho de banda} \times \text{RTT}
\]
Sustituyendo los valores:
\[
\text{Ventana óptima} = 100 \times 10^6 \times 0.05 = 5 \times 10^6 \, \text{bits}
\]
En bytes:
\[
\text{Ventana óptima} = \frac{5 \times 10^6}{8} = 625,000 \, \text{bytes}
\]

#### c) Número de segmentos MSS en tránsito:
\[
\text{Segmentos en tránsito} = \frac{\text{Ventana óptima en bytes}}{\text{MSS}}
\]
Sustituyendo los valores:
\[
\text{Segmentos en tránsito} = \frac{625,000}{1,500} \approx 416.67 \, \text{segmentos}
\]
Aproximadamente **416 segmentos MSS** pueden estar en tránsito simultáneamente.

#### d) Relación con el control de congestión:
El tamaño de ventana óptimo es crucial para evitar congestión en TCP. Si la ventana es demasiado grande, puede saturar la red, mientras que una ventana pequeña limita el rendimiento. TCP ajusta dinámicamente la ventana para equilibrar la eficiencia y evitar congestión.

---

### **Pregunta 16. Mecanismos de Control de Congestión en TCP**

#### **Algoritmo de Arranque Lento (Slow Start)**:
- **Objetivo**: Evitar saturar la red al inicio de la conexión.
- **Funcionamiento**: La ventana de congestión comienza con un tamaño pequeño y se incrementa exponencialmente hasta alcanzar el umbral de congestión.

#### **Algoritmo de Nagle**:
- **Objetivo**: Reducir el número de pequeños paquetes enviados.
- **Funcionamiento**: Agrupa pequeños paquetes en uno más grande antes de enviarlo, optimizando el uso del ancho de banda.

#### **Algoritmo de Clark**:
- **Objetivo**: Evitar el envío de paquetes pequeños cuando hay datos pendientes.
- **Funcionamiento**: Retrasa el envío de paquetes pequeños hasta que se acumule suficiente información.

---

## Parte V: Capa de Aplicación y Aplicaciones Multimedia

### **Pregunta 17. Protocolos de Correo y Funcionamiento de HTTP/FTP**

#### a) Comparación de POP3, IMAP y SMTP:
| **Protocolo** | **Función** | **Modo de operación** | **Ejemplo de uso** |
|---------------|-------------|-----------------------|--------------------|
| **POP3**      | Recuperar correos. | Descarga y elimina correos del servidor. | Cliente de correo local. |
| **IMAP**      | Recuperar correos. | Sincroniza correos entre servidor y cliente. | Acceso desde múltiples dispositivos. |
| **SMTP**      | Enviar correos.    | Transfiere correos entre servidores. | Envío de correos electrónicos. |

#### b) Funcionamiento de HTTP y FTP:
- **HTTP**:
  - Utiliza métodos como `GET`, `POST`, `PUT`, `DELETE` para interactuar con recursos web.
  - Usa una única conexión para enviar solicitudes y recibir respuestas.

- **FTP**:
  - Usa dos conexiones: una para control y otra para transferencia de datos.
  - Permite transferir archivos entre cliente y servidor.

---

### **Pregunta 18. Streaming y VoIP**

#### a) Tipos de streaming:
| **Tipo**               | **Definición** | **Ejemplo** |
|------------------------|----------------|-------------|
| **UDP Streaming**      | Transmisión rápida sin garantía de entrega. | Streaming en tiempo real. |
| **HTTP Streaming**     | Usa HTTP para transferir contenido multimedia. | YouTube. |
| **Adaptive HTTP Streaming (DASH)** | Ajusta la calidad según el ancho de banda disponible. | Netflix. |

#### b) Funcionamiento de VoIP:
- **Proceso**: Convierte la voz en paquetes de datos, los transmite por la red y los reconstruye en el receptor.
- **Problemas comunes**:
  - **Retardo**: Solución: Usar redes de baja latencia.
  - **Pérdida de paquetes**: Solución: Implementar retransmisión o corrección de errores.

---

### **Pregunta 19. Control de Congestión en Redes Multimedia y Modelos de Calidad de Servicio**

#### a) Técnicas para evitar congestión:
1. **Buffering en el cliente**: Almacena datos antes de reproducirlos para evitar interrupciones.
2. **Marcado de paquetes mediante DiffServ**: Prioriza paquetes según su importancia.

#### b) Comparación de modelos:
| **Modelo**       | **Tráfico** | **Garantía de calidad** | **Ejemplo** |
|------------------|-------------|-------------------------|-------------|
| **Best-Effort**  | No prioriza tráfico. | Sin garantía. | Navegación web. |
| **Servicios Multiclase** | Prioriza tráfico según clases. | Garantía parcial. | Streaming multimedia. |

---

## Parte VI: Seguridad en Redes

### **Pregunta 20. Problemas Críticos de Seguridad y Soluciones**

| **Área**          | **Descripción** | **Solución** |
|-------------------|-----------------|--------------|
| **Confidencialidad** | Proteger datos de accesos no autorizados. | Cifrado (AES). |
| **Autenticación**   | Verificar identidad. | Certificados digitales. |
| **No repudio**      | Garantizar que el remitente no pueda negar el envío. | Firmas digitales. |
| **Integridad**      | Asegurar que los datos no sean modificados. | Hashing (SHA-256). |

---

### **Pregunta 21. Cifrado Simétrico vs. Asimétrico**

| **Aspecto**         | **Simétrico** | **Asimétrico** |
|---------------------|---------------|----------------|
| **Número de claves** | 1 clave.      | 2 claves (pública y privada). |
| **Velocidad**        | Más rápido.   | Más lento. |
| **Ejemplos**         | AES, DES.     | RSA, ECC. |
| **Aplicaciones**     | Cifrado de datos. | Firmas digitales. |

---

### **Pregunta 22. Funcionamiento del Algoritmo RSA**

#### a) Proceso de generación de claves:
1. Seleccionar dos números primos (\(p\) y \(q\)).
2. Calcular \(n = p \times q\).
3. Calcular \(\phi(n) = (p-1) \times (q-1)\).
4. Elegir \(e\) tal que \(1 < e < \phi(n)\) y \(e\) sea coprimo con \(\phi(n)\).
5. Calcular \(d\) tal que \(d \times e \mod \phi(n) = 1\).

#### b) Ejemplo numérico:
- \(p = 3\), \(q = 11\), \(e = 7\), \(M = 4\).
- \(n = 3 \times 11 = 33\).
- \(\phi(n) = (3-1) \times (11-1) = 20\).
- \(d = 3\) (porque \(7 \times 3 \mod 20 = 1\)).
- **Cifrado**: \(C = M^e \mod n = 4^7 \mod 33 = 16\).
- **Descifrado**: \(M = C^d \mod n = 16^3 \mod 33 = 4\).

---

### **Pregunta 23. Firewalls, VPN, IPSec y SSL/TLS**

#### a) Firewalls:
- **Filtrado de paquetes**: Inspecciona cada paquete según reglas predefinidas.
- **Firewall de estado**: Monitorea el estado de las conexiones activas.

#### b) VPN vs. IPSec:
| **Aspecto** | **VPN** | **IPSec** |
|-------------|---------|-----------|
| **Propósito** | Crear redes privadas. | Proteger datos en redes públicas. |
| **Modo de operación** | Túneles cifrados. | Cifrado de paquetes. |

#### c) SSL/TLS:
- **Funcionamiento**: Establece un canal cifrado entre cliente y servidor.
- **Importancia**: Protege datos sensibles en comunicaciones web.

---

### **Pregunta 24. DNS Spoofing y Protección con DNSSEC**

#### a) DNS Spoofing:
- **Descripción**: Ataque que redirige a usuarios a sitios falsos mediante respuestas DNS manipuladas.
- **Impacto**: Compromete la integridad de las comunicaciones.

#### b) DNSSEC:
- **Descripción**: Usa firmas digitales para verificar la autenticidad de las respuestas DNS.
- **Beneficio**: Previene ataques de suplantación.
