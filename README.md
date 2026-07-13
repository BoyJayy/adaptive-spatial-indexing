# Adaptive Spatial Indexing

# or Adaptive-spatial-indexing-for-fixed-radius-neighbor-search-in-dynamic-particle-systems

Online adaptive spatial index selection for fixed-radius neighbor search
in dynamic particle systems.

## English

`adaptive-spatial-indexing` is a research-oriented C++20 project focused on
efficient fixed-radius neighbor search in dynamic particle systems.

In these systems, particles continuously change their positions. At every
simulation step, the system must find all pairs of particles located within
a specified interaction radius.

Different spatial indexing methods perform differently depending on:

- the number of particles;
- particle density and clustering;
- the size of the search radius;
- particle movement between simulation steps;
- the cost of rebuilding or updating the index;
- CPU and GPU architecture.

The project will implement and evaluate several approaches:

- brute-force pair search;
- uniform grids;
- hashed grids;
- spatial sorting;
- BVH-based search;
- index reuse, update, and rebuild strategies;
- online adaptive method selection.

The long-term goal is to build an adaptive system that analyzes the current
particle distribution and dynamically selects the most efficient spatial
index and update strategy.

The evaluation will include:

- correctness against a brute-force reference;
- index construction and update time;
- neighbor-search latency;
- throughput;
- memory usage;
- scalability;
- performance across uniform, sparse, clustered, and dynamically changing
  workloads.

### Research question

Can an online adaptive policy select spatial indexing and update strategies
that approach the performance of the best specialized method across changing
particle workloads?

### Development status

The project is developed incrementally.

Current roadmap:

1. C++20 project infrastructure;
2. 2D particle representation;
3. brute-force correctness baseline;
4. uniform-grid implementation;
5. reproducible benchmarks and workload generators;
6. hashed grids and spatial sorting;
7. dynamic index reuse and rebuild policies;
8. BVH-based search;
9. online adaptive method selection;
10. parallel CPU and GPU implementations.

Development of the implementation will begin after the first
`image-similarity-lab` milestone is completed.

---

## Русский

`adaptive-spatial-indexing` — исследовательский проект на C++20, посвящённый
эффективному поиску соседей в заданном радиусе в динамических системах частиц.

В таких системах частицы постоянно изменяют своё положение. На каждом шаге
симуляции необходимо находить все пары частиц, расстояние между которыми не
превышает заданный радиус взаимодействия.

Производительность различных пространственных индексов зависит от:

- количества частиц;
- плотности и степени кластеризации;
- радиуса поиска;
- перемещения частиц между шагами;
- стоимости перестроения и обновления индекса;
- архитектуры CPU и GPU.

В проекте будут реализованы и исследованы:

- полный перебор пар;
- равномерные пространственные сетки;
- хешированные сетки;
- пространственная сортировка;
- поиск на основе BVH;
- переиспользование, обновление и перестроение индексов;
- автоматический выбор метода во время выполнения.

Долгосрочная цель проекта — создать адаптивную систему, которая анализирует
текущее распределение частиц и динамически выбирает наиболее эффективный
пространственный индекс и стратегию его обновления.

Будут измеряться:

- корректность относительно полного перебора;
- время построения и обновления индекса;
- задержка поиска соседей;
- пропускная способность;
- потребление памяти;
- масштабируемость;
- производительность на равномерных, разреженных, кластеризованных и
  динамически изменяющихся наборах частиц.

### Исследовательский вопрос

Может ли адаптивная система во время выполнения выбирать пространственный
индекс и стратегию обновления так, чтобы приближаться к производительности
лучшего специализированного метода на изменяющихся сценариях?

### Статус разработки

Проект будет разрабатываться поэтапно.

План:

1. инфраструктура C++20-проекта;
2. представление двумерных частиц;
3. эталонный полный перебор;
4. равномерная пространственная сетка;
5. воспроизводимые benchmarks и генераторы сценариев;
6. хешированные сетки и пространственная сортировка;
7. стратегии переиспользования и перестроения индекса;
8. поиск на основе BVH;
9. автоматический выбор метода;
10. параллельные реализации для CPU и GPU.

Разработка реализации начнётся после завершения первого полноценного этапа
`image-similarity-lab`.
