# 🐍 Snake AI - Aprendizaje por Refuerzo (Deep Q-Learning)

> Un agente autónomo que aprende a jugar al clásico juego "Snake" desde cero utilizando Deep Q-Learning (DQN) y Redes Neuronales con PyTorch.

## 📋 Descripción

Este proyecto es una implementación de **Reinforcement Learning (RL)** donde una Inteligencia Artificial aprende a jugar Snake sin reglas pre-programadas de movimiento. El agente "nace" sin conocimiento y aprende mediante un sistema de recompensas y castigos, desarrollando estrategias para maximizar su puntuación y evitar colisiones.

El núcleo del aprendizaje se basa en una **Red Neuronal Profunda (Deep Q-Network)** que aproxima la función Q (calidad de una acción en un estado dado).

## 🧠 ¿Cómo funciona la IA?

El agente toma decisiones basándose en el estado actual del entorno y recibe retroalimentación inmediata.

### 1. El Vector de Estado (Inputs)

La IA no "ve" la pantalla completa como una imagen. En su lugar, recibe un vector de **11 valores booleanos** (0 o 1) que representan su entorno inmediato:

1.  **Peligro (3 valores):** ¿Hay pared/cuerpo al frente, a la derecha o a la izquierda?
2.  **Dirección actual (4 valores):** ¿Se está moviendo hacia Oeste, Este, Norte o Sur?
3.  **Ubicación de la Comida (4 valores):** ¿La comida está a la izq, der, arriba o abajo?

### 2. Acciones (Outputs)

La Red Neuronal tiene 3 neuronas de salida (Softmax/Argmax):

- `[1, 0, 0]` -> **Seguir Recto**
- `[0, 1, 0]` -> **Girar Derecha**
- `[0, 0, 1]` -> **Girar Izquierda**

### 3. Sistema de Recompensas (Reinforcement)

- **Comer manzana:** +10 Puntos.
- **Morir (Colisión):** -10 Puntos.
- **Moverse (sin comer):** 0 Puntos.

### 4. Arquitectura del Modelo

- **Input Layer:** 11 Neuronas.
- **Hidden Layer:** 256 Neuronas (Activación ReLU).
- **Output Layer:** 3 Neuronas (Valores Q para las 3 acciones posibles).
- **Optimizador:** Adam.
- **Loss Function:** MSE (Mean Squared Error).

---

## 📂 Estructura del Proyecto

```text
snake_ai_project/
├── src/
│   ├── ai/
│   │   ├── agent.py        # Cerebro: Experience Replay y Lógica de entrenamiento
│   │   └── model.py        # Arquitectura de la Red Neuronal (PyTorch)
│   ├── game/
│   │   └── snake_game_ai.py # Entorno del juego (Pygame) modificado para RL
│   ├── main.py             # Entry point y bucle de entrenamiento
│   ├── settings.py         # Hiperparámetros (Velocidad, LR, Gamma)
│   └── utils.py            # Helpers para graficar resultados
├── models/                 # Aquí se guardan los modelos (.pth) entrenados
├── requirements.txt        # Dependencias
└── README.md
```
