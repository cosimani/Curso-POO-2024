.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 08 - POO 2024
===================
(Fecha: 10 de abril)



Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`POO 2023 - Array como parámetros - QTextEdit y aritmética de punteros 2023 <https://youtu.be/FzbxG3KJkdE>`_



Array como parámetro en funciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	#include <iostream>
	using namespace std;

	void funcion( int miArray[] );
	// Le estamos pasando un puntero al primer elemento del array.

	int main()  {
	    int miA[ 5 ] = { 0, 1, 2, 3, 4 };

	    funcion( miA );

	    cout << miA[ 0 ] << miA[ 1 ] << miA[ 2 ] << miA[ 3 ] << miA[ 4 ];
	}

	void funcion( int miArray[] )  {
	    miArray[ 0 ] = 5;  // Las modificaciones quedarán.

	    miArray[ 3 ] = 5; 
	} 



Constructores con argumentos por defecto
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	class ClaseA  {
	public:
	    ClaseA( int a = 10, int b = 20 ) : a( a ), b( b )  {  }
	
	    void verDatos( int &a, int &b )  {
	        a = this->a;
	        b = this->b;
	    }

	private:
	    int a, b;
	};

	int main( int argc, char ** argv )  {
	    ClaseA * objA = new ClaseA;

	    int a, b;
	    objA->verDatos( a, b );
	
	    std::cout << "a = " << a << " b = " << b << std::endl;

	    return 0;
	}

	// Probar con:	
	
	ClaseA( int c, int a = 10, int b = 20 ) : a( a ), b( b ), c( 0 )  {  }

	ClaseA( int a = 10, int b = 20, int c ) : a( a ), b( b ), c( 0 )  {  }


QTextEdit
=========

- Un QWidget que muestra texto plano o enriquecido
- Puede mostrar imágenes, listas y tablas
- La barra de desplazamiento es automática
- Interpreta tags HTML
- Seteamos texto con setPlainText()


Desafío
=======

- Escribir la salida por consola de la siguiente aplicación:

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication app( argc, argv );

	    int a = 10, b = 100, c = 30, d = 1, e = 54;
	    int m[ 10 ] = { 10, 9, 80, 7, 60, 5, 40, 3, 20, 1 };
	    int *p = &m[ 3 ], *q = &m[ 6 ];

	    ++q;
	    qDebug() << a + m[ d / c ] + b-- / *q + 10 + e--;

	    p = m;
	    qDebug() << e + *p + m[ 9 ]++;

	    return 0;
	}


Ejercicio 14 (continuación):
============================

- Agregar la siguiente característica a Login: Si el usuario falla 3 veces la clave, bloquear por 5 minutos a ese usuario.


Ejercicio 18
============

- Utilizar un proyecto con un login cualquiera que valide admin:1234
- Cuando el usuario es válido, abrir una nueva ventana que tenga un QTextEdit que permita mostrar código HTML.
- Esta ventana deberá tener un QLineEdit que permita ingresar una URL
- Cuando se pulse Enter, se deberá buscar el html de la URL escrita y se deberá publicar en el QTextEdit.

