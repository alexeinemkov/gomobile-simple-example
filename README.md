# gomobile-simple-example 
Пример создания библиотеки для android


Структура проекта:

```
gomobile-simple-example/
--app/
------libs/
--libmobile/
----src/
------go/
--------go_say_hi(здесь имя библиотеки)/
----------go_say_hi.go
```


Создаём модуль:

```bash
go mod init libmobile/src/go/go_say_hi
```

В корневой директории должен появиться файл *go.mod*

Проверить чтобы в **PATH** был путь до *jdk* (Windows):

```
C:\Program Files\Android\Android Studio\jre\bin;
```

Проверить существование переменной **ANDROID_NDK_HOME**, в ней путь до NDK:

```
C:\Users\username\AppData\Local\Android\SDK\ndk\ndk-bundle\android-ndk-r23b
```

Или временно добавить (Windows PowerShell):

```
$Env:ANDROID_NDK_HOME="C:\Users\username\AppData\Local\Android\SDK\ndk\ndk-bundle\android-ndk-r23b"
```

Установка *gomobile*:

```bash
go get golang.org/x/mobile/cmd/gobind
go get golang.org/x/mobile/bind
go install golang.org/x/mobile/cmd/gomobile@latest
```

Инициализация *gomobile*, может занять какое-то время:

```
gomobile init
```

Генерируем файл **.aar** для импорта в Android Studio:

```
gomobile bind -v  -o app/libs/go_say_hi.aar -target=android ./libmobile/src/go/go_say_hi
```

В *app/libs/* должны появиться **jar** и **aar** файлы

Импорт в Android Studio:

```
File > New > New Module > Import .JAR or .AAR package
```

Библиотека появится в структуре проекта как новый модуль

Необходимо добавить зависимости в модуль *app*:

```
File > Project Structure > app -> Нажимаем на **+** или *Alt+Insert* -> Выбираем Module Dependency
```

Теперь можно пользоваться библиотекой:

```
import go_say_hi.Go_say_hi;
```