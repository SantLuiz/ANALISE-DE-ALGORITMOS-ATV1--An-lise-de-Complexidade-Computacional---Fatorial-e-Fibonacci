# Java Performance Benchmark: Estudo de Escalabilidade, Concorrência e Gestão de Memória

Este projeto realiza uma **Análise de Eficiência Algorítmica** e **Complexidade Computacional** no cálculo de fatoriais em larga escala. O foco principal é o **Benchmarking** de diferentes arquiteturas em Java, avaliando o impacto direto no hardware (CPU/RAM) e a otimização de recursos da **JVM (Java Virtual Machine)**.

---

## 🛠️ Stack Técnica e Competências Aplicadas

*   **Linguagens:** Java (JDK 17+) e Python (Pandas/Matplotlib para análise de dados).
*   **Performance & Concorrência:** Java Streams API (Parallel), Multi-threading, Algoritmo de Karatsuba.
*   **Gestão de Recursos:** Monitoramento de **Heap Memory**, Otimização de **Garbage Collector (GC)** e **Buffered I/O**.
*   **Fundamentos:** Complexidade Big O, Estruturas de Dados, Imutabilidade de Objetos.

---

## 🎯 Objetivos do Projeto (Métricas de Performance)

O sistema utiliza três indicadores fundamentais para medir a eficiência do software:

1.  **Δt (Variação de Tempo/Latency):** Mensuração do tempo de execução conforme a carga de processamento aumenta.
2.  **Δm (Variação de Memória/Throughput):** Monitoramento da alocação de memória na **Heap** e pressão sobre o **Garbage Collector**.
3.  **Δε (Esforço Computacional):** Análise do custo de processamento em cenários **Single-core vs Multi-core**.

---

## 🧠 Arquitetura dos Motores de Cálculo (Engenharia de Software)

O projeto compara 4 estratégias, demonstrando como decisões de design impactam a **escalabilidade** e o consumo de hardware.

### 1️⃣ F1 - Hybrid (Single-core / Low Memory)
*   **Foco:** Otimização para hardware limitado.
*   **Estratégia:** Uso de tipos primitivos (`long` - 8 bytes) com conversão tardia para `BigInteger`.
*   **Vantagem:** Evita o *overhead* de paralelismo e minimiza a criação de objetos na memória RAM.

### 2️⃣ F2 - Stream (Parallel / Multi-core / Karatsuba)
*   **Foco:** Escalabilidade Vertical e Processamento Paralelo.
*   **Estratégia:** Utiliza **Parallel Streams** para distribuir a carga entre múltiplos núcleos da CPU.
*   **Diferencial:** Implementação interna do **Algoritmo de Karatsuba**, otimizando a multiplicação de grandes inteiros.

### 3️⃣ F3 - Linear (Baseline / Ineficiente)
*   **Foco:** Demonstração de gargalos (*Bottlenecks*).
*   **Problema:** Alta instabilidade devido à **imutabilidade do BigInteger**.
*   **Impacto:** Gera milhões de instâncias temporárias, causando travamentos por excesso de trabalho do **Garbage Collector**.

### 4️⃣ F4 - Ultra Hybrid (Batching + Parallel Tree)
*   **Foco:** Performance de nível industrial (**State-of-the-art**).
*   **Estratégia:** Combina processamento em lotes (*batching*) com **Tree Reduction** (redução em árvore).
*   **Resultado:** A abordagem mais equilibrada, unindo baixo consumo de memória com máximo aproveitamento de núcleos da CPU.

---

## 📊 Resultados e Benchmarks (Amostra: 500.000 iterações)


| Métrica | Algoritmo F3 (Linear) | Algoritmo F4 (Ultra Hybrid) |
| :--- | :--- | :--- |
| **Tempo de Resposta (Δt)** | ~70.107 ms | **~1.129 ms (60x mais rápido)** |
| **Estabilidade de Memória** | Crítica (GC Spikes) | Estável e Otimizada |
| **Eficiência de Escala** | Exponencial (Ineficiente) | Linear / Estável |

---

## 🚀 Como Executar e Requisitos

### Pré-requisitos
*   **Java Development Kit (JDK) 11 ou superior.**
*   **Ambiente:** Mínimo 2GB de RAM livre para testes de alta carga (especialmente para o motor F3).

### Instalação e Execução
1. Compile os módulos:
   ```bash
   javac Main.java
   FactorialMaster.java
