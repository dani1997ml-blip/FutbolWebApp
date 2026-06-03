# Navegacion DataFlex

## Casos de la tarea

### Main -> Select -> Zoom

Desde el dashboard (`vtUndefined`) se usa `NavigateForwardCustom`, por eso la llegada al `Select` queda como `nfUndefined`. Al entrar desde el `Select` al `Zoom`, el `InvokingObject` pasa a ser el objeto que lanza la navegacion, normalmente `oList` o el boton de detalle. Ese objeto aporta el `tWebNavigateData` con la fila seleccionada.

### Child -> Zoom hijo -> Select padre

Ejemplo implementado: `SelectEquipo -> ZoomEquipo -> SelectLiga`.

En `ZoomEquipo`, el boton `Ver Liga` navega al `SelectLiga` pasando el `RowId` actual de `Liga`. Como `Liga` es padre de `Equipo`, esta navegacion se interpreta como `nfFromChild`.

### Parent -> Zoom liga

Ejemplo implementado: `SelectLiga -> ZoomLiga`.

En `ZoomLiga` hay dos soluciones:

1. Boton `Equipos`, que abre `SelectEquipo` filtrado por la liga actual.
2. Lista embebida `Equipos de esta liga`, que muestra directamente los equipos de la liga abierta.

### Undefined -> Zoom jugador -> Select posicion

Ejemplo implementado: `ZoomJugador -> SelectPosicion` con el boton `Posiciones`.

Se usa `NavigateForwardCustom`, por lo que la navegacion queda como `nfUndefined`. Entre `Jugador` y `Posicion` no hay una relacion directa en los DD de esta aplicacion; la relacion real seria muchos-a-muchos mediante una tabla intermedia (`jugador_posicion` en SQL), que no esta modelada como vista/DD en el proyecto.

## Orden general de eventos de navegacion forward

1. `OnClick` del objeto que inicia la navegacion.
2. `NavigatePath`, `NavigateForward` o `NavigateForwardCustom` en la vista destino.
3. DataFlex determina `eNavigateType`: `nfFromMain`, `nfFromParent`, `nfFromChild` o `nfUndefined`.
4. `GetNavigateForwardData` del `InvokingObject`.
5. `OnGetNavigateForwardData` del `InvokingObject`.
6. `OnNavigating` de la vista invocada.
7. `ShowView` / carga de la vista invocada.
8. `NavigateForwardFinish`.
9. `OnNavigateForwardPreFindInit` de la vista invocada.
10. Rebuild/refind de DDs y restricciones.
11. `OnNavigateForward` de la vista invocada.
12. Eventos de visualizacion de la vista: `OnLoad`, `OnBeforeShow` y `OnShow` cuando correspondan.

## Orden general de navegacion back

1. Accion de volver desde la vista actual.
2. `GetNavigateBackData` del `InvokingObject`.
3. `OnGetNavigateBackData` del `InvokingObject`.
4. Restauracion de la vista anterior en el `StackView`.
5. `OnNavigateBack` del objeto que recibe la vuelta.
6. Eventos de visualizacion de la vista restaurada.
