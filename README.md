# Box2D For Anthill

Данный плагин используется для удобной интеграции и простого использования физического движка **Box2D** в связке с **Anthill**. Плагин решает большинство вопросов о связи и использовании физики в **Anthill**.

Плагин Box2D для Anthill создавался под определенные задачи и поэтому не охватывает всех возможностей **Box2D 2.0.1a**, но вы легко можете расширять и дополнять его функционал на свое усмотрение.

## Установка

Чтобы установить плагин Box2D для Anthill следуете следующим шагам:

1. Создайте и настройте **AS3 проект** ([инструкции](http://anthill.ant-karlov.ru/wiki/guide:setup)).
2. Установите и настройте **Anthill** ([инструкции](http://anthill.ant-karlov.ru/wiki/guide:hello_world)).
3. Скачайте **Box2D 2.0.1a** ([ссылка](http://anthill.ant-karlov.ru/downloads/Box2D.zip)).
4. Скачайте плагин **Box2D для Anthill** ([ссылка](https://github.com/AntKarlov/Box2D-For-Anthill/archive/master.zip)).
5. Распакуйте и поместите **исходники Box2D** в **исходную папку с вашим проектом**.
6. Распакутей **архив с плагином Box2D** в удобное для вас место.
7. Скопируйте папку **"box2d"** из **"ru/antkarlov/anthill/plugins/box2d"**, и вставьте её в **"ru/antkarlov/anthill/plugins/"** для вашего проекта.
8. Установка завершена!

## Первые шаги

После того как проект настроен и плагин установлен, вы можете начать работу с физикой следуя следующим примерам.

Создание физического мира:

	var physicWorld:AntBox2DManager = new AntBox2DManager();
	physicWorld.create();

Включение отладочной отрисовки:

	physicWorld.enableDebugDraw = true;

Создание физической формы:

	var myShape:AntBox2DBoxShape = new AntBox2DBoxShape();
	myShape.width = 50;
	myShape.height = 50;

	// Смещение формы относительно физ.тела.
	myShape.x = -10;
	myShape.y = 10;

	// Плотность.
	myShape.density = 1;

	// Эластичность (прыгучесть).
	myShape.restitution = 0.1;

	// Трение.
	myShape.friction = 0.5;

Создание физического тела:

	var body:AntBox2DBody = new AntBox2DBody();

	// Применям одну или несколько ранее созданных форм! 
	// Формы можно изменять и применять после создания физ.тела.
	body.applyShapes(myShape, myShape2);

	// Устанавливаем позицию тела в пикселях.
	body.reset(100, 100);
	
	// Делаем тело динамическим.
	body.kind = "dynamic";
	
	// Инициализация.
	body.create();

Прикрепления спрайта к физическому телу:
	
	// Физ.тело унаследовано от AntActor, поэтому вы можете работать с ним как с актером.
	body.addAnimationFromCache("MyGreatCachedClipName");
	
	// Так же, после создания физ.тела, не забываем его
	// добавить в наш визуальный мир.
	myEntity.add(body);
	
Создание соеденения:

	var joint:AntBox2DRevoluteJoint = new AntBox2DRevoluteJoint();

	// Глобальное положение соеденения в пикселях.
	joint.x = 100;
	joint.y = 100;

	// Ограничение на вращение (если нужно).
	joint.enableLimit = true;
	joint.lowerAngle = AntMath.toRadians(-90);
	joint.upperAngle = AntMath.toRadians(90);

	// Инициализация.
	joint.create(body1, body2);

Фильтр столкновений:
	
	// Объект "ящик" будет сталкиваться только с "землей"
	// и "бочками".
	body.applyCollisionFlag("box");
	body.applyCollidesFlags([ "ground", "barrel" ]);
	
	// Чтобы "бочки" и "земля" следовали выше обозначенному
	// правилу, для них флаги должны быть установлены 
	// таким же образом.
	barrelBody.applyCollisionFlag("barrel");
	barrelBody.applyCollidesFlags([ "ground", "box" ]);

	groundBody.applyCollisionFlag("ground");
	groundBody.applyCollidesFlags([ "box", "barrel" ]);

	// Следуя выше обозначенным правилам "бочки" не будут
	// сталкиваться между собой как и "ящики". Но это
	// можно исправить добавив флаг "box" для объекта "ящика":
	body.applyCollisionFlag("box");
	body.applyCollidesFlags([ "ground", "barrel", "box" ]);

Удаление физ.объектов или соеденений:

	body.kill();
	joint.kill();

Не забывайте, что вы можете переиспользовать физ.объекты и соеденения:

	body = myEntity.recycle() as AntBox2DBody;
	joint = myEntity.recycle() as AntBox2DRevoluteJoint;

Это основа использования плагина **Box2D для Anthill**.

## Дополнительно

В ближайшее время будет создана более подробная инструкция по работе с плагином, а так же будут подготовлены примеры.

Приятного использования!
