---
title: "Введение в Razor Pages в ASP.NET Core"
author: Rick-Anderson
description: "Этот документ содержит общие сведения об использовании страниц Razor в ASP.NET Core для упрощения разработки в сценариях, где применяются страницы."
keywords: "ASP.NET Core, страницы Razor"
ms.author: riande
manager: wpickett
ms.date: 09/12/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/razor-pages/index
ms.openlocfilehash: 3112faa38bb9702f6856097e315c413f0974010d
ms.sourcegitcommit: 3ba32b2b6425ed94604cb0f681db0d5bb5f8ad58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2017
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a>Введение в Razor Pages в ASP.NET Core

Авторы: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson) и [Райан Новак](https://github.com/rynowak) (Ryan Nowak)

Razor Pages — это новая функция платформы MVC ASP.NET Core, которая делает создание кодов сценариев для страниц проще и эффективнее.

Если вам требуется руководство на основе подхода "модель-представление-контроллер", см. статью [Начало работы с MVC ASP.NET Core](xref:tutorials/first-mvc-app/start-mvc).

<a name="prerequisites"></a>

## <a name="aspnet-core-20-prerequisites"></a>Предварительные требования ASP.NET 2.0

Установите [.NET Core](https://www.microsoft.com/net/core) 2.0.0 или более поздней версии.

Если вы используете Visual Studio, установите [Visual Studio](https://www.visualstudio.com/vs/) 2017 версии 15.3 или более поздней версии, а также следующие рабочие нагрузки:

* **ASP.NET и веб-разработка**
* **Кроссплатформенная разработка .NET Core**

<a name="rpvs17"></a>

## <a name="creating-a-razor-pages-project"></a>Создание проекта Razor Pages

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

Подробные инструкции по созданию проекта Razor Pages с помощью Visual Studio см. в статье [Начало работы с Razor Pages](xref:tutorials/razor-pages/razor-pages-start).

#   <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio для Mac](#tab/visual-studio-mac)

Из командной строки выполните команду `dotnet new razor`.

Откройте созданный файл *.csproj* в Visual Studio для Mac.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code.](#tab/visual-studio-code) 

Из командной строки выполните команду `dotnet new razor`.

#   <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli) 

Из командной строки выполните команду `dotnet new razor`.

---

## <a name="razor-pages"></a>Razor Pages

Функция Razor Pages активируется в файле *Startup.cs*:

[!code-cs[main](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

Рассмотрим простую страницу: <a name="OnGet"></a>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

Представленный выше код выглядит как файл представления Razor и отличается от него только директивой `@page`. Директива `@page` превращает файл в действие MVC, а значит обрабатывает запросы напрямую, минуя контроллер. Директива `@page` должна быть первой директивой Razor на странице. Директива `@page` влияет на поведение всех остальных конструкций Razor.

Похожая страница с использованием класса `PageModel` показана в следующих двух файлах. Файл *Pages/Index2.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

Файл кода "программной части" *Pages/Index2.cshtml.cs*:

[!code-cs[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

Как правило, файл класса `PageModel` называется так же, как файл Razor Pages, но с расширением *.cs*. Например, представленная выше страница Razor Pages называется *Pages/Index2.cshtml*. Файл, содержащий класс `PageModel`, называется *Pages/Index2.cshtml.cs*.

Сопоставления URL-адресов со страницами определяются расположением конкретной страницы в файловой системе. В приведенной ниже таблице показаны пути Razor Pages и соответствующие URL-адреса.

| Имя файла и путь               | Соответствующий URL |
| ----------------- | ------------ |
| */Pages/index.cshtml* | `/` или `/Index` |
| */Pages/Contact.cshtml* | `/Contact` |
| */Pages/Store/Contact.cshtml* | `/Store/Contact` |
| */Pages/Store/Index.cshtml* | `/Store` или `/Store/Index` |

Примечания.

* Среда выполнения по умолчанию ищет файлы Razor Pages в папке *Pages*.
* Если в URL-адресе не указана конкретная страница, по умолчанию открывается страница `Index`.

## <a name="writing-a-basic-form"></a>Создание простой формы

Функция Razor Pages предназначена для упрощения типовых шаблонов, которые используются в браузерах. [Привязки модели](xref:mvc/models/model-binding), [вспомогательные функции тегов](xref:mvc/views/tag-helpers/intro) и вспомогательные методы HTML *отлично работают* со свойствами, определенными в классе Razor Pages. Рассмотрим страницу с простой формой связи для модели `Contact`.

В представленных в этой статье примерах `DbContext` инициализируется в файле [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16).

[!code-cs[main](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

Модель данных:

[!code-cs[main](index/sample/RazorPagesContacts/Data/Customer.cs)]

Файл представления *Pages/Create.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

Файл кода программной части *Pages/Create.cshtml.cs* для представления:

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

Как правило, класс `PageModel` называется `<PageName>Model` и находится в том же пространстве имен, что и страница.

Применение файла кода программной части `PageModel` позволяет выполнять модульное тестирование, но требует написания явного конструктора и класса. Страницы без файлов кода программной части `PageModel` поддерживают компиляцию среды выполнения, что может пригодиться в процессе разработки.  <!-- review: advantage because you can make changes and refresh the browser without explicitly compiling the app -->

Страница содержит *метод обработчика* `OnPostAsync`, который выполняется по запросам `POST` (когда пользователь публикует форму). Методы обработчика можно добавить для любой HTTP-команды. Наиболее распространенные обработчики

* `OnGet` — инициализация необходимого для страницы состояния. Пример обработчика [OnGet](#OnGet).
* `OnPost` — обработка отправленных через форму данных.

Суффикс `Async` не является обязательным, но часто используется для асинхронных функций. Код `OnPostAsync` в приведенном выше примере похож на то, что обычно пишут в контроллере. Этот код типичен для Razor Pages. Большинство примитивов MVC, включая [привязку модели](xref:mvc/models/model-binding), [проверку](xref:mvc/models/validation) и результаты действий, являются общими.  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

Предыдущий метод `OnPostAsync`:

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

Простая схема `OnPostAsync`

Проверка на наличие ошибок проверки.

*  Если ошибок нет, сохранение данных и перенаправление.
*  Если есть ошибки, отображение страницы с сообщениями проверки. Проверка на стороне клиента выполняется точно так же, как в традиционных приложениях MVC ASP.NET Core. Во многих случаях ошибки проверки выявляются на клиентском компьютере и на сервер не отправляются.

После успешного ввода данных метод обработчика `OnPostAsync` вызывает метод обработчика `RedirectToPage`, чтобы получить экземпляр `RedirectToPageResult`. `RedirectToPage` — это новый результат действия, аналогичный `RedirectToAction` или `RedirectToRoute`, но настроенный для страниц. В приведенном выше примере он выполняет перенаправление на корневую страницу индекса (`/Index`). Более подробно `RedirectToPage` рассматривается в разделе [Создание URL для страниц](#url_gen).

Если в отправленной форме имеются ошибки проверки (переданные на сервер), метод обработчика `OnPostAsync` вызывает метод обработчика `Page`. `Page` возвращает экземпляр `PageResult`. Возвращение `Page` аналогично тому, как действия в контроллерах возвращают `View`. `PageResult` — значение типа возвращаемого значения <!-- Review  --> по умолчанию для метода обработчика. Метод обработчика, вернувший `void`, визуализирует страницу.

Для указания согласия на привязку модели в свойстве `Customer` используется атрибут `[BindProperty]`.

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

По умолчанию функция Razor Pages привязывает свойства ко всем командам, кроме GET. Привязка к свойствам позволяет сократить объем необходимого кода. Привязка уменьшает код за счет того, что для визуализации полей формы (`<input asp-for="Customer.Name" />`) и получения входных данных используется одно и то же свойство.

Домашняя страница (*Index.cshtml*):

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

Файл кода программной части *Index.cshtml.cs*:

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

Файл *Index.cshtml* содержит следующую разметку для создания ссылки на правку для каждого контактного лица.

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

[Вспомогательный тег привязки](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) использует атрибут [asp-route-{value}](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper#route) для создания ссылки на страницу редактирования. Эта ссылка содержит данные о маршруте с идентификатором контактного лица. Например, `http://localhost:5000/Edit/1`.

Файл *Pages/Edit.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

Первая строка содержит директиву `@page "{id:int}"`. Ограничение маршрутизации `"{id:int}"` указывает, что страница должна принимать обращенные к ней запросы, которые содержат данные о маршруте `int`. Если запрос к странице не содержит данные о маршруте, которые можно конвертировать в `int`, среда выполнения возвращает ошибку HTTP 404 (не найдено).

Файл *Pages/Edit.cshtml.cs*:

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

Файл *Index.cshtml* также содержит разметку для создания кнопки удаления у каждого контакта клиента:

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

Во время обработки кнопки удаления в HTML ее `formaction` включает параметры для следующего:

* Идентификатор контакта клиента, указанный атрибутом `asp-route-id`.
* Параметр `handler`, указанный атрибутом `asp-page-handler`.

Пример отображенной кнопки удаления с идентификатором контакта клиента `1`:

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

При выборе кнопки на сервер отправляется запрос формы `POST`. По соглашению имя метода обработчика выбирается на основе значения параметра `handler` в соответствии со схемой `OnPost[handler]Async`.

Так как `handler` — `delete` в этом примере, метод обработчика `OnPostDeleteAsync` используется для обработки запроса `POST`. Если `asp-page-handler` имеет другое значение, например `remove`, выбирается метод обработчика страницы с именем `OnPostRemoveAsync`.

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

Метод `OnPostDeleteAsync`:

* Принимает `id` из строки запроса.
* Отправляет в базу данных запрос контакта клиента с `FindAsync`.
* Если контакт клиента найден, он удаляется из списка контактов. База данных обновляется.
* Вызывает `RedirectToPage` для перенаправления на корневую страницу индекса (`/Index`).

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a>XSRF/CSRF и Razor Pages

Вам не придется писать отдельный код для [проверки подлинности запросов](xref:security/anti-request-forgery). Razor Pages включает создание и проверку маркеров защиты от подделок по умолчанию.

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a>Использование макетов, частичных реплик, шаблонов и вспомогательных функций тегов с Razor Pages

Pages работает со всеми функциями представлений Razor. Макеты, частичные реплики, шаблоны, вспомогательные функции тегов, а также файлы *_ViewStart.cshtml* и *_ViewImports.cshtml* работают точно так же, как и в стандартных представлениях Razor.

Давайте упростим нашу страницу с помощью некоторых из этих функций.

Добавим [макет страницы](xref:mvc/views/layout) в файл *Pages/_Layout.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

Этот [макет](xref:mvc/views/layout):

* управляет макетом каждой страницы (кроме страниц с отказом от макета);
* импортирует HTML-структуры, такие как JavaScript и таблицы стилей.

Дополнительные сведения см. в статье о [макете](xref:mvc/views/layout).

Свойство [Layout](xref:mvc/views/layout#specifying-a-layout) определяется в файле *Pages/_ViewStart.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

**Примечание.** Макет хранится в папке *Pages*. Pages ищет другие представления (макеты, шаблоны, частичные реплики) в иерархическом порядке, начиная с той папки, где находится текущая страница. Макет в папке *Pages* можно использовать на любой странице Razor, которая находится в папке *Pages*.

Корпорация Майкрософт рекомендует **не** размещать файл макета в папке *Views/Shared*. *Views/Shared* — это шаблон представлений MVC. Razor Pages опирается на иерархию папок, а не на условные обозначения путей.

Поиск представлений в Razor Pages охватывает папку *Pages*. Макеты, шаблоны и частичные реплики *работают* с контроллерами MVC и стандартными представлениями Razor.

Добавим файл *Pages/_ViewImports.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

`@namespace` описывается далее в этом руководстве. Директива `@addTagHelper` добавляет [встроенные вспомогательные теги](xref:mvc/views/tag-helpers/builtin-th/Index) на все страницы в папке *Pages*.

<a name="namespace"></a>

Явное применение директивы `@namespace` на странице:

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

Данная директива задает пространство имен для страницы. Включать пространство имен в директиву `@model` не требуется.

Если директива `@namespace` содержится в файле *_ViewImports.cshtml*, указанное пространство имен определяет префикс для созданного в Pages пространства имен, куда импортируется директива `@namespace`. Остальная часть созданного пространства имен (суффикс) представляет собой разделенный точками относительный путь между папкой с файлом *_ViewImports.cshtml* и папкой, содержащей страницу.

Например, файл кода программной части *Pages/Customers/Edit.cshtml.cs* задает пространство имен явно:

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

Файл *Pages/_ViewImports.cshtml* задает следующее пространство имен:

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

Сформированное пространство имен для файла *Pages/Customers/Edit.cshtml* Razor Pages совпадает с именем файла кода программной части. Директива `@namespace` разработана таким образом, чтобы добавляемые в проект классы C# и сгенерированный страницами код *просто работали* без добавления директивы `@using` для файла кода программной части.

**Примечание.** `@namespace` также работает со стандартными представлениями Razor.

Исходный файл представления *Pages/Create.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

Обновленный файл представления *Pages/Create.cshtml*:

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

[Начальный проект Razor Pages](#rpvs17) содержит файл *Pages/_ValidationScriptsPartial.cshtml*, который подключает проверку на стороне клиента.

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a>Формирование URL-адресов для страниц

На представленной выше странице `Create` используется `RedirectToPage`:

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

Это приложение имеет следующую структуру файлов и папок:

* */Pages*

  * *Index.cshtml*
  * */Customer*

    * *Create.cshtml*
    * *Edit.cshtml*
    * *Index.cshtml*

После успешного выполнения страницы *Pages/Customers/Create.cshtml* и *Pages/Customers/Edit.cshtml* перенаправляются на страницу *Pages/Index.cshtml*. Строка `/Index` составляет часть URL-адреса для доступа к указанной выше странице. Строка `/Index` позволяет создавать URL-адреса для страницы *Pages/Index.cshtml*. Пример:

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

Имя страницы — это путь к странице из корневой папки */Pages* (включая начальный символ `/`, например `/Index`). Приведенные выше примеры создания URL-адресов задействуют гораздо больше функций, чем просто прописывание URL в коде. Формирование URL-адресов включает [маршрутизацию](xref:mvc/controllers/routing) и позволяет генерировать и включать в код параметры в зависимости от того, как определяется маршрут в пути назначения.

Формирование URL-адресов для страниц поддерживает относительные имена. В приведенной ниже таблице показано, какая страница индекса выбирается с каждым параметром `RedirectToPage` в *Pages/Customers/Create.cshtml*.

| RedirectToPage(x)| Страница |
| ----------------- | ------------ |
| RedirectToPage("/Index") | *Pages/Index* |
| RedirectToPage("./Index"); | *Pages/Customers/Index* |
| RedirectToPage("../Index") | *Pages/Index* |
| RedirectToPage("Index")  | *Pages/Customers/Index* |

`RedirectToPage("Index")`, `RedirectToPage("./Index")` и `RedirectToPage("../Index")` — это *относительные имена*. Для получения имени целевой страницы параметр `RedirectToPage` *комбинируется* с путем текущей страницы.  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page. -- page name, not page path -->

Привязка относительных имен полезна при создании сайтов со сложной структурой. Если для связи между страницами в определенной папке используются относительные имена, эту папку можно переименовать. При этом все ссылки останутся рабочими (так как не включают имя папки).

## <a name="tempdata"></a>TempData

ASP.NET Core позволяет использовать свойство [TempData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller#Microsoft_AspNetCore_Mvc_Controller_TempData) в [контроллере](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller). Это свойство хранит данные до тех пор, пока они не будут прочитаны. Для проверки данных без удаления можно использовать методы `Keep` и `Peek`. `TempData` удобно использовать для перенаправления, когда данные требуются больше чем для одного запроса.

Атрибут `[TempData]` появился в ASP.NET 2.0 и поддерживается в контроллерах и на страницах.

В следующем коде значение `Message` задается с помощью `TempData`:

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

Представленная ниже разметка в файле *Pages/Customers/Index.cshtml* отображает значение `Message` с помощью `TempData`.

```cshtml
<h3>Msg: @Model.Message</h3>
```

Файл кода программной части *Pages/Customers/Index.cshtml.cs* применяет атрибут `[TempData]` к свойству `Message`.

```cs
[TempData]
public string Message { get; set; }
```

Дополнительные сведения см. в разделе [TempData](xref:fundamentals/app-state#temp).

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a>Несколько обработчиков на страницу

Следующая страница формирует разметку для двух обработчиков страницы с помощью вспомогательного тега `asp-page-handler`:

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there is no `asp-` attribute   -->

Форма в предыдущем примере включает две кнопки отправки, каждая из которых отправляет данные на отдельный URL-адрес с помощью `FormActionTagHelper`. Атрибут `asp-page-handler` является дополнением к `asp-page`. Атрибут `asp-page-handler` формирует URL-адреса, ,которые используются для отправки данных в каждый из методов обработчиков, определенных страницей. `asp-page` не задается, так как пример сопоставлен с текущей страницей.

Файл кода программной части:

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

В представленном выше коде используются *именованные методы обработчика*. Именованные методы обработчика создаются путем размещения определенного текста в имени после `On<HTTP Verb>` и перед `Async` (если есть). В приведенном выше примере использовались методы страницы OnPost**JoinList**Async и OnPost**JoinListUC**Async. Если убрать *OnPost* и *Async*, имена обработчиков будут выглядеть как `JoinList` и `JoinListUC`.

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

При использовании представленного выше кода URL-путь для отправки данных в `OnPostJoinListAsync` будет выглядеть как `http://localhost:5000/Customers/CreateFATH?handler=JoinList`. URL-путь для отправки данных в `OnPostJoinListUCAsync` будет иметь вид `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.

## <a name="customizing-routing"></a>Настройка маршрутизации

Если вы не хотите, чтобы в URL-адресе отображалась строка запроса `?handler=JoinList`, измените маршрут таким образом, чтобы в качестве пути в URL-адресе указывалось имя обработчика. Для настройки маршрута можно добавить после директивы `@page` шаблон маршрута, заключенные в двойные кавычки.

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

В представленном выше маршруте вместо строки запроса URL-путь содержит имя обработчика. Символ `?` после `handler` означает, что параметр маршрута является необязательным.

С помощью директивы `@page` можно добавить к маршруту страницы дополнительные сегменты и параметры. Все, что вы добавите, будет **присоединено** к маршруту страницы по умолчанию. Использовать для изменения маршрута страницы абсолютный или виртуальный путь (например, вида `"~/Some/Other/Path"`) нельзя.

## <a name="configuration-and-settings"></a>Конфигурация и параметры

Чтобы настроить дополнительные параметры, воспользуйтесь методом расширения `AddRazorPagesOptions` в построителе MVC:

[!code-cs[main](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

В настоящее время `RazorPagesOptions` позволяет задавать корневую папку для страниц и добавлять для них обозначения моделей приложений. В дальнейшем мы планируем расширить спектр его возможностей.

Сведения о предварительной компиляции представлений см. в статье [Компиляция представлений Razor](xref:mvc/views/view-compilation).

[Загрузить или просмотреть пример кода](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).

Представленные общие сведения являются вводными для статьи [Начало работы с Razor Pages в ASP.NET Core](xref:tutorials/razor-pages/razor-pages-start).
