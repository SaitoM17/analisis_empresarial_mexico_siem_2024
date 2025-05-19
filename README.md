# 📊 Sistema de Información Empresarial Mexicano (SIEM)
# Análisis Empresaral Mexicano SIEM 2024

---

## 📚 Tabla de Contenidos

- [🎯 Propósito](#-propósito)
- [📦 Conjunto de Datos](#-conjunto-de-datos)
- [🧪 Desarrollo del Proyecto](#-desarrollo-del-proyecto)
- [📈 Conclusiones y Recomendaciones](#-conclusiones-y-recomendaciones)
- [🛠️ Tecnologías](#-tecnologías)
- [⚙️ Instalación](#-instalación)
- [👤 Autores](#-autores)

---

## 🎯 Propósito

Analizar la distribución y características de las empresas registradas en el Sistema de Información Empresarial Mexicano (SIEM) para obtener insights sobre su localización, tamaño, sector económico predominante y diferencias regionales, usando técnicas estadísticas y visualización de datos.

---

## 📦 Conjunto de Datos

El conjunto de datos utilizado contiene las siguientes columnas:

- `_id`: Identificador único del registro	
- `razon_social`: Nombre de la empresa o establecimiento
- `estado`: Estado de la República Mexicana	
- `municipio`: Municipio del establecimiento	
- `domicilio`: Dirección completa	
- `colonia`: Colonia donde se ubica el establecimiento
- `cp`: Código postal
- `telefono`: Teléfono de contacto
- `e_mail`: Correo electrónico de contacto
- `giro`: Giro comercial o actividad económica principal
- `scian`: Código SCIAN correspondiente al giro
- `rango_de_empleados`: Rango estimado de empleados en el establecimiento
- `registrado_por`: Organización o cámara que registró el negocio
- `fn_razon_social`: Nombre comercial final, si aplica
- `fn_telefono`: Teléfono adicional o actualizado
- `fn_e_mail`: Correo electrónico adicional o actualizado
- `fn_giro`: Giro comercial final corregido, si aplica
- `estado_etq`: Etiqueta o formato estándar del estado (Ej. Estado de México)


Fuente: [!Datos.gob]https://www.datos.gob.mx/dataset/sistema_informacion_empresarial_mexicano.

---

## 🧪 Desarrollo del Proyecto

1. **Carga y exploración inicial de los datos**:
   - Exploración básica con `.head()`, `.info()`, `.describe()`, etc.

2. **Limpieza y preprocesamiento**:
   - Manejo de valores nulos, duplicados, formatos y conversiones de fechas.

3. **Análisis exploratorio de datos (EDA)**:
   - [Ej. Distribución, correlaciones, agrupaciones, etc.]

4. **Visualización de datos**:
   - Uso de gráficos de barras, líneas, cajas, dispersión y mapas de calor.

5. **Modelado o reportes (opcional)**:
   - [Si aplica: modelos de ML, clustering, predicciones, etc.]

6. **Conclusiones y recomendaciones**:
   - Síntesis de hallazgos clave y propuestas de acción.

---

## 📈 Conclusiones y Recomendaciones

- [Insight 1]
- [Insight 2]
- [Recomendación práctica o estratégica basada en los datos]

---

## 🛠️ Tecnologías

- Python
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook / Google Colab
- [Otras herramientas que uses, como Scikit-learn, Plotly, etc.]

---

## ⚙️ Instalación

### 1. Clonar este repositorio:
```bash
git clone https://github.com/tu_usuario/nombre_del_proyecto.git
```
### 2. Uso de un Entorno Virtual para Aislar Dependencias

Para evitar conflictos con versiones de librerías, se recomienda usar entornos virtuales.

####  Crear y Activar un Entorno Virtual

##### Crear el entorno virtual:
```
python -m venv venv
```
##### Activar el entorno:
* #### En Windows:

    ```
    venv\Scripts\activate
    ```

* #### En Mac/Linux::

    ```
    source venv/bin/activate
    ```
#### 3. Instalar dependencias dentro del entorno:
* #### Opición 1:
    ```
    pip install -r requirements.txt
    ```

* #### Opción 2 (De forma manual):
    ```
    pip install numpy pandas matplotlib seaborn scikit-learn
    ```
---

## 👤 Autor

**Said Mariano Sánchez** – *smariano170@gmail.com*  
Este proyecto forma parte de mi portafolio como analista de datos Jr.

---

## 📝 Licencia

Este proyecto está licenciado bajo la **Licencia MIT**. Puedes usarlo, modificarlo y distribuirlo libremente, siempre que menciones al autor original.

---