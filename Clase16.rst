.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 16 - POO 2024
===================
(Fecha: 20 de mayo)


Registro en video de algunos temas de la clase de hoy
=====================================================

`const 2021 <https://youtu.be/UqXE4GeFd_s>`_ 

`QFile 2021 <https://youtu.be/Zf-yAkNmqso>`_ 


const
=====

- Una variable definida como const no podrá ser modificada a lo largo del programa (se crea como sólo lectura)
- Se puede aplicar a cualquier tipo:

.. code-block:: c	

	const float pi = 3.14;
	const peso = 67;  // Si no se indica el tipo entonces es int
	                  // Aunque sólo en compiladores viejos



const con punteros
^^^^^^^^^^^^^^^^^^

.. code-block:: c	

	int x = 10;
	int * px = &x;  // normal

	const int y = 10;
	int * py = &y;  // El compilador dirá: "invalid conversion from const int*
	               // to int*". La inversa sí se permite

	int y = 10;
	const int * py = &y;  // permitido (pero el contenido es de sólo lectura)

	*py = 6;  // No permitido. El contenido apuntado es de sólo lectura


const en parámetros de funciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Cuando los parámetros son punteros, decimos que no podrá modificar los objetos referenciados

.. code-block:: c	

	int funcion( const char * ch )


- Lo mismo sucede con referencias

.. code-block:: c	

	int funcion( const char& ch )


const en clases
^^^^^^^^^^^^^^^

.. code-block:: c	

	class ClaseA  {
	    const int i;
	    int x;

	public:
	    int funcion( ClaseA cA, const ClaseA &c )  {
	        cA.x = 1;
	        cA.i = 2;  // No compila. i es de sólo lectura.
	        c.x = 3;   // No compila. El objeto c es de sólo lectura.

	        return cA.x;
	    }
	}; 


.. code-block:: c	

	// A la variable i sólo la puede inicializar el constructor y sólo con la forma:
	ClaseA() : i( 8 )  {  }   

	// Si en el cuerpo del constructor se hace:
	ClaseA()  { 
	    i = 8;  // Compila? i es de solo lectura o no
	}   


- Aplicado a métodos de una clase no permite modificar ninguna propiedad de la clase

.. code-block:: c	

	class ClaseB  {
	    int x;

	    void funcion( int i ) const  {
	        x = x + i;  // Compila?
	    }
	};


Clase QFile
^^^^^^^^^^^

- Permite leer y escribir en archivos. 
- Puede ser utilizado además con ``QTextStream`` o ``QDataStream``.

.. code-block:: c	

	QFile( const QString & name )
	viod setFile( const QString & name )

- Existe un archivo? y lo eliminamos.

.. code-block:: c	

	bool exists() const
	bool remove()

- Lectura de un archivo línea por línea:

.. code-block:: c	

	QFile file( "c:/in.txt" );
	if ( !file.open ( QIODevice::ReadOnly | QIODevice::Text ) )
	    return;

	while ( !file.atEnd() )  {
	    QByteArray linea = file.readLine();
	    qDebug() << linea;
	}



Clase QFileDialog
=================

- Permite abrir un cuadro de diálogo para buscar un archivo en disco

.. code-block:: c	

	QString file = QFileDialog::getOpenFileName( this, "Abrir", "./", "Imagen (*.png *.jpg)" );


Ejercicio 24:
=============

- Crear un **parser** que pueda analizar cualquier html en busca de todas las URLs que encuentre
- Crear una GUI que permita al usuario ingresar un sitio web en un QLineEdit
- Que descargue en archivos todos los recursos de dicho sitio web
- Es decir, que busque en el html las imágenes, los css, los javascript y los descargue en archivos
- Que le permita al usuario indicar en qué directorio descargar los archivos
- También agregar un botón que upermita elegir un archivo de imagen del disco con ``QFileDialog`` y que la dibuje en pantalla con paintEvent.


Tareas adicionales:
===================

- Revisión de entornos virtuales en sus computadoras
- Instalación y funcionamiento de FastAPI y MongoDB
- Utilización de Postman para consultar APIs
- Probar consultas a APIs con el envío de credenciales de usuario, access token o similar
- Probar, por ejemplo, con MercadoLibre, Instagram, Spotify






