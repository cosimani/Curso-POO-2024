.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 03 - POO 2024
===================
(Fecha: 18 de marzo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Clases 2021 <https://www.youtube.com/watch?v=dH0WqMW3-_w>`_ 


Cadena de caracteres
^^^^^^^^^^^^^^^^^^^^

- Al estilo C	

.. code-block:: c

	#include <string.h>

	char cadena1[ 30 ], cadena2[ 30 ];
	strcpy( cadena1, "Hola" );
	cin >> cadena2;
	
- Con C++ usamos   

.. code-block:: c

	#include<string>

	Asignación       s1 = s2    s1 = "Hola"
	Concatenación    s1 = s2 + s3	
	Comparación      if ( s1 == s2 )
	Subcadenas       s1.substr( 3, 5 )
	Longitud         s1.length()    s2.size()  // Son lo mismo
	Acceso a char    s1[ 2 ]    s2.at( 2 )  // Lanza out_of_range
	Limpiar          s1.clear()
	Busca cadena     s1.find( "cadena" );    s1.find( s2 );
	Puntero a char   const char *c = s1.c_str()



Punteros
========

**Declaración**

.. code-block:: c

	int * entero;     // entero es un puntero a int
	char * caracter;  // puntero a char

	entero      es el puntero
	*entero     es el contenido


**Punteros a variables**

.. code-block:: c

	int entero;         // entero es una variable int
	int * pEntero;      // pEntero es un puntero a int
	pEntero = &entero;  // &entero es la dirección de memoria donde se almacena entero

**Arrays y punteros**

.. code-block:: c

	int miArray[ 10 ];	// miArray es como un puntero al primer elemento
	int* puntero;

	puntero = miArray;  // similar a:  puntero = &miArray[0];
	( *puntero )++;     // equivale a miArray[0]++;  // incrementa
	puntero++;          // equivale a &miArray[1];   // se mueve una posición

	puntero = puntero + 3;  // se desplaza 3 posiciones int






Clases
======

.. code-block:: c

	class Poste  {
	    // Lista de miembros (generalmente funciones y datos)
	    // Los datos no pueden ser inicializados fuera del constructor 
	    // Si las funciones se definen fuera, se usa el operador :: 
	    // :: es el operador de acceso a ámbito
	};


.. code-block:: c

	class Poste;  // Esto es la declaración de una clase.

.. code-block:: c

	class Poste  {  // Esto es la declaración y definición de una clase.
	     
	};




**Ejemplo:**

.. code-block:: c

	#include <iostream>
	
	class Poste  {
	private:
	    // Datos miembro de la clase Poste. También llamados atributos.
	    int altura;
	    int seccion;
		
	public:
	    // Funciones miembro de la clase Poste. Llamados también métodos.
	    void getDatos( int & a, int & s );
	    void setDatos( int a, int s )  {
	        altura = a;
	        seccion = s;
	    }
	};

	void Poste::getDatos( int & a, int & s )  {
	    a = altura;
	    s = seccion;
	}

	int main()  {
	    Poste poste;
	    int x, y;  // Variables donde se copiarán los valores de poste

	    poste.setDatos( 12, 32 );
	    poste.getDatos( x, y );

	    cout << "(" << x << “, ” << y << “)” << endl;
	}
	
	// La función "setDatos()" se definió en el interior de la clase (lo haremos sólo cuando
	// la definición sea muy simple, ya que dificulta la lectura y comprensión del programa). 

**Constructor**

.. code-block:: c

	class Poste  {
	private:
	    int altura;
	    int seccion;

	public:
	    Poste( int a, int s );

	    void getDatos( int & a, int & s );
	    void setDatos( int a, int s );
	};

	Poste::Poste( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

	void Poste::getDatos( int & a, int & s )  {
	    a = altura;
	    s = seccion;
	}

	void Poste::setDatos( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

**Cuestiones sobre declaraciones**

.. code-block:: c

	Poste poste;  // Llama al constructor sin parámetros. En esta última versión 
	              // de Poste, esto no serviría, ya que no hay constructor sin parámetros. 
	              // Si no se especifica un constructor, el compilador crea uno. 
	              // Por lo tanto, esta declaración sirve para una clase Poste 
	              // donde el programador no escriba constructor, o escriba uno sin recibir parámetros.

	Poste poste();  // Se entiende como el prototipo de una función sin parámetros que 
	                // devuelve un objeto Poste. Es decir, no sirve para instanciar un 
					// objeto con el contructor sin parámetros de Poste.

	Poste poste1( 12, 43 );  // Válido
	Poste poste2( 45, 34 );  // Válido


**Inicialización de objetos**

.. code-block:: c

	// Lo siguiente se permite y funciona casi siempre, (salvo cuando usemos const, que
	// veremos más adelante). Hay que tener presente que aquí, primero se reserva lugar 
	// en memoria para altura y seccion conteniendo basura y luego se le asignan los 
	// valores que vienen en los parámetros del constructor.
	Poste( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

	// La siguiente sería la manera más correcta de inicializar los atributos de un 
	// objeto. En este caso, altura y seccion nunca contienen basura, sino que 
	// directamente se crean en memoria con el valor que vienen en los parámetros del constructor.
	Poste::Poste( int a, int s ) : altura( a ), seccion( s )  {  }

	Poste::Poste() : a( 0 ), b( 0 )  {  }

**El puntero this**

- Es un puntero que ya se exite dentro del ámbito de una clase y apunta al propio objeto instanciado.
- Se utiliza para acceder a los atributos y métodos.

.. code-block:: c

	class Poste  {
	private:
	    int altura;
	    int seccion;

	public:
	    Poste( int altura, int seccion );

	    void getDatos( int & altura, int & seccion );
	    void setDatos( int altura, int seccion );
	};

	Poste::Poste( int altura, int seccion ) : altura( altura ), seccion( seccion )  {  
	}

	void Poste::getDatos( int & altura, int & seccion )  {
	    altura = this->altura;
	    seccion = this->seccion;
	}

	void Poste::setDatos( int altura, int seccion )  {
	    this->altura = altura;
	    this->seccion = seccion;
	}


**Destructor**

.. code-block:: c

	Poste::~Poste()  {
	    altura = 0;  
	    seccion = 0;
	}
	
	




Ejercicio 1:
============

- Instalar Qt. Lo cual incluye las herramientas de compilación C++, la biblioteca Qt y Qt Creator.
- Crear un primer programa que muestre por la consola de QtCreator 10 números aleatorios en el intervalo [ 2, 20 ]
- Cada vez que se ejecute el programa, los números deberán ser aleatorios y distintos en cada ejecución.


Ejercicio 2:
============

Objetivo: Familiarización con librerías, archivos DLL y variable de entorno PATH. Tener presente la distinción entre biblioteca, librería y library.

Descripción: Crear un programa simple en C++ que utilice una librería externa (en forma de archivo DLL o similar en otros sistemas operativos) y que haga uso de la variable de entorno PATH para ubicar dicha librería.

Pasos a seguir:

a. Crear una librería en C++ y compilarla como un archivo DLL 8o similar en otros sistemas operativos). Programar en la librería una función que imprima un mensaje simple, como "Hola, desde la biblioteca".

b. Crear un programa principal en C++ que utilice esta librería. Hacer referencia (o linkear) a la librería de manera dinámica.

c. Incluir la ruta al archivo DLL en la variable de entorno PATH.

d. En el programa principal, cargar la librería, invocar a la función y mostrar el mensaje.


Ejercicio 3:
============

- Elija un nombre para su propio espacio de nombres para todo lo que se haga en este asignatura
- Luego de elegido el nombre para su namespace, defina una función dentro de ese namespace para devolver el número de versión junto con la fecha de la última actualización de la biblioteca

.. code-block:: c

	QString getVersion();  // Devuelve un texto como "v0.0.1 - 20240318"


Ejercicio 4:
============

- Crear un std::vector para contener int
- Cargar 30 valores pseudo aleatorios entre 1 y 15
- Publicar la moda


Ejercicio 5:
============

- Crear un std::vector para contener objetos de la clase std::string
- Cargar 5 expresiones idiomáticas, como por ejemplo: pan comido
- Publicar por consola ordenado alfabéticamente


Ejercicio 6:
============

- En un Empty qmake Project
- Crear una nueva clase (que no sea Persona, ni Cliente, ni Poste). Invente una clase.
- Agregar uno o más constructores, agregar sus métodos y sus atributos
- Crear algunos objetos de esta clase en la función main

Ejercicio 7:
============

- Empty qmake Project
- Utilizar la clase creada en el ejercicio anterior para crear objetos y almacenarlos en un ``std::vector``
- ¿Se pueden ordenar? Qué estrategia utilizaría para ordenarlos de menor a mayor



Aclaraciones:
=============

- Todos los ejercicios serán actualizados en un repositorio en GitHub
- Escribir el README con contenido para poder ejecutar los ejercicios
- Cada ejercicio tendrá su propia carpeta ejercicio01, ejercicio02, ...
- Que cada ejercicio debe contener todo lo necesario para poder compilarlo y ejecutarlo.
- Excluir los archivos y carpetas que no sean necesarios, como se el archivo con extensión .pro.user y la carpeta build-

