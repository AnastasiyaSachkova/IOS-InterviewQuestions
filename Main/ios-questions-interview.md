Вопросы на собеседование iOS разработчика (дополненное издание):

- Что такое [`полиморфизм`](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/OOP_ObjC/Articles/ooObjectModel.html#//apple_ref/doc/uid/TP40005149-CH5-SW11)?
> Полиморфизм — возможность объектов с одинаковой спецификацией иметь различную реализацию.
> Пример: Класс или интерфейс геометрических фигур (эллипс, многоугольник) может иметь методы для геометрических трансформаций (вычисление площади, смещение, поворот, масштабирование).
> 


- Что такое [`инкапсуляция`](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/OOP_ObjC/Articles/ooObjectModel.html#//apple_ref/doc/uid/TP40005149-CH5-SW10)? 
> инкапсуляция - языковой механизм ограничения доступа к определённым компонентам объекта
> ```
> @interface Demo : NSObject
> {
>    NSInteger total; //private valible
> }
> -(void)printTotal;  //public method
> @end
> ```

- Что такое `нарушение инкапсуляции`?
> нарушение инкапсуляции - это все утечка внутренней логики работы класса.
> Пример: прямое обращение к внутренним переменным класса

- Чем `абстрактный` класс отличается от `интерфейса`?
> Интерфейсы, в отличии от абстрактных классов, поддерживают множественное наследование. Т.е. класс-потомок может реализовывать 2 или более интерфейсов одновременно: class A implements Int1, Int2, но class A extends AbstrB
>
> Интерфейс содержит исключительно объявления методов, но не содержит реализации. Абстрактный класс же может содержать как абстрактные методы (без реализации), так и обыкновенные.
>
> Интерфейс не может включать в себя свойства, в абстрактном классе, как и в любом другом, свойства могут присутствовать.
>
> Класс-потомок обязан реализовывать все методы интерфейса, методы абстрактного класса же могут в нем не присутствовать.
>
> В интерфейсе все методы открытые, в абстактном классе они могут содержать спецификаторы доступа (private, protected, pubic).


- Расскажите о [`паттерне MVC`](https://ru.wikipedia.org/wiki/Model-View-Controller). Чем отличается `пассивная` модель от `активной`?
> Концепция MVC позволяет разделить данные, представление и обработку действий пользователя на три отдельных компонента:
>
> -Модель (англ. Model). Модель предоставляет знания: данные и методы работы с этими данными, реагирует на запросы, изменяя своё состояние. Не содержит информации, как эти знания можно визуализировать.
>
> -Представление, вид (англ. View). Отвечает за отображение информации (визуализацию). Часто в качестве представления выступает форма (окно) с графическими элементами.
>
> -Контроллер (англ. Controller). Обеспечивает связь между пользователем и системой: контролирует ввод данных пользователем и использует модель и представление для реализации необходимой реакции.
>
>Важно отметить, что как представление, так и контроллер зависят от модели. Однако модель не зависит ни от представления, ни от контроллера. Тем самым достигается назначение такого разделения: оно позволяет строить модель независимо от визуального представления, а также создавать несколько различных представлений для одной модели.
>
> Пассивная модель — модель не имеет никаких способов воздействовать на представление или контроллер, и пользуется ими в качестве источника данных для отображения. Все изменения модели отслеживаются контроллером и он же отвечает за перерисовку представления, если это необходимо. Такая модель чаще используется в структурном программировании, так как в этом случае модель представляет просто структуру данных, без методов их обрабатывающих.
>
> Активная модель — модель оповещает представление о том, что в ней произошли изменения, а представления, которые заинтересованы в оповещении, подписываются на эти сообщения. Это позволяет сохранить независимость модели как от контроллера, так и от представления.
>

- Реализация [`синглтона (Singleton)`](http://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CocoaFundamentals/CocoaObjects/CocoaObjects.html#//apple_ref/doc/uid/TP40002974-CH4-SW32) в [`ARC`](http://habrahabr.ru/post/209288/) и в `non-ARC`?
> ARC, thread safe
> ```
>	+ (instanceType *)sharedInstance {
>        static instanceType *sharedInstance = nil;
>        static dispatch_once_t onceToken; // onceToken = 0
>        dispatch_once(&onceToken, ^{
>            sharedInstance = [[instanceType alloc] init];
>        });
>
>         return sharedInstance;
>    }
>```

- Какие еще [`паттерны`](http://habrahabr.ru/post/202960/) знаете?
- Паттерны `порождающие, создания объектов (Creational): Singleton, Abstarct Factory`?
- Паттерны `структурные (Structural): MVC, Decorator(Categories, Delegation), Adapter(Delegation), Facade, Composite`?
- Патерны `поведения и взаимодействия объектов (Behavioral): Observer(Notification, KVO), Memento(Archiving+UserDefaults), Chain of Recponsibility, Command(Target-Action mechanism)`?

- Что такое [`responder chain`](https://developer.apple.com/library/prerelease/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/event_delivery_responder_chain/event_delivery_responder_chain.html#//apple_ref/doc/uid/TP40009541-CH4-SW2)?
> Это цепочка по которой проходит событие от отправителя к получателю, от First Responder, по иерархии контроллеров, до root view controller, window object и последнего - app object.
> ````
> -UIControl Actions(например, нажатие кнопки)
> -User events: (touches, shakes, motion, etc...)
> -System events: (low memory, rotation, etc...)
> ````

- Как работают [`push нотификации`](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html)?
> [Push-уведомление](http://habrahabr.ru/post/156811/) — это короткое сообщение, состоящее из токена девайса, полезной нагрузки (payload) и ещё некоторой информации. Полезная нагрузка — это актуальные данные, которые будут отправляться на девайс.
 
Objective-C, [Foundation](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/ObjC_classic/index.html):
------------------------
- Опишите `основные понятия ОО программирования` в терминах Objective-C (`интерфейс, реализация, свойства, протоколы,` и т.д)
> ````
> @interface Начинает объявление класса или категории (категория – расширение класса дополнительными методами без наследования)
> @implementation Начинает определение класса или категории
> @protocol Начинает объявление протокола (аналог класса С++, состоящего из чисто виртуальных функций)
> @end Завершает объявление\определение любого класса, категории или протокола
> @private Ограничивает область видимости инвариантов класса методами класса (аналогично С++)
> @protected Стоит по умолчанию. Ограничивает область видимости инвариантов класса методами класса и методами производных классов (аналогично С++)
> @public Удаляет ограничения на облать видимости (аналогично С++)
> @try Определяет блок с возможной генерацией исключений (аналогично С++)
> @throw Генерирует объект-исключение (аналогично С++)
> @catch () Обрабатывает исключение, сгенерированное в предшествующем блоке @try (аналогично С++)
> @finally Определяет блок после блока @try, в который предается куправление независимо от того, было или нет сгенерировано исключение
> @class Сокращенная форма объявления класса (только имя (аналогично С++))
> @selector(method_name) Возвращает скомпилированный селектор для имени метода method_name
> @protocol(protocol_name) Ворзвращает экземпляр класса-протокола с именем protocol_name
> @encode(type_spec) Инициализирует строку символов, которая будет использована для шифрования данных типа type_spec
> @synchronized() Определяет блок кода, выполняющегося только одной нитью в любой определенный момент времени
> ````

- Что такое назначеный [`инициализатор`](https://developer.apple.com/library/ios/documentation/General/Conceptual/CocoaEncyclopedia/Initialization/Initialization.html#//apple_ref/doc/uid/TP40010810-CH6-SW1)['(designated initializer`)](https://developer.apple.com/library/ios/documentation/General/Conceptual/DevPedia-CocoaCore/Initialization.html#//apple_ref/doc/uid/TP40008195-CH21) , напишите любой элементарный инициализатор, почему он так выглядит? (имеется ввиду `if (self  = [super ...])`)?
> ````
> -(id)init {
>    if (self = [super init]) { // equivalent to "self does not equal nil"
>        date = [[NSDate date] retain];
>    }
>    return self;
>  }
> ````
> `designated initializer`  
>The designated initializer guarantees the object is fully initialised by sending an initialization message to the superclass. The implementation detail becomes important to a user of the class when they subclass it.

- Суть [`рантайма (Runtime)`](http://habrahabr.ru/post/177421/), отправление сообщения;
> Runtime - предоставляет набор функций в системе исполнения для выполнения скомпилированного кода
> Автоматический поиск переменных/методов. Apple уже реализовало это в виде Key-Value Coding: вы задаете имя, в соответсвии с этим именем получаете переменную или метод. Вы можете делать это и сами, если вас чем-то не устраивает реализация Apple.(прим. переводчика — например, вот так Better key-value observing for Cocoa)
> Автоматическая регистрация/вызов подклассов. Используя objc_getClassList вы можете получить список классов, уже известных Runtime и, проследив иерархию классов, выяснить, какие подклассы наследуются из данного класса. Это дает вам возможность писать подклассы, которые будут отвечать за специфичиские форматы данных, или что-то в этом роде, и потом дать суперклассу возможность находить их самому, избавив себя от утомительной необходимости регистрировать их все руками.
> Автоматически вызвывать метод для каждого класса. Это может быть полезно для unit-testing фреймворков и подобного рода вещей. Очень похоже на #2, но с акцентом на поиск возможных методов, а не на иерархию классов
> Перегрузка методов во время исполнения. Runtime предоставляет вам полный набор инструментов для изменения реализации методов классов, без необходимости изменять что-либо в их исходном коде
> Bridging Имеея возможность динамически создавать классы и просматривать необходимые поля, вы можете создать мост между Objective-C и другим (достаточно динамичным) языком.
>
>
> В Objective-C каждый вызов метода транслируется в соответствующий вызов функции objc_msgSend:
> ```` 
> // Вызов метода
> [array insertObject:foo atIndex:1];
> // Соответствующий ему вызов Runtime-функции
> objc_msgSend(array, @selector(insertObject:atIndex:), foo, 1);
> ````
> Вызов objc_msgSent инициирует процесс поиска реализации метода в кеш таблице методов класса вверх по иерархии наследования — в суперклассах данного класса. Если же и при поиске по иерархии результат не достигнут, запускается динамический поиск — вызывается один из специальных методов: resolveInstanceMethod или resolveClassMethod. Этот механизм позволяет реализовать Method Swizzling.


- Объявление `свойств (property)` `(retain, assign, nonatomic, readonly, copy)`. С подвохом: вопрос о несуществующем параметре `atomic`, что он означает? Как правильно реализовать сетер для свойства с параметром retain? Вопрос о циклах в графах владения, и почему свойства delegate (предоставляющие доступ к делегату) обычно задаются как `assign`?
> @property (<атрибуты>) Type* propertyName; 
> атрибуты:
> readwrite — у свойства есть как акцессор, так и мутатор. Является атрибутом по умолчанию.
> readonly — у свойства есть только акцессор.
>
> assign — для задания нового значения используется оператор присваивания. Используется только для POD-типов либо для объектов, которыми мы не владеем.
> retain — указывает на то, что для объекта, используемого в качестве нового значения instance-переменной, управление памятью происходит вручную (не забываем потом освободить память).
> copy — указывает на то, что для присваивания будет использована копия переданного объекта.
> weak — аналог assign при применении режима автоматического подсчёта ссылок. (ARC должен поддерживаться компилятором)
> strong — аналог retain при применении режима автоматического подсчёта ссылок. (ARC должен поддерживаться компилятором)
> 
> Директива @synthesize автоматически генерирует set- и get-методы. Требует dealloc без ARC. 
> @­synthesize property = _property; обязательно при одновременном переопределении set- и get-методов, для iVar не генерируется автоматически 
> @property лишь генерирует сигнатуры геттера и мутатора. Но если свойство синтезированное (через @synthesize или по умолчанию), то кроме этого генерируется и ivar.
 

- В чем разница между `точечной нотацией` и использованием квадратных скобок? 
> `точечная нотация` используется для обращения к свойствам обькта
> C использованием квадратных скобок - объекту посылается сообщение objc_msgSend

- Что происходит когода мы пытаемся вызвать метод у nil указателя?
>  objc_msgSend проверяет первый агрумент (получателя) и прерывается если получатель == nil

- Разница между nil и Nil?
>````
>  #define nil (id)0 -  это указатель на нулевой объект
>  #define NULL ((void *)0) - используется для указателей (тоже самое что nil) 
>  #define Nil (Class)0 - нулевой указатель типа Class
>  NSNull — это своего рода обёртка над NULL и nil, позволяющая хранить их в объектах-коллекциях Objective-C. 
>````


- Что такое [`селектор (selector)`](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/DevPedia-CocoaCore/Selector.html#//apple_ref/doc/uid/TP40008195-CH48-SW1)? 
> Селектор определяет метод для вызова.
Как его вызвать? 
> ````[object performSelector:aSelector];````
как отложить вызов селектора? 
>````
> performSelector:withObject:afterDelay:
> performSelector:withObject:afterDelay:inModes:
> performSelectorOnMainThread:withObject:waitUntilDone:
> performSelectorOnMainThread:withObject:waitUntilDone:modes:
> performSelector:onThread:withObject:waitUntilDone:
> performSelector:onThread:withObject:waitUntilDone:modes:
> performSelectorInBackground:withObject:
> cancelPreviousPerformRequestsWithTarget:
> cancelPreviousPerformRequestsWithTarget:selector:object:
> ````
> или 
> [`(NSInvocation)`](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSInvocation_Class/index.html#//apple_ref/doc/uid/20000212)
> 
Что делать если селектор имеет много параметров? 
Как запустить селектор во второстепенном `(фоновом) потоке`?
> так:
>```` dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
>        [self doSomething:param];
>     });````
> или так
> ````[myObj performSelectorInBackground:@selector(doSomething:) withObject:param];````
> или так
> ````[NSThread detachNewThreadSelector:@selector(doSomething:) toTarget:myObj withObject:param];````


- Как запустить `поток`? 
> [NSThread](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html#//apple_ref/doc/uid/10000057i-CH15-SW2)
> [NSThread detachNewThreadSelector:@selector(myThreadMainMethod:) toTarget:self withObject:nil];
>
> [NSStream](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Streams/Articles/CocoaStreamsOverview.html#//apple_ref/doc/uid/20002272-BABJFBBB)


- Что первым нужно сделать при запуске `потока`? `(NSAutoreleasePool)` 
> NSAutoreleasePool пулы обеспечивают механизм, посредством которого можно отправить объекту "отложенные" release сообщения.Каждый поток в Cocoa приложении сохраняет свой ​​собственный стек объектов NSAutoreleasePool

- Что такое [`runLoop`](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1), кодга он используется? `(timers, nsurlconnection ...)`
> [NSRunLoop `Циклы выполнения`](http://macbug.ru/cocoa/mthreadrunloops) - цикл обработки событий, который используются для планирования работы и координации получения входящих событий.
> Объект NSRunLoop также обрабатывает события NSTimer

- Что такое `делегат (delegate)`? 
> Другой вариант паттерна «Декоратор» — это [делегирование](http://habrahabr.ru/post/202960/). Механизм, при котором один объект взаимодействует от имени другого объекта (или в координации с ним).

- Как создать и [использовать](http://2tickets2dublin.com.ua/protocols_delegats_extensions_categories/) делегат? 
> ````@protocol CustomProtocol
> @required
> -(void)do_required;
> @optional
> -(void)do_optional;
> @end
> 
> @interface MyObject:NSObject
>  @property (nonatomic, weak) id  <CustomProtocol> delegate; 
> @end
> ````

- Как представлены `структуры C` (CGRect, CGSize, CGPoint) в Objective-C?
> Структура - это область в памяти, в которой содержаться ссылки на объекты (переменные). 


- Чем объект Objective-c отличается от [структуры С](https://ru.wikipedia.org/wiki/%D0%A1%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0_(%D1%8F%D0%B7%D1%8B%D0%BA_%D0%A1%D0%B8)), что такое структура в С.
> В языке Си, структура (struct) — композитный тип данных, инкапсулирующий без сокрытия набор значений различных типов. Порядок размещения значений в памяти задаётся при определении типа и сохраняется на протяжении времени жизни объектов, что даёт возможность косвенного доступа (например, через указатели)
> ````
> struct str_name
> {
> 	int	member_1;
> 	float	member_2;
> 	char	member_3[256];
> 	/* ... */
> };
>````
> Objective-c любую структуру данных, у которой есть указатель на класс в правильном местоположении, можно рассматривать как объект.
> ````
> typedef struct objc_object {
>    Class isa;
> } *id;
> ````


- Какие существуют [`root классы`](https://developer.apple.com/library/ios/documentation/General/Conceptual/DevPedia-CocoaCore/RootClass.html) в iOS? 
> root класс - это класс самого верхнего уровня наследования иерархии который  не наследуется от любого другого класса. Он предоставляет базовый функционал всем остальным классам фреймворка.
> в Objective-C 2 root классов - NSObject и NSProxy, которые является частью Foundation framework.


- Для чего нужны `root классы`? Корневые классы: NSObject, [NSProxy](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSProxy_Class/)? 
> NSObject является корневым классом большинства иерархий классов Objective-C. Через NSObject объекты наследуют базовый интерфейс к runtime.
> NSProxy реализует основные методы, необходимые из корневого класса, в том числе тех, которые определены в протоколе NSObject. В отличии от NSObject не предоставляет метода инициализации, и вызывает исключение при получении любого сообщения для которого нет обработчика.

- Как работает proxy? 
> NSProxy принимает сообщеине и перенаправляет его реальному обьекту или вызывает загрузку реального обьекта (сам стает нужным обьектом)

- Как имитировать множественное наследование?
> Objective-c не поддерживает множественное наследование, но поддерживает несколько корней.
> Основные опции для "имитации" - это категории, протоколы, композиция, message forwarding.


- `Тип id`. Что случится во время компиляции если мы посылаем сообщение объекту `типа id`? Что случится во время выполнения если этот метод существует? Что произойдет здесь (компиляция  + время выполнения): `NSString *s = [NSNumber numberWithInt:3]; int i = [s intValue];`
> Переменная типа id фактически является указателем на произвольный объект. Для обозначения нулевого указателя на объект используется константа nil.
При этом вместо id можно использовать и более привычное обозначение с явным указанием класса. В частности последнее позволяет компилятору осуществлять некоторую проверку поддержки сообщения объектами — если компилятор из типа переменной не может сделать вывод о поддержке объектом данного сообщения, то он выдаст предупреждение, а не ошибку. 


- Что такое `указатель isa`? Для чего он нужен?
> Каждый объект Objective-C содержит в себе атрибут isa — указатель на class object для данного объекта. class object автоматически создается компилятором и существует как один экземпляр, на который через isa ссылаются все экземпляры данного класса.


- Что происходит с методом после того, как он не нашелся в объекте класса, которому его вызвали? Цепочка ответсвенности, что происходит с методом после того как он не нашелся в объекте класса, которому его вызвали (в сторону [forwardInvocation:](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtForwarding.html))?
> Отправка сообщения обьекту без обработчика вызывает ошибку. Перед генерацией ошибки, runtime отправляет объекту forwardInvocation: сообщение с объектом NSInvocation в качестве единственного аргумента-объекта. NSInvocation инкапсулирует исходное сообщение и аргументы, которые были переданы с ним.


- Чем `категория` отличается от `расширения` (extension, наименованная категория)? `категория vs extension`?
> С помощью категорий добавляются новые методы в существующий класс
> Расширения особый случай категорий, которые позволяют определить методы, которые должны быть объявлены в основном блоке реализации.

- Можно ли добавить `ivar` в категорию?
> Нет, но с OSX10.6 и iOS3.1 это можно обойти это с помощью ассоциативных ссылок. Это делается с помощью objc_setAssociatedObject и objc_getAssociatedObject.

- Когда лучше использовать `категорию`, а когда `наследование`? `категория vs наследование`?
> при наследовании меняетcя поведение класса, обернув его в подкласс
> категория позволяет добавлять методы к существующим классам без наследования не создавая экземпляр класса, который она расширяет. Новые методы добавляются при компиляции и могут быть выполнены как обычные методы расширенного класса.

- Что такое `notifications (уведомления)`? как мы должны их использовать?
> В паттерне «Наблюдатель» один объект уведомляет другие объекты об изменениях своего состояния.

- Какая разница м/у использование `делегатов (delegation)` и `нотификейшенов (notification)`?
> delegation - механизм, при котором один объект взаимодействует от имени другого объекта (или в координации с ним).
> notification - Когда состояние меняется, все объекты-наблюдатели будут уведомлены об изменении.


- В чем разница между `NSArray и NSMutableArray`?
> Объект NSMutableArray управляет изменяемым массивом, который позволяет добавлять и удалять записи в любое время, автоматически выделяя память по мере необходимости.


- Чем отличается `NSSet от NSArray`? 
> NSSet
> используется для сравнения элементов
> не упорядочен 
> не допускает дубликаты
> NSArray
> доступ к элементам по индексу
> упорядочен
> может содержать дубликаты


- Какие `операции` происходят быстро в `NSSet` и какие в `NSArray`?
> [инфа](http://www.cocoawithlove.com/2008/08/nsarray-or-nsset-nsdictionary-or.html)
> перебор элементов быстрее с NSArray
> проверка на вхождение быстрее с NSSet


- [`Формальный и неформальный (informal)` протокол](https://developer.apple.com/library/ios/documentation/General/Conceptual/DevPedia-CocoaCore/Protocol.html)? Протоколы (protocols): основные отличия между c#/java интерфейсами и Objective-C протоколами. Что делать в случае если класс не реализует какой-то метод из протокола?
> Формальный протокол (formal protocol) обьявляет список методов (@required и @optional) которые должны быть реализованы в классе клиента.
> Неформальный протокол (informal protocol) является категорией NSObject, которая неявно делает почти все объекты унаследованными от протокола. (Категория функция языка, который позволяет добавлять методы в класс без наследования ее.) Реализация методов - @optional. Перед вызовом метода необходимо проверить реализацию в объекте.



- Есть ли `приватные и защищенные` методы в Objective-C?
> Все методы публичны



- Что такое `быстрое перечисление (fast enumeration)`? 
> это итерация по обьектам любого класса, который реализует протокол NSFastEnumeration, в том числе NSArray, NSSet и NSDictionary. 
> Реализация протокола состоит из одного метода:
> ```` -(NSUInteger)countByEnumeratingWithState:(NSFastEnumerationState *)state objects:(id *)stackbuf count:(NSUInteger)len; ````



- Что такое [`KVO`](http://habrahabr.ru/company/eastbanctech/blog/202884/)? Когда его нужно использовать? Методы для обозревания объектов? Работает ли `KVO с instance переменными (полями)` объекта?
> KVO (key-value observing) [docs](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/KeyValueObserving/KeyValueObserving.html) — еще одна реализация патерна наблюдатель. В этом случае наблюдатель следит не за событиями, а за конкретным свойством (property) объекта. Когда значение этого свойства меняется, наблюдателю приходит уведомление и он соответствующим образом реагируют.
> addObserver:forKeyPath:options:context:  //подписаться на уведомления
> observeValueForKeyPath:ofObject:change:context: //уведомить об изменении


- Что такое `KVC`? Когда его нужно использовать?
> [docs](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/KeyValueCoding/Articles/KeyValueCoding.html)
> KVC (Key-Value Coding) представляет собой механизм для доступа к свойству объекта косвенно, с помощью строк для идентификации свойств, а не через вызов аксессора или доступ к ним непосредственно через переменных экземпляра. 
> Часто используется для фильтрации в массивах (NSPredicate)


- Как удалить объект в ходе итерации по циклу?


- Как лучше всего загрузить `UIImage c диска(с кеша)`?
> В iOS присутствует функция кэширования, но прямого доступа к данным в кэше нет. Для получения доступа следует использовать класс [NSCache](https://developer.apple.com/library/prerelease/mac/documentation/Cocoa/Reference/NSCache_Class/index.html). NSCache — это объекты, которые реализуют протокол NSDiscardableContent. Класс NSCache включает в себя различные политики автоматического удаления, обеспечивающие использование не слишком большого количества памяти системы.

- Какой контент лучше хранить в `Documents`, а какой в `Cache`?
> NSDocumentDirectory - контент, созданный самим пользователем
> Library/Caches - все остальное


- Как связаны `NSRunLoop и NSAutoreleasePool` [на пальцах](http://brain-twists.blogspot.com/2012/03/nsrunloop-autorelease-pool.html)?
> NSRunLoop запускается внутри NSAutoreleasePool который управляет памятью обьектов.

- Почему нам не следует вызывать `instance методы в методе initialize`?


- `NSCoding, archiving`
> NSCoding это протокол для сериализации и десериализации  данных. Реализуется двумя методами: -initWithCoder: и encodeWithCoder :. Классы, которые соответствуют NSCoding могут быть заархивированы с NSKeyedArchiver/NSKeyedUnarchiver


- Протокол [`NSCopying`](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSCopying_Protocol/index.html), почему мы не можем просто использовать любой собственный объект в качестве ключа в словарях (NSDictionary) , что нужно сделать чтобы решить эту проблему? (разница между глубоким и поверхностным копированием)
> NSCopying используется для создания копии экземпляра класса со всеми его свойствами
> Реализуется с помощью метода:
>```` -(id)copyWithZone:(NSZone *)zone ````

Memory Management:
------------------
- Как происходит `ручное управление памятью - MRC` в iOS?
> retain/release/autorelease

- `autorelease vs release`?
> release сообщение уменьшит retain count на 1, если retain count == 0, обьект уничтожится
> autorelease сообщение добавляет обьект в текущий NSAutoreleasePool. При очистке NSAutoreleasePool отправит всем инстансам -release сообщение 


- Что означает `ARC`?
> Automatic Reference Counting


- Что делать, если проект написан с использованием ARC, а нужно использовать классы сторонней библиотеки написанной без ARC?
> Добавить флаг  -fno-obj-arc в "Build phases->Compile Sources"


- `Weak vs assign`, `strong vs copy`?
> weak - arc аналог assign. В ARC assign используется для примитивных типов таких как BOOL, int, float.
> copy - подобно strong только делает копию обьекта и стоновится его владельцем,также предотвращает возможность изменения обьекта извне.
> strong - стает владельцем обьекта

- `Atomic vs nonatomic`. Чем отличаются? Как вручную переопределить atomic/nonatomic сеттер в не ARC коде?
> Многопоточный доступ — atomic/nonatomic( синхронизировать чтение/запись между потоками или нет)


- Зачем все свойства ссылающиеся на делегаты `strong/retain`. :))) 
> Это бред

- Что такое `autorelease pool`?
> Autorelease pool - это механизм, который позволяет посылать отложенное сообщение об освобождении объекта.

- Как можно заимплементировать `autorelease pool на с++`?


- Если я вызову `performSelector:withObject:afterDelay:` - объекту пошлется сообщение retain?
- Как происходит обработка `memory warning`(предупреждение о малом  количестве памяти)? Зависит ли обработка от версии iOS, как мы должны их обрабатывать?
- Напишите простую реализацию `NSAutoreleasePoll` на Objective-C
- Когда нужно использовать метод `retainCount` (никогда, почему?) Объясните что такое `подсчет ссылок (retain count`)?
- Темы управления памятью, такие как владение `retain/release/autorelease`. 
- Что случится если вы добавите только что созданный объект в `Mutable Array`, и пошлете ему сообщение `release`? Что случится если послать сообщение `release` массиву? Что случится если вы удалите объект из массива и попытаетесь его использовать?

- С подвохом: `сборщик мусора` для iPhone.
> сборщика мусора в iPhone нет

- Нужно ли `ретейнить` (посылать сообщение retain) `делегаты`?
> нет, обьект не должен являться влядельцем делегата

- Опишите правильный способ управленя памятью выделяемой под `Outlet'ы`?
> ARC - память управляется автоматически
> non-ARC - нужно освобождать обьекты в dealloc

- Реализуйте следующие методы: `retain, release, autorelease`?

Networking:
----------
- Преимущества и недостатки `синхронного и асинхронного` соединения?
- Что означает [`http`](https://ru.wikipedia.org/wiki/HTTP), [`tcp`](https://ru.wikipedia.org/wiki/TCP)?
> HTTP (HyperText Transfer Protocol — «протокол передачи гипертекста») — протокол прикладного уровня передачи данных.
> TCP (англ. Transmission Control Protocol, протокол управления передачей) — один из основных протоколов передачи данных Интернета, предназначенный для управления передачей данных в сетях и подсетях TCP/IP. 


- Какие различия между `HEAD, GET, POST, PUT`? 
> [HTTP](https://ru.wikipedia.org/wiki/HTTP)


- Как загрузить что-то из интернета? В чем разница между `синхронными и асинхронными запросами`? Небольшое задание. Опишите как загрузить изображение из интернета и отобразить его в ImageView — все это должно происходить после нажатия кнопки.

Multithreading:
---------------
- Что такое `deadlock`?
> Deadlock — ситуация в многозадачной среде или СУБД, при которой несколько процессов находятся в состоянии бесконечного ожидания ресурсов, захваченных самими этими процессами.
>
>````
> dispatch_queue_t q = dispatch_queue_create("deadlock queue", DISPATCH_QUEUE_SERIAL);
> NSLog(@"1");
> dispatch_async(q, ^{
>     NSLog(@"2");
>     dispatch_sync(q, ^{
>         NSLog(@"3"); //этот код не выполнится
>     });
>     NSLog(@"4"); //этот код не выполнится
> });
> NSLog(@"5");
> 
>````
> Результат
> 1
> 5
> 2


- Что такое `livelock`?
> livelock частая проблема в асинхронных системах. Потоки почти не блокируются на критических ресурсах. Вместо этого они выполняют свою небольшую неблокируемую задачу и отправляют её в очередь на обработку другими потоками. Может возникнуть ситуация, когда потоки друг другу начинают перекидывать какое-то событие и его обработка зацикливается. Явного бесконечного цикла, как бы, не происходит, но нагрузка на асинхронную систему резко возрастает. В результате чего эти потоки больше ничем не успевают занимаются.


- Что такое [`семафор (semafor)`](http://idev.by/ios/22699/)?
> Семафор позволяет выполнять какой-либо участок кода одновременно только конкретному количеству потоков. В основе семафора лежит счетчик, который и определяет, можно ли выполнять участок кода текущему потоку или нет. Если счетчик больше нуля — поток выполняет код, в противном случае — нет.
> В GCD выглядит так:
> semaphore_create – создание семафора (аналог sem_init)
> semaphore_destroy – удаление, соответственно (аналог sem_destroy)
> semaphore_wait – блокирующее ожидание на семафоре (аналог sem_wait)
> semaphore_signal – освобождение семафора (аналог sem_post)

- Что такое `мьютекс (mutex)`?
> [wiki](https://ru.wikipedia.org/wiki/%D0%9C%D1%8C%D1%8E%D1%82%D0%B5%D0%BA%D1%81), [docs](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Multithreading/ThreadSafety/ThreadSafety.html#//apple_ref/doc/uid/10000057i-CH8-SW1)
> Мьютексы — это простейшие двоичные семафоры, которые могут находиться в одном из двух состояний — отмеченном или неотмеченном. Отличается от семафора тем, что только владеющий им поток может изменить отмеченное состояние

- `Асинхронность` vs `многопоточность`. Чем отличаются?
> Асинхронность говорит о порядке исполнения кода. Если вызываемая функция не возвращает значение сразу, а отдаёт управление вызывающему коду с обещанием выдать значение позже, то эта функция асинхронная. При этом нет никаких предположений о том, как это значение будет считаться: параллельно или нет.
> Многопоточность говорит о том, что в физически происходит несколько потоков одновременно.
>
> [Многопоточность](http://idev.by/ios/6599/) - каждый поток имеет свой стек и планируется на исполнение отдельно kernel’ом. Поток может общаться с другими потоками. Все потоки находятся в общем адресном пространстве приложения и делят одну и ту же виртуальную память и имеют те же права доступа что и процесс приложения.
> [Асинхронность](http://pragmaticperl.com/issues/21/pragmaticperl-21-%D0%B5%D1%89%D0%B5-%D0%BD%D0%B5%D0%BC%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BE%D0%B1-%D0%B0%D1%81%D0%B8%D0%BD%D1%85%D1%80%D0%BE%D0%BD%D0%BD%D0%BE%D0%BC-%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B8-%D0%BD%D0%B0-anyevent.html) Асинхронные событиямя выполняются независимо от основного потока в неблокирующем режиме, что позволяет основному потоку программы продолжить обработку. Т/е/ результат работы функции приходит не сразу после вызова, а когда-нибудь потом.
>
> в многопоточной реализации бывают случаи когда потоки простаивают в ожидании входных данных тем самым расходуя общие ресурсы
> асинхронность позволяет всегда занять процессор какими то действиями ставя все события в очередь


- Какие технологии в iOS возможно использовать для работы с потоками. Преимущества и недостатки.
- Чем отличается `dispatch_async от dispatch_sync`?
> [docs](https://developer.apple.com/library/prerelease/ios/documentation/Performance/Reference/GCD_libdispatch_Ref/index.html)
> dispatch_async ставит копию блока на выполнение в очередь и немедненно возвращает управление 
> dispatch_sync ставит ссылку блока на выполнение в очередь и ожидает завершения операции 


- Для чего при разработке под iOS использовать `POSIX-потоки`? `pthread_create(&thread, NULL, startTimer, (void *)t);`
> [docs](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Multithreading/CreatingThreads/CreatingThreads.html)
> NSThread - это надстройка для pthreads


- А чем реально `POSIX-потоки` лучше чем `GCD или NSOperationQueue вместе с NSOperation`? Приходилось ри реально использовать POSIX и как в этом были прюсы? Реально, просто интересно…
 `Use POSIX calls if cross-platform portability is required. If you are writing networking code that runs exclusively in OS X and iOS, you should generally avoid POSIX networking calls, because they are harder to work with than higher-level APIs. However, if you are writing networking code that must be shared with other platforms, you can use the POSIX networking APIs so that you can use the same code everywhere. `
> [read](http://blog.spec-india.com/difference-between-nsthread-and-nsoperation)


UIKit:
------
- Разница между свойствами `bounds и frame` объекта UIView? Понимание системы координат?
> frame – это прямоугольник описываемый положением location(x, y) и размерами size (width, height) вьюхи относительно ее superview в которой оа содержится. 
> bounds – это прямоугольник описываемый положением location(x, y) и размерами size (width, height) вьюхи относительно ее собственной систмы координат (0, 0).


- Какие бывают `состояния` у приложения?
> [docs](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/TheAppLifeCycle/TheAppLifeCycle.html#//apple_ref/doc/uid/TP40007072-CH2-SW1)
> 1 Not running - не запущено
> 2 Inactive - работает в фоне но не обрабатывает события (в основном это промежуточное состояние при переходе между состояниями)
> 3 Active - работает и обрабатывает события
> Background - фоновый режим в который приложение получает управление на некоторое время
> Suspended - фоновый режим в который приложение "спит". Этот режим инициализируется системой


- Цикл жизни [`UIViewController`](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/)?
> [read](http://habrahabr.ru/post/129557/), 
> Создание
>    init
>    initWithNibName:
> Создание view
>    (BOOL)isViewLoaded
>    loadView
>    viewDidLoad
>    (UIView*) initWithFrame:(CGRect)frame
>    (UIView*) initWithCoder:(NSCoder *)coder
> Обработка изменения состояния view
>    viewDidLoad
>    viewWillAppear:(BOOL)animated
>    viewDidAppear:(BOOL)animated
>    viewWillDisappear:(BOOL)animated
>    viewDidDisappear:(BOOL)animated
>    viewDidUnload
> Обработка memory warning
>    didReceiveMemoryWarning
> Уничтожение
>    viewDidUnload
>    dealloc



- Что такое `View` (представление) и что такое `window`?
> [docs](http://developer.apple.com/library/ios/#documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503), [read](http://www.techotopia.com/index.php/Understanding_iPhone_Views,_Windows_and_the_View_Hierarchy)
> window экземпляр класса UIWindow занимается отображеним видимой View иерархии. Является корневым представлением.
> UIView - это основной обьект для взаимодействует с пользователем. Основные задачи:
> 1 Layout and subview management
> 2 Drawing and animation
> 3 Event handling


- Какого [разрешение экранов iphon'ов](http://www.idev101.com/code/User_Interface/sizes.html), и в чем разница между `points (точками)` и `пикселями (pixels)`?
> pixels (px) - точки на экране
> points (pt) - плотность точек на экране


- Что означают `IBOutlet` и `IBAction`, для чего они нужны, и что значат для препроцессора?
> [read](http://nshipster.com/ibaction-iboutlet-iboutletcollection/)
> ````
>		#define IBAction void
>		#define IBOutlet
> ````
> Используются для Interface Builder


- Как работает `UITableView`?

- Как многопоточность работает с `UIKit`?
> Все операции с UI должны происходить в гравном потоке


- Что можно сделать если клавиатура при появлении скрывает важную часть интерфейса?
- Почему мы должны `релизить IBOutlet'ты` во viewDidUnload?
- Что такое `awakeFromNeeb`, в чем разница между `xib и nib` файлами?
> xib - новый формат IB(с версии 3) nib который хранится в текстовом файле, что делает его более подходящим для хранения в системах контроля версий

- Иерархия наследования [UIButton](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIButton_Class/).
> NSObject->UIResponder->UIView->UIControl->UIButton

Базы данных, CoreData:
----------------------
- Составить SQL запрос на выборку всех проектов  на которых сидит девелопер с
id ==3. (`Developers:id,name; Projects:id,name; Developers&Projects:project_id,developer_id`)?
- Зачем нужно делать `двустороннии связи` в таблицах?

- Что такое [`Core Data`](http://habrahabr.ru/post/191334/)?
> Core Data - это фрэймворк для работы с хранимыми на устройстве данными


- В каких случаях лучше использовать `SQLite`, а в каких `Core Data`?
> В большинстве случаев Core Data хранит данные в SQLite



- Что такое `контекст (Managed object context)`? Как происходят `изменения в NSManagedObjectContext`?
> NSManagedObjectContext - это среда в которой находится объект и которая следит за состоянием обьекта и зависимыми объектами.


- Что такое `Persistent store coordinator`? Зачем нужен `NSPersistentStoreCoordinator`?
> NSPersistentStoreCoordinator отвечает за хранение объектов данных которые передаются из NSManagedObjectContext


- Какие есть нюансы при использовании `Core Data в разных потоках`? Как `синхронизировать данные между потоками`(Как синхронизировать контекст)? Синхронизация разных типов NSManagedObjectContext (получение и изменение данных в child контекстах)? 
> NSManagedObjectContext не thread-safe
> [read](http://habrahabr.ru/post/218457/)
> для многопоточности основная идеа - создавать для кажного потока свой NSManagedObjectContext и потом синхронизтровать


- Использовали ли `NSFetchedResultsController`? Почему? 
> NSFetchedResultsController представляет собой контроллер, предоставляемый фрэймворком Core Data для управления запросами к хранилищу.
> Использование NSFetchedResultsController становится актуальным для больших обьемов данных и операчиями над ними. NSFetchedResultsController предоставляет механизм для обработки данных (изменения, удаления, добавления) и отображает эти изменения в таблице.


- Что такое [`Fault`]() и зачем он нужен?
>  Fault является прототипом объекта, который представляет собой управляемый объект, который еще не был полностью реализован, или коллекцию объектов, которые представляют отношения:
>  -Управляемый объект понижает экземпляр соответствующего класса, но его постоянные переменные не инициализируются.
>  -Отношение понижения является подклассом класса коллекции, который представляет отношения.

- Что таке [`Fetched Property`](http://www.cimgf.com/2014/01/01/fetched-properties-useful/) и особенности работы с ним по сравнению с обычной связью?
> Это свойство NSManagedObject которое хранит NSFetchRequest


- Что такое [`NSManagedObjectId`](http://macbug.ru/cocoa/coredatausing)? Можем ли мы сохранить его на потом если приложение закроется?
> NSManagedObjectID объект является универсальным идентификатором для управляемого объекта, а также предоставляет основу для уникальности в структуре Core Data. NSManagedObjectID – универсальный потокобезопасный идентификатор. Бывает временным и постоянным. Используется в случае передачи объекта из одного контекста в другой.


- Какие [`типы хранилищ`](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CoreData/Articles/cdPersistentStores.html) поддерживает CoreData?
> XML
> SQLite
> In-Memory
> Binary


- Что такое `ленивая загрузка (lazy loading)`? Что ее связывает с CoreData? Опишите ситуация когда она может быть полезной?
> Это автоматическая подгрузка fault зависимостей 
> lazy loading лучше для использования памяти, и быстрее, для извлечения связанных больших или редкоиспользуемых объектов

CoreAnimation, CoreGraphics:
----------------------------
- Чем отличается `UIView от CALayer`?
> в UIView добавлены обработчики событий которых нет в CALayer

- Какие типы `CALayer` есть?
> CATextLayer
> CAOpenGLLayer
> CATiledLayer
> CALayer


- Чем отличается [`UIView based Animation`](http://www.erudenko.com/2013/05/uiview.html) от [`Core Animation`](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CoreAnimation_guide/CoreAnimationBasics/CoreAnimationBasics.html)?
> UIView Animation - это по факту Cocoa оболочка над CoreAnimation, но с упрощенным интерфейсом


- [Тайминги](http://macbug.ru/cocoa/canimation04) в `CoreAnimation`?
> Классы анимации и протокол CAMediaTiming предоставляют функции для управления продолжительностью анимации, темпом (как интерполированные значения распределяются по длительности), повторить ли анимацию и сколько раз, следует ли автоматически обратная когда каждый цикл завершается, и ее визуальное состояние, когда анимация завершена.


- Что такое `backing store`?
- Чем отличаются `аффинные преобразования от трехмерных`?
- Нужно ли `ретейнить (посылать сообщение retain)` делегат для `CAAnimation`?


- Чем отличается include от import?
> #import //защищен от многократного включения кода

- Для чего нужны методы isKindOfClass isMemberOfClass?
> isKindOfClass - проверяет иерархию классов
> isMemberOfClass - проверяет конкретный класс


Algorithms:
-----------
- Напишите код, который `разворачивает строку на С++`. (переставить символы в строке в обратном порядке)?
- Поменять местами a и b не используя промежуточную переменную?
> ````a=3;
> b=5;
> a=a+b;
> b=a-b;// здесь уже будет 3
> a=a-b; // а теперь равно 5````
>
> [или так](http://ideone.com/nEzFkn)
> ````
> int a=3, b=5;
> a^=b^=a^=b;
> cout<<a<<endl<<b; 
> ````

- Написать функцию вычисления n-го числа последовательности фебоначи. (если решить через рекурсию, спросят чем опасно такое решение)?
- Решить задачку о массиве: дан массив из 1001 элемента в котором присутсвуют все числа от 1 до 1000 и одно повторяется дважды, узнать какое, если к каждому элементу можно обратиться только 1 раз?
- Как из строки вытащить подстроку?

Logical:
--------
- Есть 4 человека, каждый проходит мост за 1, 2, 5, и 10 минут соответственно. Через мост они могут переходить только парами, держась за руку и только с фонариком. Притом один должен вернуться обратно и передать фонарик. Необходимо переправить всех за 17 мин на другую сторону. Задача решаема.


Code Puzzels:
-------------
- Что не так с этим кодом? Зачем нужны `инициализаторы`?

```objective-c
[[[SomeClass alloc] init] init];
```

- Сработает ли `таймер`? Почему? 

```objc
void startTimer(void *threadId) 
{
   [NSTimer  scheduleTimerWithTimeInterval:10.0f 
      target:aTarget 
          selector:@selector(tick: ) 
          userInfo:nil
           repeats:NO];
}

pthread_create(&thread, NULL, startTimer, (void *)t);
```

- Какой метод вызовется: класса A или класса B? Как надо изменить код, чтобы вызвался метод класса A?

```objc
@interface A : NSObject
- (void)someMethod;
@end

@implementation A
- (void)someMethod
{
    NSLog(@"This is class A");
}
@end

@interface B : A
@end

@implementation B
- (void)someMethod 
{
    NSLog(@"This is class B");
}
@end

@interface C : NSObject
@end

@implementation C
- (void)method 
{
    A *a = [B new];
    [a someMethod];
}
```

- В каких случаях лучше использовать `strong`, а в каких `copy` для NSString? Почему?
> Чтобы предотвратить изменения другими обьектами
```objc
@property (nonatomic, strong) NSString *someString;
@property (nonatomic, copy) NSString *anotherString;
```

- Что выведется в консоль? Почему?
```objc
- (BOOL)objectsCount
{
    NSMutableArray *array = [NSMutableArray new];
    for (NSInteger i = 0; i < 1024; i++) 
    {
        [array addObject:[NSNumber numberWithInt:i]];
    }
    return array.count;
}

- (void)someMethod 
{
    if ([self objectsCount]) 
    {
        NSLog(@"has objects");
    }
    else
    {
        NSLog(@"no objects");
    }
}
```

- Выведется ли в дебагер «Hello world»? Почему?

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    dispatch_sync(dispatch_get_main_queue(), ^{
        NSLog(@"Hello world");
    });

   /* Another implementation */
   return YES;
}
```

- Что выведется в консоль?

```objc
 dispatch_async(dispatch_get_main_queue(), ^
    {
        NSLog(@"A %d", [object retainCount]);
        dispatch_async(dispatch_get_main_queue(), ^
        {
            NSLog(@"B %d", [object retainCount]);
        });
        NSLog(@"C %d", [object retainCount]);
    });
    NSLog(@"D %d", [object retainCount]);
```

- Что произойдет при исполнении следующего кода? 

```objc
Ball *ball = [[[[Ball alloc] init] autorelease] autorelease];
```
Additional:
-----------------------------
- Анкета в которой просят оценить свои знания по технологиям по 10 бальной шкале.
