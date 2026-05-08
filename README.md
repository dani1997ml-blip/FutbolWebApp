# FutbolWebApp

Proyecto DataFlex Web Mobile conectado a MySQL para gestionar datos de futbol.

## Contenido

- Base de datos `futbol` en MySQL.
- Vistas Select y Zoom para `entrenador`, `jugador`, `posicion`, `equipo` y `liga`.
- Dashboard con accesos a las cinco tablas principales.
- Tablas internas de DataFlex configuradas en MySQL.

## Arranque local

La aplicacion queda publicada en IIS como:

```text
http://localhost/FutbolWebApp/Index.html
```

El workspace de DataFlex es:

```text
FutbolWebApp.sws
```

## Base de datos

El script de la base de datos esta en:

```text
Database/futbol.sql
```

Los archivos `.int` usan MySQL ODBC contra la base de datos `futbol`. Antes de ejecutar el proyecto en otro equipo hay que revisar la cadena de conexion en `Data/*.int` y poner el usuario y la contrasena locales de MySQL.
