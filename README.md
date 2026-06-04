# Proyecto_Cardiovascular_Undes_1er_TALLER_MEPI_PIllanes
===========================================================
  # ESTUDIO: FACTORES DE RIESGO CARDIOVASCULAR 
  # =============================================================


# --- 1. EL CONTEXTO CLÍNICO: NUESTRA COHORTE ---
# Imaginemos que hemos recolectado datos de 50 pacientes en un consultorio.
set.seed(2026) 
datos_clinicos <- data.frame(
  id = 1:50,
  edad = sample(18:85, 50, replace = TRUE),
  sexo = factor(sample(c("Femenino", "Masculino"), 50, replace = TRUE)),
  presion_sistolica = round(rnorm(50, 132, 12)), # mmHg (Promedio 132)
  fumador = factor(sample(c("Fumador", "No Fumador"), 50, replace = TRUE)),
  colesterol_total = round(rnorm(50, 210, 35)), # mg/dL
  evento_cardiaco = sample(c(TRUE, FALSE), 50, replace = TRUE) # TRUE = Tuvo infarto/ACV
)

# --- 2. PREPARACIÓN DEL LABORATORIO ---
# Para investigar, necesitamos herramientas. Instalamos y cargamos 'tidyverse'.
install.packages("tidyverse")
library(tidyverse) 

# --- 3. PROCESAMIENTO (La pregunta de investigación) ---
# ¿Cuál es el colesterol promedio en pacientes fumadores mayores de 50 años?
reporte_riesgo <- datos_clinicos %>%
  filter(edad > 50) %>%                
  group_by(sexo, fumador) %>%           
  summarize(promedio_col = mean(colesterol_total))

# --- 4. VISUALIZACIÓN DE EVIDENCIA ---
install.packages("ggplot2")
library(ggplot2)
ggplot(datos_clinicos, aes(x = edad, y = presion_sistolica, color = fumador)) +
  geom_point(size = 3) +
  geom_smooth(method = "lm") + 
  labs(title = "Relación Edad y Presión Arterial según Hábito Tabáquico",
       subtitle = "Cohorte de Estudio Cardiovascular - Módulo 0")
