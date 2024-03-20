.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 04 - POO 2024
===================
(Fecha: 20 de marzo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Función genérica 2021 <https://www.youtube.com/watch?v=PkmAW31KuV0>`_ 

`Función genérica - arrays - string - punteros 2022 <https://www.youtube.com/watch?v=gdrMyvjf7M4>`_ 

`getDatos de Poste - Convenciones 2021 <https://www.youtube.com/watch?v=7l0QZzqbQjI>`_

`Introducción a Qt 2021 <https://www.youtube.com/watch?v=JYADonAlKPc>`_

`Primer aplicación en Qt 2021 <https://www.youtube.com/watch?v=krfWC8mWTQM>`_




Función Genérica
================

- Supongamos que debemos implementar una función que imprima en la salida los valores de un array de enteros:

.. code-block:: c

	void imprimir ( int v[], int cantidad )  {
	    for ( int i = 0 ; i < cantidad ; i++ )
	        std::cout << v[ i ] << " ";
	    std::cout << std::endl;
	}

	int main( int, char ** )  {
	    int v1[ 5 ] = { 5, 2, 4, 1, 6 };
	    imprimir( v1, 3 );

	    return 0;
	}

- Ahora necesitamos la impresión de un array de float

.. code-block:: c

	void imprimir( float v[], int cantidad );

- Vemos que las versiones se diferencian por el tipo de datos del array. Entonces podemos utilizar lo siguiente:

.. code-block:: c

	template < class T > void imprimir ( T v[], int cantidad )  {
	    for ( int i=0 ; i < cantidad ; i++ )
	        std::cout << v[ i ] << " ";
	    std::cout << std::endl;
	}

	int main( int, char ** )  {
	    int v1[ 5 ] = { 5, 2, 4, 1, 6 };
	    float v2[ 4 ] = { 2.3, 5.1, 0, 2 };

	    imprimir( v1, 5 );  // qué pasa si pongo cantidad 10 -> Publica basura
	    imprimir( v2, 2 );

	    return 0;
	}

- El compilador utiliza el código de la función genérica como plantilla para crear automáticamente dos funciones sustituyendo T por el tipo de dato concreto.

.. code-block:: c

	Con T = int     utiliza -->     void imprimir( int v[], int cantidad )

	Con T = float   utiliza -->     void imprimir( float v[], int cantidad )

- Aquí, la única operación que realizamos sobre los valores de tipo T es:

.. code-block:: c

	std::cout << v[ i ]

- Esto pone una restricción, ya que sólo se admitirá los tipos de datos para los que se puedan imprimir en pantalla con:

.. code-block:: c

	std::cout <<



Revisión de la clase Poste
==========================

**¿ Cómo funciona el método getDatos() ?**


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



Convenciones para escribir nuestro código
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Los nombres de las clases, structs y enum comienzan con mayúsculas (usando ``UpperCamelCase``).
- Nombres de variables, funciones y métodos comienzan con minúsculas (usando ``lowerCamelCase`` y con palabras separadas con guión bajo).

- Ejemplos para nombres de clases: ``Persona`` - ``PrimeraClase`` - ``Ventana``
- Ejemplos para nombres de variables y funciones: ``velocidad`` - ``sumarNumeros`` - ``alto_imagen`` - ``anchoImagen``

**CamelCase**: Es escribir con la forma de jorobas de camello con las mayúsculas y minúsculas.

UpperCamelCase: La primera letra de cada palabra es mayúscula. Ejemplo: ``EjemploDeUpperCamelCase``.
lowerCamelCase: Igual a UpperCamelCase con excepción de la primer palabra. Ejemplo: ``ejemploDeLowerCamelCase``


Primer aplicación en Qt con interfaz gráfica
============================================

- Qt(Quasar Toolkit) 
	- Biblioteca para desarrollo de software de Quasar Technologies
	- Se llamó también Trolltech
	- Biblioteca multiplataforma
	- En el 2008 lo compró Nokia
	- Aplicaciones escritas con C++ (Qt)
		- KDE
		- VLC Media Player
		- Skype
		- VirtualBox
		- Google Earth 
		- Spotify para Linux
	- En 2012, Digia compra Qt y comercializa las licencias 
	- Digia desarrolló herramientas para usar Qt en iOS y Android.
		

**Ejemplo**

- Creación de una aplicación Qt

.. code-block:: c

	#include <QApplication>	
	// - Administra los controles de la interfaz
	// - Procesa los eventos
	// - Existe una única instancia
	// - Analiza los argumentos de la línea de comandos

	int main( int argc, char** argv )  {	
	    // app es la instancia y se le pasa los parámetros de la línea
	    // de comandos para que los procese.
	    QApplication app( argc, argv ); 

	    QLabel hola( "<H1 aling=right> Hola </H1>" );
	    hola.resize( 200, 100 );
	    hola.setVisible( true );

	    app.exec();  // Se le pasa el control a Qt
	    return 0;
	}



Ejercicio 8:
============

- En un Empty qmake Project
- Crear una función genérica que imprima por consola una descripción de cualquier objeto.
- El mensaje puede ser algo así: "Persona con nombre Lucrecia", "Poste con altura de 8 metros y 15 cm de diámetro".
- Probar esta función en main utilizando dos objetos de la clase Persona y dos objetos de la clase Poste.
- Incluir todo el código fuente en el archivo main.cpp.
- Pedirle al chat el código, interpretarlo y hacerlo funcionar.


Ejercicio 9:
============

- En un Empty qmake Project
- Crear una función genérica que imprima por consola sus valores ordenados
- Es decir, se le pasa un array con sus valores en cualquier orden, y la función genérica los imprime ordenados
- Que el prototipo sea: ``template < class T > void imprimir( T * v, int cantidad, bool mayor_a_menor );``
- Utilizar el método de ordenamiento por inserción
- Probar esta función en main utilizando dos arrays (int y float) y ordenar de mayor a menor y el otro al revés


Ejercicio 10:
============

- En un Empty qmake Project
- Crear una clase Jugador con atributos ``int velocidad``, ``int fuerza`` y ``std::string nombre``
- Usar constructor inicializando de la manera recomendada la velocidad en 0, fuerza en 0 y nombre "sin nombre" 
- Crear los métodos setter y getter para setear y obtener los valores de los atributos
- Incluir el destructor
- En la función main crear un ``std::vector< Jugador >`` e insertar 10 jugadores distintos
- Por último, publicar los datos de cada uno de los jugadores con ``std::cout``


Ejercicio 11:
============

- En un Empty qmake Project
- En la función main crear un objeto de la clase QLabel, uno de QWidget, uno de QPushButton y uno de QLineEdit
- Invocar al método show() de cada uno de estos 4 objetos
- Notar que cada objeto se muestra independiente

Ejercicio 12:
============

- En un Empty qmake Project
- En la función main crear un objeto de la clase QLabel y pegarle en el mismo objeto QLabel una imagen de alta resolución.
- Que la imagen se obtenga desde un archivo JPG del disco duro
- Mostrar el QLabel de forma maximizada y que la imagen no se deforme.
- Al cabo de 3 segundos, el QLabel y la aplicación se deberá cerrar


Aclaraciones:
=============

- Todos los ejercicios tienen que ser actualizados en un repositorio en GitHub en carpetas ejercicio01, ejercicio02, ...
- Contener todo lo necesario para poder compilarlo y ejecutarlo.
- Excluir los archivos y carpetas que no sean necesarios, como se el archivo con extensión .pro.user y la carpeta build-
- Enviar un mail a cesarosimani@gmail.com con la URL del repositorio.

