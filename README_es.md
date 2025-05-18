# Tabla de Dimensión Calendario

> [!IMPORTANT]  
Antes de comenzar, asegúrate de tener instalada al menos la versión de enero de 2025 de Power BI Desktop.  
Habilita la opción en Archivo > Opciones y configuración > Opciones > Características de vista previa > ✅ Vista TMDL

## 1. Modo local directamente en Power BI Desktop con TMDL

> Este método está destinado a quienes desean una tabla de dimensión calendario independiente para cada modelo semántico.  
> Este es el único método que no requiere ninguna licencia.

Ventajas:
- Independencia de otros elementos como dataflows, lakehouses y warehouses.

Desventajas:
- Mayor tiempo de actualización.
- Mayor volumen de datos en Power BI Service.
- Posibles discrepancias entre modelos.

Instrucciones:
- Crea o importa cualquier tabla en Power BI Desktop;
- Haz clic en el botón `TMDL` en la barra lateral izquierda;
- Copia el código para el idioma deseado desde [TMDLDesktop](./TMDLDesktop/) y pégalo en el área de código.
- Haz clic en `Aplicar` y luego, en la alerta superior, haz clic en `Actualizar ahora`.

## 2. Dataflow gen1 Import (PRO)

> Este método es recomendado para quienes desean una única tabla de dimensión calendario para toda la organización utilizando dataflows gen1.  
> Es el método más recomendado para usuarios con licencia PRO.

Ventajas:
- Fuente única de fechas para la organización;
- Estandarización;
- Rendimiento;
- Reutilización.

Desventajas:
- Más pasos para la configuración inicial.

Instrucciones:
- Crea un nuevo dataflow gen1;
- Crea una consulta en blanco;
- Copia el código para el idioma deseado desde [PowerQueryOrDataflow](./PowerQueryOrDataflow/) y pégalo en el editor avanzado de la consulta en blanco;
- Renombra tu tabla a DimCalendario;
- Haz clic en `Guardar y cerrar`;
- Guarda el dataflow y asígnale el nombre DfwCalendario;
- Actualiza el dataflow;
- Configura la actualización automática diaria a las 00:00 según tu zona horaria;
- Abre un archivo en blanco en Power BI Desktop;
- En la pestaña `Inicio`, haz clic en `Obtener datos` y luego en `Dataflows`;
- Si se solicita, inicia sesión con tu cuenta y contraseña;
- Busca el Workspace y el Dataflow `FlwCalendario`, marca la tabla `dCalendario` y haz clic en `Cargar`;
- Haz clic en el botón `TMDL` en la barra lateral izquierda;
- Arrastra la tabla DimCalendario desde la pestaña Tablas a la derecha al campo de código de Script1;
- Crea el Script2 haciendo clic en `+` en la pestaña inferior;
- Copia el código para el idioma correspondiente desde [TMDLAfterDataflow](./TMDLAfterDataflow/) y pégalo en Script2. ¡No apliques todavía!;
- Vuelve a Script1, desplázate hasta el final del código y copia desde 'partition' hasta el final;
- Ve a Script2, desplázate hasta el final y pega sobre 'partition' hasta el final;
- Haz clic en `Aplicar`.

### 3. Modo Direct Lake (Usuarios de Fabric)

> Este modo está recomendado para quienes utilizan modelos semánticos en Direct Lake de Fabric.  
> El código se actualiza a través de Dataflows gen2 y puede ser alojado tanto en Lakehouses como en Warehouses.  
> Para la demostración, la carga será en un Warehouse simulando la capa gold de nuestro proyecto.

Ventajas:
- Fuente única de fechas para la organización;
- Estandarización;
- Rendimiento;
- Reutilización.

Desventajas:
- Más pasos para la configuración inicial.

Instrucciones:
- Crea un Workspace y configúralo para una Capacidad de Fabric (o Trial);
- Crea un nuevo Warehouse;
- Nombra el Warehouse como DW_Gold;
- Dentro del Warehouse, haz clic en `Obtener datos` y luego elige `Nuevo Dataflow Gen2`;
- Nómbralo DfwCalendario y marca la opción `Habilitar integración con Git...` y haz clic en `Crear`;
- Crea una consulta en blanco;
- Copia el código para el idioma deseado desde [PowerQueryOrDataflow](./PowerQueryOrDataflow/) y pégalo en el editor avanzado de la consulta en blanco;
- Renombra tu tabla a DimCalendario;
- Guarda el dataflow y ciérralo;
- Espera la publicación y actualización inicial. Si no ocurre, fuerza la actualización;
- Configura la actualización automática diaria a las 00:00 según tu zona horaria mediante programación o Data Pipelines;
- Abre el warehouse, haz clic en `Informes` y luego en `Nuevo modelo semántico`;
- Elige la tabla `dCalendario` y otras tablas deseadas para tu modelo;
- Nómbralo `SMGold` y guarda;
- Abre Power BI Desktop y en la pestaña `Inicio` haz clic en OneLake catalog y luego en `Power BI Semantic Models`;
- Haz clic en el modelo `SMGold` pero no en el botón conectar, sino en la flecha al lado y luego en `Editar`;
- Haz clic en el botón `TMDL` en la barra lateral izquierda;
- Arrastra la tabla DimCalendario desde la pestaña Tablas a la derecha al campo de código de Script1;
- Crea el Script2 haciendo clic en `+` en la pestaña inferior;
- Copia el código para el idioma correspondiente desde [TMDLDirectLake](./TMDLDirectLake/) y pégalo en Script2. ¡No apliques todavía!;
- Vuelve a Script1, desplázate hasta el final del código y copia desde 'partition' hasta el final;
- Ve a Script2, desplázate hasta el final y pega sobre 'partition' hasta el final;
- Aplica y actualiza;
- Haz clic en `Aplicar`.