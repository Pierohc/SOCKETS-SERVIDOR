# SOCKETS - SERVIDOR: 

libreria que sirve para networking

    import  socket 
    
Se establece un tamaño para el buffer. Cuando se lee información del socket, se leerán y almacenarán hasta 1024 bytes de datos en el buffer de memoria antes de que se procesen o manipulen. 

En resumen, un buffer es una región de memoria utilizada para almacenar datos temporales mientras se transfieren entre dos entidades, como un cliente y un servidor a través de una conexión de red. En el contexto de la programación de sockets en Python, el tamaño del buffer se refiere a la cantidad de datos que se pueden recibir y almacenar en el buffer antes de que se procesen o manipulen. Un tamaño de buffer más grande puede permitir recibir más datos en una sola lectura, mientras que un tamaño de buffer más pequeño puede ser adecuado para procesar los datos rápidamente
    
    sock_buffer = 1024 
    
    
socket.AF_INET se utiliza para especificar que se va a trabajar con direcciones IPv4 al crear un socket en Python. Es una constante que indica la familia de direcciones de Internet y es necesaria para establecer conexiones TCP/IP a través de IPv4.    
El término "data tipo stream" se refiere a un tipo de datos o flujo de datos secuencial en el que los datos se transmiten o procesan en forma continua, sin divisiones o estructura predefinida. En el contexto de la programación de sockets, un socket de tipo stream, como el utilizado en TCP (Transmission Control Protocol), establece una conexión continua y confiable entre dos extremos de comunicación.    
    
    if __name__ = '__main__':
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
 --------------------------------------------------------------------------
 Ojo: 
 
 
Un tuple (también conocido como tupla en español) es una estructura de datos en Python que permite almacenar múltiples elementos en una secuencia ordenada. Es similar a una lista, pero a diferencia de las listas, los tuples son inmutables, lo que significa que no se pueden modificar después de su creación.

Los tuples se definen utilizando paréntesis () y los elementos se separan por comas. Por ejemplo:

    mi_tuple = (1, 2, "Hola", 3.14)
    
    print(mi_tuple[0])  # Imprime: 1
    print(mi_tuple[2])  # Imprime: Hola
En el ejemplo anterior, mi_tuple es un tuple que contiene cuatro elementos: el número entero 1, el número entero 2, la cadena de texto "Hola" y el número decimal 3.14.

Los tuples pueden contener elementos de diferentes tipos de datos y se pueden acceder a sus elementos individualmente mediante la indexación, de manera similar a las listas.

Los tuples son útiles cuando se necesitan almacenar datos que no deben cambiar después de su creación, como coordenadas, valores constantes o elementos relacionados que deben permanecer juntos como un conjunto inmutable. También se utilizan en situaciones en las que se requiere una estructura de datos más liviana o cuando se desea garantizar que los datos no sean modificados accidentalmente.

Existiria un error de sintaxis si se quiere modificar el tuple, por ejemplo luego del ejemplo se pone:

        mi_tuple[0[ = 4

-------------------------------------------------------------------------------------
# ENLACE DE IP CON UN PUERTO PARA OBTENER EL SOCKET DEL SERVIDOR

socket = ip + puerto

El puerto me permite elegir la aplicacion a la quiero entrar, la que quiero usar.

web = puerto 80
correo = puerto 50

La función sock.bind() se utiliza para enlazar un socket a una dirección IP y un puerto específicos en un servidor.

Al enlazar un socket a una dirección IP y un puerto, se establece la "puerta de entrada" a la cual los clientes se conectarán para comunicarse con el servidor. De esta manera, el socket queda asociado a esa dirección IP y puerto en particular.

    server_address = ('0.0.0.0', 5000)  #(direccion ip, puerto)
    print(f"Iniciando servidor en IP {server_address[0]}, con puerto {server_address[1]}")

    sock.bind(server_address)
    
Es equivalente a si pusiera: 
      
      server_ip = '0.0.0.0'
      server_port = 5000
      
      sock.bind(server_ip, server_port)
      
  SOCK.BIND(...) : Es importante destacar que esta función debe llamarse después de crear el socket y antes de comenzar a escuchar o enviar datos a través del socket. Si la operación de enlace es exitosa, el socket estará listo para aceptar conexiones entrantes o enviar datos según su propósito específico (cliente o servidor). En caso de error, se lanzará una excepción que indica el motivo del fallo. 
 
Se utiliza en la programación de sockets en Python para enlazar o asociar un socket a una dirección específica (server_address) en el sistema operativo. Esta función se utiliza principalmente en el lado del servidor para configurar el socket y escuchar conexiones entrantes.

-----------------------------------------------------------------------------------------------
# PONER EL SERVIDOR EN MODO LISTENING(DISPONIBLE PARA RECIBIR CONEXIONES)

      sock.listen(5)
      
La función `sock.listen(5)` se utiliza en la programación de sockets en Python en el lado del servidor para poner el socket en modo de escucha (listening mode) y especificar el número máximo de conexiones entrantes que se permiten en la cola de conexiones pendientes.

Aquí tienes una explicación más detallada de lo que hace `sock.listen(5)`:

1. `sock` es el objeto socket que se ha creado previamente utilizando la función `socket.socket()` y al que se le ha aplicado la función `sock.bind()` para enlazarlo a una dirección.

2. `sock.listen(5)` pone el socket `sock` en modo de escucha, lo cual significa que el socket está preparado para aceptar conexiones entrantes de los clientes.

3. El argumento de `listen()` especifica el tamaño máximo de la cola de conexiones pendientes, es decir, el número máximo de conexiones en espera que se permiten antes de rechazar nuevas conexiones entrantes. En este caso, se ha especificado 5 como valor de ejemplo, lo que significa que el socket aceptará hasta 5 conexiones en espera en la cola.

Una vez que se ha llamado a `sock.listen(5)`, el socket está en modo de escucha y puede aceptar conexiones entrantes mediante la función `sock.accept()`. La función `sock.accept()` bloquea la ejecución del programa hasta que se establece una conexión entrante, momento en el cual se devuelve un nuevo socket para manejar esa conexión específica.

Es importante destacar que `listen()` debe llamarse después de `bind()` y antes de `accept()`. Si se intenta llamar a `accept()` antes de `listen()`, se producirá un error.

--------------------------------------------------------
# ACCEPT: SE RECIBE IP Y PUERTO DEL CLIENTE Y SE CREA UN NUEVO OBJETO DE SOCKET PARA ENVIAR/RECIBIR DATOS

La línea de código `conn, client_address = sock.accept()` se utiliza en la programación de sockets en Python en el lado del servidor para aceptar una conexión entrante y obtener un nuevo socket y la dirección del cliente que ha establecido la conexión.

            conn, client_address = sock.accept()

La variable `client_address` en el contexto de `sock.accept()` contendrá una tupla con dos elementos: la dirección IP del cliente y el número de puerto utilizado en la conexión. Por lo tanto, para acceder a cada uno de estos elementos, se utilizaría la notación de índices de tupla.

`client_address[0]` y `client_address[1]` para acceder a la dirección IP y al número de puerto respectivamente.

Por ejemplo:

    conn, client_address = sock.accept()
    print(client_address[0])  # Imprime la dirección IP del cliente
    print(client_address[1])  # Imprime el número de puerto del cliente

Por otro lado, `conn`es un nuevo objeto socket que representa una conexión específica establecida con un cliente. Se utiliza para enviar y recibir datos de manera individual con ese cliente en particular. Este nuevo objeto de socket es independiente del socket de escucha original y se utiliza para enviar y recibir datos específicamente para esa conexión cliente-servidor.
El nuevo objeto de socket tiene su propio conjunto de métodos y propiedades que se pueden utilizar para interactuar con el cliente, como send() para enviar datos al cliente y recv() para recibir datos del cliente.

--------------------------------------------------------------------------------------------
Creamos una iterativa, como ya enlazamos el tuple y tenemos el socket del servidor, se puso el servidor en modo listening, por lo que esta esperando alguna conexion.
    
Se imprime el mensaje de ello ("Esperando conexiones...")

Al recibir alguna conexion se digita `sock.accept()`, la cual dará valores. Ello lo almacenamos en client_address, variable que obtendra dos valores, la ip del cliente como tambien el puerto. Conn, recibira un nuevo objeto de socket, es independiente del socket de escucha original y se utiliza para enviar y recibir datos específicamente para esa conexión cliente-servidor.

Y se imprime el mensaje que se ha recibido un socket externo, el de un cliente, indicando su ip y el puerto.

     while True:
        print("Esperando conexiones...")
        conn, client_address = sock.accept()
        print(f"Conexion desde: {client_address[0]}:{client_address[1]}")

----------------------------------------------------------------------------------------------------


Se utiliza `conn.recv(SOCK_BUFFER)` para recibir datos del cliente. La variable `conn` representa un objeto de conexión de socket. `SOCK_BUFFER` es una variable que especifica el tamaño del búfer utilizado para recibir los datos.

Luego, se realiza una comprobación con `if data:` para verificar si se ha recibido algún dato del cliente. Si se recibe algún dato, se imprime el mensaje "Recibido" junto con los datos decodificados utilizando el formato UTF-8. A continuación, se utiliza `conn.sendall(data)` para enviar de vuelta los mismos datos al cliente.

En caso de que no se reciba ningún dato (la condición if data: sea falsa), se imprime el mensaje "No hay más datos" y se rompe el bucle while utilizando break, lo que indica que no se recibirán más datos y el bucle se detiene.

         try:
            while True:
                data = conn.recv(SOCK_BUFFER)

                if data:
                    print(f"Recibido {data.decode('utf-8')}")
                    conn.sendall(data)
                else:
                    print("No hay mas datos")
                    break
                    
 --------------------------------------------------------------------------------------------------------

        import socket

        SOCK_BUFFER = 1024


        if __name__ == "__main__":
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)   # DEFINIR EL SOCKET 
            server_address = ('0.0.0.0', 5000)  #CREAR EL TUPLE
            print(f"Iniciando servidor en IP {server_address[0]}, con puerto {server_address[1]}")

            sock.bind(server_address)   # CREAR EL SOCKET(IP + PUERTO)

            sock.listen(5)   # PONER AL SERVIDOR EN MODO ESCUCHA

            while True:
                print("Esperando conexiones...")
                conn, client_address = sock.accept()   # ACEPTA CONEXION CON EL CLIENTE Y ALMACENA SU IP Y PUERTO EN CLIENT ADRESS, CREAR EL CONN
                print(f"Conexion desde: {client_address[0]}:{client_address[1]}")

                try:
                    while True:
                        data = conn.recv(SOCK_BUFFER)   # RECIBE DATA DEL CLIENTE, DE UN CIERTO TAMAÑO (SOCK_BUFFER)

                        if data:
                            print(f"Recibido {data.decode('utf-8')}")
                            conn.sendall(data)          # EL SERVIDOR DEVUELVE LA DATA AL CLIENTE
                        else:
                            print("No hay mas datos")
                            break
                except ConnectionResetError:             #EXCEPCION
                    print("El cliente ha cerrado la conexion de forma abrupta")
                finally:
                    print("El cliente ha cerrado la conexion")
                    conn.close()                          #SE CIERRA LA CONEXION CON EL CLIENTE POR MEDIO DEL OBJETO CREADO(CONN)

El primer while es para esperar conexion con un cliente, el que sigue que esta dentro el try es para recibir los datos que envie el cliente, luego se procede a enviarselos de nuevo o sino a indicar que no hay datos, tambien existe una exepcion, y por ultimo siempre se mostrata al final de todoo ello lo del finally, para indicar que el cliente con el que se hizo conexion al principio del while, ha cerrado la conexion.

Es importante destacar que el bloque except está ubicado después del bucle while True, lo que significa que cualquier excepción de tipo ConnectionResetError que ocurra dentro del bucle será capturada y manejada, permitiendo que el bucle continúe su ejecución en caso de otros errores no relacionados con la conexión.

El bloque finally se ejecuta siempre, independientemente de si se captura una excepción o no. En este caso, se imprime el mensaje "El cliente ha cerrado la conexión" y se cierra la conexión utilizando el método `conn.close()` del objeto de conexión conn.

En resumen, el código intenta recibir datos del cliente de forma continua, los procesa y los envía de vuelta. Si el cliente cierra la conexión de forma abrupta, se maneja la excepción y se cierra la conexión de manera adecuada. El bloque finally se utiliza para realizar acciones que deben ejecutarse siempre, como cerrar la conexión.


















