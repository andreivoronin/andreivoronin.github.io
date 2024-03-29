---
layout: post
title: Базовые принципы проектирования
permalink: design-basic
date: 2017-08-10 18:00:00 +0400
tags: design basic
subtitle: Отзывчивость, надежность и скромность
favorite: true
---

Выполняя базовые принципы проектирования, дизайнеры взаимодействия и разработчики могут создавать системы, отвечающие ожиданиям человека. Такие системы люди будут считать естественными. Ниже представлен список принципов с характерными примерами.

## 1. Отзывчивость
> Реакция должна быть мгновенной, независимо от сложности процесса и доступных ресурсов.

### Закрытие приложений должно быть мгновенным, независимо от обстоятельств.

**Плохо: закрытие приложений во "взрослых" операционных системах.** Закрытие приложений на Windows/macOS/Linux происходит зачастую не сразу. Могут появляться уведомления о сохранение, о незаконченности действий. Приложение так же может просто подвиснуть.

![Windows app close](/img/design-basic/windows-app-close.png)

*Плохо: уведомление закрытия блокнота в Windows*

**Хорошо: закрытие приложение в мобильных операционных системах.** Закрытие приложений на iOS/Android происходит сразу же при нажатии кнопки Home. На телефонах это критически необходимо, т. к. человека в любой момент может что-то отвлечь. Приложения на телефонах рассчитаны, что их в любой момент могут "убить".

<iframe width="315" height="560" src="https://www.youtube.com/embed/Lk-3Ga7SZHU?autoplay=1&amp;loop=1&amp;mute=1&amp;rel=0&amp;controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>
*Хорошо: мгновенное закрытие Tweetbot в iOS*

**Вывод:** приложения должны быть рассчитаны, что их в любой момент могут закрыть. При закрытии приложение не должно делать никаких уведомлений и запросов у человека. Помнить, что "закрыть" ≠ "завершить работу приложения". Сначала можно, и нужно, скрывать приложение. Затем в фоне делать необходимые действия: сохранения, оптимизации, обновления.

### Реакция сетевых приложений должна быть мгновенной и позитивной

**Плохо: переключение на следующее фото в Twitter.** При переключении на следующее фото нет никакой реакции. Непонятно: ты плохо нажал или фотография ещё грузится. Особенно это заметно при плохом интернете. 

![Feedback Twitter](/img/design-basic/feedback-twitter.gif)

*Плохо: медленное переключение фото в Twiiter*

**Хорошо: Like в Facebook.** Если тебе понравилось сообщение, то ты можешь сразу поставить Like и увидеть при этом обратную реакцию, хотя сетевой запрос ещё не дошел до сервера. Интернета в этот момент может вообще не быть. 

![Feedback Facebook](/img/design-basic/feedback-facebook.png)

*Хорошо: мгновенная обратная реация Like в Facebook*

**Вывод:** сетевые приложения должны понимать, что интернет может быть плохой или его не может быть вовсе. И это не какой-то крайний случай, это обычная жизнь приложения. Сейчас у человека быстрый 4G, он заходит в метро, и у него 2G с задержками и потерей сетевых пакетов. У человека при этом не должен ухудшиться опыт использования приложения.

### Появление контента (или его placeholder'а) должно быть мгновенным

**Плохо: открытие приложения Twitter.** При открытии Twitter появляется анимированный экран загрузки — увеличивающаяся птица. В результате загрузка воспринимается дольше и нет ощущения, что приложение сразу же готово к использованию.

![Open Twitter](/img/design-basic/open-twitter.webp)

*Плохо: брендированное открытие приложения Twitter*

**Хорошо: загрузка поста в Facebook.** При открытии Facebook появляется загрузка поста в примерном будущем его виде. Ты уже можешь подсознательно подготовиться понять расположение элементов на странице и подготовиться к чтению. Похожий эффект создаётся в прогрессивном JPEG, когда сначала показывается размытая картинка, а затем постепенно увеличивается её качество.

<video autoplay loop muted playsinline width="1472" height="532" title="Load Facebook">
  <source src="/img/design-basic/load-facebook.mp4" type="video/mp4">
</video>

*Хорошо: placeholder при загрузке поста в Facebook*

**Вывод:** при загрузке сначала показывайте placeholder (образ) контента. В случае изображений подойдет JPEG с прогрессивной разверткой. Можно улучшить эффект, показав [маленькую размытую картинку](https://jmperezperez.com/medium-image-progressive-loading-placeholder/). А в первое мгновение – блок, закрашенный [ключевым цветом изображения](https://jmperezperez.com/medium-image-progressive-loading-placeholder/#Other-ways-of-improving-placeholders-Google-Images-Search). Для текста используйте placeholder, показывающий структуру сообщения, заменяя текст на серые полоски. Анимация поможет понять, что перед вами не окончательный контент. Для приложений не используйте экран загрузки для брендинга. Вместо него показывайте [элементы управления первого экрана](https://developer.apple.com/ios/human-interface-guidelines/icons-and-images/launch-screen/).

### Итого по отзывчивости:
- Отделяйте представление приложения от его логики. Визуальная часть приложения и его "работа" не должны быть связаны.
- Внезапное закрытие, отсутствие сети, нехватка ресурсов – это не крайний случай, а нормальная работа приложения.
- Если человек попросил что-то сделать, не нужно что-то спрашивать (Сохранить?) или уведомлять (OK?).
- Реакция в сетевых приложениях должна быть позитивной.
- Показывайте placeholder, пока контент не был получен. Сначала показывайте легкий контент "низкого" качества.
- Используйте предварительную загрузку содержимого. Будьте готовы, что человек нажмет на кнопки _Подробнее_, _Следующая фотография_, _Отправить_.


## 2. Надежность
> Нельзя безвозвратно удалять данные человека, даже если человек прямо попросил это сделать.

### При закрытии нужно сохранять документ всегда, независимо от действий человека

**Плохо: сохранение в TextEdit.** При закрытии документа в простых текстовых редакторах задается вопрос о сохранении. И если человек случайно нажмёт _Не сохранять_, то приложение спокойно удалит документ, который человек мог набирать весь день.

![Save TextEdit](/img/design-basic/save-textedit.png)

*Плохо: вопрос о сохранении в TextEdit*

**Хорошо: сохранение в Google Docs.** При закрытии Google Docs, документ сохраняется всегда. Никаких запросов нет.

![Save Google Docs](/img/design-basic/save-googledocs.png)

*Хорошо: «тихое» сохранение в Google Docs*

**Вывод:** сохраняйте данные, независимо от действий человека. Даже, если он явно сказал, что документ ему не нужен, в действительности он может ему понадобится через 5 минут.

### Сохранять нужно все данные, полученные от человека

**Плохо: Прокрутка в Word Online.** При открытии документа в облачном офисном пакете от Microsoft не сохраняется место прошлого просмотра.

![Scroll Word](/img/design-basic/scroll-word.png)

*Плохо: Положение прокрутке не сохраняется в Word Online*

**Хорошо: прокрутка в Word 2013.** При открытии документа в десктопной версии Word 2013, он предлагает продолжить работу с места, где вы остановились в прошлый раз. При чем заметьте как аккуратно сделано: при закрытии приложение не спрашивает "Сохранить место просмотра?", тихо сохраняет сам. При открытии так же тактично предлагает перейти к прошлому месту, не блокируя взаимодействие и не перекидывая автоматически. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/AM64bcBzdzg?autoplay=1&amp;loop=1&amp;mute=1&amp;rel=0&amp;controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>
*Хорошо: Положение прокрутке сохраняется в Word 2013*

**Вывод:** Сохраняйте не только основной документ, но и всю вспомогательную информацию, которая может помочь в будущем.

### Хранить нужно не только последнюю версию файла

**Плохо: автоматическое сохранение в Notes.app.** Заметки всё сохраняют без вопросов – это замечательно. Но что, если ты удалил важный фрагмент и закрыл приложение? Тогда его будет уже не вернуть. Теряется надежность заметок в глазах человека. Даже обычную физическую записку ты можешь восстановить, достав её из корзины, что не скажешь про её цифровую версию.

![Version Notes.app](/img/design-basic/version-notesapp.jpg)

*Плохо: отсутсвие версионности в Notes.app*

**Хорошо: version history в Google Docs.** Google Docs хранит все версии документа. В любой момент можно вернуться к любой из них. Никаких специальных действий для версионирования делать не нужно.

![Version Google Docs](/img/design-basic/version-googledocs.gif)

*Хорошо: version history в Google Docs*

**Вывод:** Хранить нужно не только последнюю версию файла, но и предыдущие. Предыдущие версии файла так же цены.


### Итого по надежности
- Данные человека бесценны.
- Данные человека нужно сохранять все и всегда.
- Данные человека – это не только написанное сообщение или созданный файл, но любые информационные действия со его стороны: ввод в текстовое поле, выбранные пункты и опции, выделения текста/изображения/файла/объектов, состояние приложения, позиция курсора и прокрутки страницы, просмотренные страницы, положение и размеры окна.
- Хранить нужно даже то, что человек явно удалил.
- Хранить нужно не только последнюю версию файла, но и предыдущие. Предыдущие версии файла так же ценны.
- Для хранения используйте контроль версий, резервное копирование, временные папки, корзину.


## 3. Скромность
> Нельзя отвлекать человека вещами, которые нужны компьютеру, но не важны для человека.
Компьютерные проблемы решает компьютер.

### Выбором места хранения файла должен заниматься компьютер

**Плохо: загрузка в Firefox.** Человек хочет скачать файл. Но ему предлагают сделать другие действия. В этот момент, как правило, браузер ждет реакции человека, хотя мог бы уже давно скачать файл.

![Firefox download](/img/design-basic/firefox-download.png)

*Плохо: ожидание ответа человека при загрузке в Firefox*

**Хорошо: загрузка в Chrome.** Браузер сразу же загружает файлы, нет никаких запросов. Для этого он использует временную папку Downloads. Если нужно посмотреть файл, то просто кликаешь на него на панели загрузок. Он откроется сразу же или автоматически после скачки. Нет никаких задержек загрузки из-за ожидания человека.

![Chrome download](/img/design-basic/chrome-download.png)

*Хорошо: автоматическая загрузка в Chrome*

**Вывод:** не спрашивайте и не ждите действия человека, когда он попросил что-то сделать. Делайте предварительную загрузку. Для временного хранения файлов используйте специальную папку. Если человек нажал "Скачать" случайно, дайте быстро отменить загрузку или удалить файл, если он уже скачался.

### Созданием резервной копией должен занимать компьютер даже без первичной настройки человеком

**Плохо: File History из Windows.** Предварительно нужно самим включить и настроить создание резервных копий. Создание резервных копий – это не цель человека (если только он не занимается таким бизнесом). Если человека всё таки убедили сделать бекап, то ему нужно сделать нетривиальные технические настройки. Доступное место ограничено (маленькие SSD) и не получится бекапить "всё". Нужно предугадать что бекапить, как часто и на какой срок. И это не так просто. Например, внутри папки с "легкими" документами могут быть "тяжелые" файлы, которые сразу забьют всё место. Или тебе важны частые бекапы тяжёлых [бинарных](https://ru.wikipedia.org/wiki/%D0%94%D0%B2%D0%BE%D0%B8%D1%87%D0%BD%D1%8B%D0%B9_%D1%84%D0%B0%D0%B9%D0%BB) (а-ля PSD) файлов, из которых нельзя сделать "легкие" инкрементальные изменения.

![Windows history](/img/design-basic/windows-history.jpg)

*Плохо: необходимость предварительной настройки File History из Windows*

**Хорошо. Version history из Dropbox.** При использовании Dropbox человек совершенно не заботится о резервных копиях. Он даже может не знать, что такое "бекапы", и что они у него создаются. Часто слышу, что кого-то [в очередной раз спас Dropbox](https://twitter.com/search?q=dropbox%20%D1%81%D0%BF%D0%B0%D1%81). Хорошо с версионированием справляются так же офисные пакеты Google Docs и Office Online, облачные хранилища Google Drive и OneDrive, множество других небольших веб-сервисов.

![Dropbox history](/img/design-basic/dropbox-history.gif)

*Хорошо. Автоматический version history из Dropbox.*

**Вывод:** в своих приложениях делайте бекапы сразу без предварительной настройки. Иметь версию файла, актуальную неделю назад, такое же базовое требование приложения, как устойчивость к сбоям. Сохраняйте инкрементальные изменения, экономьте место человека. Не используйте бинарные файлы для хранения данных, они сильно увеличивают объем бекапа. Помните, человек вспомнит о бекапе только тогда, когда будет уже поздно. Минимизируйте необходимость настройки со стороны человека. Плохой бекап лучше, чем никакой. Преимуществом в сфере бекапов имеют, конечно, облачные хранилища с их условно неограниченным хранилищем.

### Защитой и обслуживанием компьютера должен заниматься он сам

**Плохо: Kaspersky Internet Security.** Антивирус ставит себя в центр мира. Нужно постоянно обновлять базы. Панель управления выглядит как у космического корабля, много графиков. Показывает, что ты всегда в опасности. А пищание при нахождении вируса невозможно забыть. Некоторые люди, кстати, думают, что писк издают сами вирусы.

![Kaspersky antivirus](/img/design-basic/kaspersky-antivirus.png)

*Плохо: требования большого внимания от Kaspersky Internet Security*

**Хорошо: Windows Defender Antivirus.** Работает сразу и тихо. Его не замечаешь, он не кричит. Ты про него можешь и не знать. Если есть угроза безопасности, то он спокойно об этом говорит. Т. к. это проблема защищенности компьютера, а не человека.

![Windows antivirus](/img/design-basic/windows-antivirus.png)

*Хорошо: «тихая» работа от Windows Defender Antivirus*

**Вывод:** безопасностью компьютера должен заниматься компьютер. Если найден вредоносный файл, можно показать ненавязчивое уведомление (_хорошее решение_). Или понять, что компьютер под угрозой, обновить базу, проверить автоматически весь диск, и по результатам вывести отчет, что "Вы в безопасности" (_лучше_). Или тихо нейтрализовать вирусы, помещать неизлечимые файлы в безопасное хранилище (карантин), и только тогда, когда человек пытается их открыть, говорить, что файлы небезопасны, и предлагать открыть предыдущую безопасную версию файла (_великолепное решение_).

### Организацией закладок должен заниматься компьютер

**Плохо: Закладки в Chrome.** При добавлении закладки появляется окно (в загрузках файлов избавились от окна, а тут не смогли). Предлагают ввести имя, хотя оно уже и так есть. Предлагают выбрать папку хранения из сотни, что у меня доступны. Цель закладок — быстро сохранить текущее местонахождение, а не заполнение метаинформации.

![Bookmark Chrome](/img/design-basic/bookmark-chrome.png)

*Плохо: вопросы при добавлении закладки в Chrome*

**Хорошо: _нет примера_.** Ближе всего к идеалу создания закладок _Add to Reading List_ в Safari, хотя цель у этой функции совсем другая. Стандартными закладками на iPad непригодны: не удобно сохранять и все равно в итоге ничего не найдешь. На десктопе в Chrome сохраняю закладки перетаскиванием иконки на папку или в начало списка закладок (рядом с кнопкой "Назад" в браузере). Так же можно поставить [расширение](https://chrome.google.com/webstore/detail/sprucemarks/fakeocdnmmmnokabaiflppclocckihoj), чтобы при нажатии на _Звездочку_ окно сразу закрывалось, а закладка улетала в начала списка.

![Bookmark Chrome Good](/img/design-basic/bookmark-chromegood.png)

*Хорошо: _нет примера_. Ближе всего: сохранение закладки перетаскиванием в Chrome*

**Вывод:** Сохранение закладок должно быть мгновенным в 1-клик без запросов. Всё, что требует больше одного клика, уже не может называться закладкой. Категоризация и установка тегов должна быть автоматическая по содержимому страницы. Кроме того, нужно сохранять вспомогательную информацию, которая поможет при последующем поиске: как попал на страницу, что до этого искал, как человек себя вёл на странице, какие страницы так же смотрел. Сейчас поиск по истории у браузеров примерно никакой, проще найти в интернете заново.

### Итого по скромности:
- Вопросы и уведомления должны касаться только целей человека.
- Не путайте цели человека и цели компьютера. Это сложно, но важно.
- Считайте, что на вопросы, не касающиеся целей человека, зачастую будут даны вредные и опасные ответы. А в большинстве случаев уведомления будут совсем проигнорированы.
- Оценивая качество и удовлетворенность вашего приложения считайте, что все вопросы, необходимые компьютеру, будут проигнорированы или отвечены некорректно. Если приложение спросило: "Куда сохранять бекапы?", значит приложение не имеет функции хранения резервных файлов. И на странице _Features_ сайта вашего приложения можно смело вычеркнуть этот пункт.

## Общий итог
При создании приложений пользуйтесь базовыми принципами проектирования для создания естественного взаимодействия и удовлетворенности от использования. Отзывчивость создаст удобное использование. Благодаря надежности человек получит безопасную систему. В следствии скромности компьютера человек будет полностью погружен в решении своих задач.

