# KDTree как структура быстрого поиска данных
## Общие сведения

KD-дерево (KDTree) – это структура данных с разбиением пространства для упорядочивания точек в k-мерном пространстве. KD-деревья — особый вид двоичных деревьев поиска

В данной лабораторной рассмотрены построение дерева KDTree, поиск данных с помощью дерева поиска, а также поиск, частично использующий дерево, и частично – перебор.


## Point
 
Вспомогательный класс, представляющий из себя трехмерную точку (**std::array<float, 3> coordinates**)
 
 #### Реализованные методы
 
| Метод  | Описание |
| ------------- | ------------- |
| `Point()`  | Конструктор по умолчанию |
| `Point(std::array<float, 3>)` | Конструктор по трем координатам |
| `Point(std::initializer_list<float> list)` | Конструктор по списку инициализации |
| `~Point()`  | Деструктор |
| `float getCoordByIdx(size_t index) const` | Получение координаты по ее индексу  |
| `double getDistance(const Point& pt) const` | Вычисление квадрата эвклидового расстояния |


 ## KDTree
 
 Данный класс служит для построения и работы дерева. Узлы дерева – структура *Node*, содержащая данные экземпляра точки (**Point pivotPoint**), а также две ссылки на потомков Node* leftChildNode, Node* rightChildNode. Дерево хранит информацию о векторе узлов **std::vector<Node> nodeVector**, корне дерева Node* root, лучшем узле в смысле близости к данной точке Node* best, расстояние от best до данной точки **double bestDist**, количество посещенных вершин **size_t visited**
 
 #### Реализованные методы
 
| Метод  | Описание |
| ------------- | ------------- |
| `KDTree(const KDTree&)`  | Конструктор по умолчанию |
| `KDTree(iterator begin, iterator end)` | Конструктор по шаблонному итератору |
| `KDTree(iterator begin, iterator end, int k)`  | Конструктор по шаблонному итератору (на листах k элементов) |
| `size_t totalVisited() ` | Подсчет количества посещенных вершин  |
| `double distance()` | Расстояние от данной точки до ближайшего элемента из дерева |
| `Node* buildTree(size_t begin, size_t end, size_t index)` | Построение дерева (на листах 1 элеемент) |
| `Node* kNearestBuildTree(size_t begin, size_t end, size_t step, size_t k)` | Построение дерева (на листах k элеементов) |
| `const Point& closestPoint(const Point& pt)` | Вычисление ближайшей точки дерева к данной точке (на листах 1 элемент) |
| `const Point& kClosestPoints(const Point& pt, int k)` | Вычисление ближайшей точки дерева к данной точке (на листах k элементов) |
| `void closestPointFromIdxStep(Node* tRoot, const Point& point, int index)` | (вспомогательный метод) Вычисление ближайшей точки дерева к данной точке (на листах k элементов), с учетом шага index|
| ` void kClosestPointsFromIdxStep(Node* tRoot, const Point& point, int k, int step, size_t begin, size_t end)` | (вспомогательный метод) Вычисление ближайшей точки дерева к данной точке (на листах k элементов) с учетом шага step|

В рамках курса работа данной реализации KDTRee сравнивается поиском ближайшего соседа перебором, а совмещенным поиском (где перебором вычисляется точка среди k вершин, найденных деревом).

Результаты определяются при помощи библиотеки chrono и компилируются, тесты приведены в каталоге **prj.test/KDTree**
