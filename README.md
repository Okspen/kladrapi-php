PHP API "КЛАДР в облаке"
========================

Предоставляет классы для удобной работы с сервисом  [kladr-api.ru] [1].

Описание API
------------

**Kladr\Api**

Контроллер доступа к сервису

Функции
* *QueryToJson(Query $query, $assoc = false)* - выполняет запрос к сервису
* *QueryToArray(Query $query)* - выполняет запрос к сервису, возвращая данные в виде ассоциативного массива
* *QueryToObjects(Query $query)* - выполняет запрос к сервису, возвращая данные в виде массива объектов КЛАДР

Свойства
* *Error* - текст последней, возникшей при обращении к сервису, ошибки



**Kladr\Query**

Объект запроса к сервису

Свойства
* *ParentType* - тип родительского объекта для ограничения области поиска (регион, район, город)
* *ParentId* - идентификатор родительского объекта для ограничения области поиска
* *ContentType* - тип искомого объекта (регион, район, город)
* *ContentName* - название искомого объекта
* *Zip* - почтовый индекс искомого объекта
* *OneString* - выполнить поиск по всему адресу (одной строкой), при включении этой опции результат нельзя получить в виде объектов КЛАДР, только в виде ассоциативного массива
* *WithParent* - получить объекты вместе с родителями (если true у объекта заполняется свойство Parent)
* *Limit* - ограничение количества возвращаемых объектов



**Kladr\Object**

Объект КЛАДР

Свойства
* *Id* - идентификатор объекта
* *Name* - название объекта
* *Zip* - почтовый индекс объекта
* *Type* - подпись объекта полностью (область, район)
* *TypeShort* - подпись объекта коротко (обл, р-н)
* *Okato* - ОКАТО объекта
* *ContentType* - Тип объекта из перечисления ObjectType
* *Parents* - массив родительских объектов (заполняется если в запросе был установлен флаг WithParent)



**Kladr\ObjectType**

Перечисление типов  объектов, используемых в запросах к сервису

Константы
* *Region* - регион
* *District* - район
* *City* - населённый пункт
* *Street* - улица
* *Building* - строение

Примеры
-------

Получение списка всех населённый пунктов, название которых начинается на "Арх"

`````php
// Инициализация api, в качестве параметров указываем токен и ключ для доступа к сервису
$api = new Kladr\Api('51dfe5d42fb2b43e3300006e', '86a2c2a06f1b2451a87d05512cc2c3edfdf41969');

// Формирование запроса
$query = new Kladr\Query();
$query->ContentName = 'Арх';
$query->ContentType = Kladr\ObjectType::City;
$query->WithParent = true;
$query->Limit = 2;

// Получение данных в виде ассоциативного массива
$arResult = $api->QueryToArray($query);
`````

Лицензия
--------
Решение распространяется под лицензией «Общественное достояние» (Public Domain) и может быть свободно используемо любым лицом без выплат авторских вознаграждений.

[1]: http://kladr-api.ru/        "КЛАДР API"
