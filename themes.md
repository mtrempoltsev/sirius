### Обзор андроид gui

Для разработки пользовательского интерфейса используются следующие классы:
- Activity - активность, служит контекстом окружения для окон
- View - базовый класс окна. В андроиде есть ряд готовых виджетов как кнопки
- ViewGroup - расширение View для управления размерами и положением дочерних элементов, базовый класс для группировщиков и виджетов типа ListView
- Drawable - абстрактное представление изображения

Опредилить форму активности можно явно в коде или через xml ресурcы в папке res/layout

#### Группировщики
Визуальные контейнеры для других элеметов интерфейса

- LinearLayout - выстраивает в ряд дочерние элементы по вертикали или горизонтали
- RelativeLayout - позволяет задавать позицию относительно соседних элементов или самого себя
- ScrollView - позволяет прокручивать содержимое дочернего элемента

#### Диалоги

- Dialog - базовый класс для диалогов
- AlertDialog - простой диалог отображающий сообщение и 1/2/3 кнопки
- DatePickerDialog - диалог выбора даты
- TimePickerDialog - диалог выбора времени
- ProgressDialog - диалог отображающий индикатор хода процесса

#### События

Для обработки событий в виджете можно перегрузить нужный метод onXxx(), например onClick(). Либо создать переменную анонимного класса, реализующий интерфейс OnxxxListener. А затем зарегистрировать его в виджете методом setOnxxxListener(). 

Некоторые из интерфейсов:

- OnClickListener - событие клика на виджете
- OnFocusChangeListener - смена фокуса
- OnKeyListener - события клавиатуры
- OnLongClickListener - событие клика с длинным удержанием
- OnTouchListener - событие касания на сенсорном экране
- OnCreateContextMenuListener - создание контекстного меню

#### Кнопки

- Button - кнопка
- CompoundButton - базовый класс для кнопок с двумя состояниями:
  - CheckBox - кнопка флажок
  - RadioButton - несколько таких кнопок объединяются в группу, и только одна из них может быть отмечена
- ToggleButton - кнопка переключатель
- ImageButton - кнопка на основе изображения
- ZoomButton - всплывающая кнопка

#### Текст

- TextView - поле отображения статического текста
- EditText - поле ввода текста

#### Время

- DatePicker - выбор даты
- TimePicker - выбор времени
- AnalogClock - аналоговые часы
- DigitalClock - цифровые часы
- Chronometer - текстовый хронометр

#### Списки и таблицы
- ListView - одноуровневый список с вертикальной прокруткой
- ExpandableListView - двух уровневый список с вертикальной прокруткой
- Gallery - список элементов с горизонтальной прокруткой
- GridView - сетка, функционально похожа на список

#### Прочие виджеты

- ImageView - отображает указанную картинку, например иконку
- MediaController - медиаконтролер со стандартными кнопками типа play
- ProgressBar - индикатор прогресса какого-либо процесса
- RatingBar - отображение рейтинга в виде звезд

#### Пример виджета

```
<Button android:id="@id/btReg" 
        android:background="@drawable/btleft"
        android:text="@string/ui_ready" 
        android:layout_height="fill_parent"
        android:layout_width="fill_parent" 
        android:textSize="13dip"
        android:textStyle="bold" 
        android:layout_weight="1"
        android:layout_margin="5dip" />
```

```
public class App extends Activity {
     protected void onCreate(Bundle icicle) {
         super.onCreate(icicle);
         setContentView(R.layout.main_form);
         Button button = (Button) findViewById(R.id.button_id);
         button.setOnClickListener(new View.OnClickListener() {
             public void onClick(View v) {
                 // что-то делаем
             }
         });
     }
}
```

### Ресурсы приложения

Ресурсы находятся в директории res проекта. Для различных типов ресурсов в ней создаются отдельные поддиректории. Имена файлов ресурсов должны состоять из маленьких английских букв и цифр.

Для доступа к ресурсам в коде используется класс R, в котором определены целочисленные идентификаторы ресурсов. R генерируется автоматически и сохраняется в папке gen проекта.

#### Типы ресурсов

- АНИМАЦИЯ - папка animation, id ресурса в коде R.animation.xxx, где xxx имя xml файла с описанием анимации
- ИЗОБРАЖЕНИЯ - папка drawable, id ресурса в коде R.drawable.xxx, где где xxx имя xml файла с описанием изображения или имя графического файла (png, jpg, gif)
- ФОРМА - папка layout, id ресурса в коде R.drawable.xxx, где xxx имя xml файла с описанием расположения элементов пользовательского интерфейса
- МЕНЮ - папка menu, id ресурса в коде R.menu.xxx, где xxx имя xml файла с описанием меню
- ЗНАЧЕНИЯ - папка values, id ресурса в коде R.typeres.xxx, где xxx имя ресурса, а typeres тип ресурса определяемый в большинстве случаев названием тега:
  - color - цвет
  - dimen - размер
  - string - строка
  - bool - булево значение
  - integer - целое значение
  - id - идентификатор элемента графического интерфейса
  - array - массивы (строк, целых или прочих ресурсов)

#### Загрузка ресурсов

```
Resources res = getResources();
boolean screenIsSmall = res.getBoolean(R.bool.screen_small);
```

#### Ссылка на ресурс в xml ресурсах

При определении xml ресурса, например формы, можно использовать ссылки на другие ресурсы по формуле @[package:]typeres/filename.

```
<ImageView
    android:layout_height="fill_parent"
    android:layout_width="fill_parent"
    android:src="@drawable/logo"
    android:adjustViewBounds="@bool/adjust_view_bounds" />
```

#### Значения

Ресурсы определяющие простые значения определяются в директории values в xml файле с корневым элементом resource, который не имеет каких-либо атрибутов. Имя файла любое, но обычно строки записывают в strings.xml, целые в integers.xml и т.п.

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <bool name="screen_small">true</bool>

    <!-- #RGB, #ARGB, #RRGGBB, #AARRGGBB -->
    <color name="opaque_red">#f00</color>

    <integer name="min_speed">5</integer>
</resources> 
```

#### Массивы

```
<integer-array name="bits">
    <item>4</item>
    <item>8</item>
    <item>16</item>
    <item>32</item>
</integer-array>

<string-array name="planets">
    <item>Mercury</item>
    <item>Venus</item>
    <item>Earth</item>
    <item>Mars</item>
</string-array>
```

```
Resources res = getResources();
String[] planets = res.getStringArray(R.array.planets);
```

#### Альтернативные ресурсы

Android позволяется указывать альтернативные ресурсы для различных конфигураций устройств. Делается это добавлением суффикса к имени директории ресурса через - . Когда указывается несколько суффиксов, то они следуют в порядке указанном ниже. Другими словами нельзя указать вначале размер экрана, а потом язык. Правильно будет указать язык, а потом размер экрана.

- язык кодировка, например, en, fr, en-rUS, fr-rFR, fr-rCA, где r во второй части определяет регион, регистр символов неважен. Это параметр может измениться во время работы программы, если пользователь изменит язык в настройках, это можно обработать
- размер экрана:
  - small - маленький экран основанный на QVGA малой плотность. Например, QVGA малой плотностью, и VGA с большой плотностью
  - normal - экраны основанный на HVGA средней плотности. Например, WQVGA малой плотности, HVGA средней плотности, WVGA высокой плотности, QVGA малой плотности
  - large - экран основанный на VGA средней плонтности. Такие экраны имею больше размер по ширине и высоте чем HVGA экран. Например, VGA и WVGA средней плотности
  - xlarge - любой экран больший HVGA средней плонтности, в основном это планшетные устройства (tablet-style)
- соотношение экрана не зависимо от ориентации, может принимать значения:
  - long - длинные экраны (WQVGA, WVGA, FWVGA)
  - notlong - не длинные экраны (QVGA, HVGA, VGA)
- ориентация экрана:
  - port - портретная (вертикальная)
  - land - альбомная (горизонтальная)
- ночной режим, именение этого параметра можно обработать
  - night - ночь
  - notnight - день
- плотность экрана
  - ldpi - малая плотность, около 120dpi
  - mdpi - средняя плотность, около 160dpi
  - hdpi - повышенная плонтность, около 240dpi
  - xhdpi - сверх повышенная плотность, около 320dpi
  - nodpi - используется для изображений, которые не должны масштабироваться в зависимости от плотности экрана
- версия api андроида, например v3, v4, v7

Примеры:

```
drawable-en-notouch-12key/
drawable-port-ldpi/
```

### Идентификатор элемента интерфейса

Идентификаторы элемента интерфейса в основном используются для получения объекта интерфейса описанного в xml форме и для относительного позиционирования в группировщике RelativeLayout. Если идентификатор не используется, его можно не задавать.

Внутри одной формы не должно быть элементов с одинаковым идентификатором, но один и тот же идентификатор может быть в разных формах.

Идентификаторы лучше вынести в отдельный ресурсный файл проекта, например res/values/id.xml, иначе могут возникнуть сбои при включении одной формы в другую.

```
<LinearLayout>
    <EditText style="@style/fw" android:id="@id/etText" />
</LinearLayout>
```

##### id.xml

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <item type="id" name="etText" />
</resources>
```

#### Изображения

Изображения могут быть представлены графическими файлами .png, .jpg или .gif в папке res/drawable/.

При сборке приложения графические файлы оптимизируются. Например, если true-color png файлу в реальности не нужно больше 256 цветов, то он будет преобразован 8-битный png файл с цветовой палитрой. За счет этого экономится память. Это не касается изображений помещенных в папку res/raw/.

```
Resources res = getResources();
Drawable drawable = res.getDrawable(R.drawable.myimage);
BitmapDrawable drawable =
    (BitmapDrawable) res.getDrawable(R.drawable.myimage);
```

### Создание формы

Формы рекомендуется описывать в виде xml ресурса в папке res/layout, т.е. отдельно от кода:

- появляется возможность задать альтернативные ресурсы под различные конфигурации и параметры устройства
- набор значений атрибутов можно объединить в стили и темы

В большинстве случаев в качестве корневого элемента выступает один из группировщиков, внутри которого определяются элементы интерфейса - виджеты. В корневом элементе указывается пространство имен андроида для доступа к атрибутам виджетов. Обязательными атрибутами любого элемента является ширина и высота.

```
<LinearLayout
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent">
    <ListView 
        android:layout_width="fill_parent"
        android:layout_height="fill_parent" 
        android:id="@id/lvList" 
        android:background="@color/cWhite"
        />
</LinearLayout>
```

### Размер, позиция, выравнивание

Каждому элементу формы необходимо указать его размеры - ширину и высоту:
- layout_height - задает высоту элемента, может принимать следующие значения:
  - "wrap_content" - чтобы уместилось содержимое
  - "fill_parent" - растянуть в высоту родительского элемента
  - x - высота элемент в каких-либо единицах, например 15dp или ссылка на размер
- layout_width - задает ширину элемента, значения аналогичны предыдущему
- minWidth - минимальная широта
- maxWidth - максимальная широта
- minHeight - минимальная высота
- maxHeight - максимальная высота
- layout_gravity - указывает как выравнить элемент внутри группы, приведенные ниже значения можно комбинировать операцией |
  - bottom - поместить объект вниз, не меняя размера
  - center - по центру
  - center_horizontal - по центру горизонтали
  - center_vertical - по центру вертикали
  - fill - заполнить родительское окно (размеры объекта меняются)
  - fill_horizontal - заполнить по горизонтали
  - fill_vertical - заполнить по вертикали
  - left - влево
  - no_gravity - нет выравнивания
  - right - вправо
  - top - вверх

#### Выравнивание контента

Общее выравнивание дочерних элементов, или содержимого виджета, например, текст в кнопке, делается через атрибут gravity. Значения атрибута аналогичны layout_gravity.

```
<Button 
   android:id="@id/btAccount" 
   android:layout_width="wrap_content"
   android:layout_height="wrap_content" 
   android:background="@drawable/account" 
   android:text="Аккаунт" 
   android:textStyle="bold" 
   android:gravity="center_horizontal|bottom"            
/> 
```

#### Отступы

Внутренние отступы - отступы между содержимым элемента (текст, изображение) и его границей:
- padding - для всех четырех отступов, этот атрибут главнее следующих. Например, если задать стиль с этим атрибутом элементу, а в описании элемента указать paddingLeft, то значение paddingLeft будет игнорироваться
- paddingBottom - отступ снизу
- paddingLeft - отступ слева
- paddingRight - отступ справа
- paddingTop - отступ сверху

Внешние отступы задают расстояние между границей элемента и его окружающих элементов, включая границы родительского элемента:
- layout_margin - для всех четырех отступов
- layout_marginLeft - отступ слева
- layout_marginTop - отступ сверху
- layout_marginRight - отступ справа
- layout_marginBottom - отступ снизу

#### Настройка текста

Стандартные виджеты с текстом как кнопка являются расширением класса TextView. Наиболее часто используемые свойства:
- text - строка или ссылка на строку текста
- textColor - цвет или ссылка на цвет текста
- textSize - размер или ссылка на размер текста
- textStyle - стиль текста, может принимать следующие значения:
  - normal - обычный текст
  - bold - жирный текст
  - italic - курсив (наклонный текст)
- typeface - определяет начертание (шрифт текста), может принимать одно из следующих значений:
  - normal
  - sans
  - serif
  - monospace

#### Задний фон

Задний фон можно задать цветом, ссылкой на цвет или ссылкой на изображение

```
android:background="#ff0000"
android:background="#80ff0000"

<!-- ссылка на встроенный цвет -->
android:background="@android:color/transparent"

<!-- ссылка на изображение определенное в папке res/drawable-xxx -->
android:background="@drawable/button_more_comment_states"
```

### Темы и стили на Android

Стиль представляет собой набор свойств, которые определяют внешний вид и способы отображение виджета на устройствах с разными размерами экрана. С помощью стилей можно задавать такие свойства, как высота, отступы, цвет и размер шрифта, а также цвет фона и многое другое. В Android стили работают аналогично CSS (каскадные таблицы стилей), которые используются в веб-разработке.

Стили определяются xml файле в директории res/values/. При определении свойства в элементе item префикс пространства имен android: обязателен.

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="CodeFont" parent="@android:style/TextAppearance.Medium">
        <item name="android:layout_width">fill_parent</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:textColor">#00FF00</item>
        <item name="android:typeface">monospace</item>
    </style>
</resources>
```

Далее стиль назначается элементу управления:

```
<TextView
    style="@style/CodeFont"
    android:text="@string/hello" />
```

Так это выглядит без использования стиля:

```
<TextView
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:textColor="#00FF00"
    android:typeface="monospace"
    android:text="@string/hello" />
```

#### Родительский стиль

При создании стиля на основе стандартного стиля используется атрибут parent:

```
<style name="fw">
     <item name="android:layout_width">fill_parent</item>
     <item name="android:layout_height">wrap_content</item>
</style>

<style name="ListItem" parent ="@style/fw">
     <item name="android:minHeight">20dp</item>
     <item name="android:paddingLeft">@dimen/marginx2</item>
     <item name="android:paddingRight">@dimen/marginx2</item>
     <item name="android:paddingTop">@dimen/margin</item>
     <item name="android:paddingBottom">@dimen/margin</item>
     <item name="android:background">@drawable/bg_list_item</item>
</style>
```

### Темы

Тема - набор стилей. Синтаксис определения аналогичен определению стиля. В качестве родительской темы может выступать тема определенная в классе android.R.style. Стандартные темы и стили доступные для переопределения находятся в классе R.styleable.

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
  <style name="MyTheme" parent="android:Theme.Light">
     <item name="android:windowNoTitle">true</item>
     <item name="android:windowBackground">@color/translucent_blue</item>
  </style>
</resources>
```

В манифесте (AndroidManifest.xml) тема назначается либо всему приложению, либо отдельным активностям.

```
<!-- тема для всего приложения -->
<application android:theme="@style/MyTheme">

<!-- тема для активности -->
<activity ... android:theme="@android:style/Theme.Translucent">
```

### Настройки приложения

- создать файл preferences.xml в директории res/xml
- работать с настройками из кода

Элементы настроек имеют следующие атрибуты:
- android:key — имя настройки, по поторому в дальнейшем можно получить ее значение
- android:title — заголовок элемента настройки
- android:summary — краткое описание элемента настройки
- android:defaultValue — значение по умолчанию

Доступные типы элементов настроек:
- CheckBoxPreference — простой чекбокс, который возвращает значения true или false
- ListPreference — группа переключателей (radioGroup), из которых может быть выбран только один элемент. Атрибут android:entries указывает на массив со значениями в res/values/arrays.xml, а android:entryValues на массив с подписями
- EditTextPreference — показывает диалоговое окно с полем ввода. Возвращает строку в качестве значения
- Preference — настройка, работающая как кнопка
- PreferenceScreen — экран с настройками. Когда один PreferenceScreen вложен в другой, то открывается новый экран с настройками
- PreferenceCategory — категория настроек

##### preferences.xml

```
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
  <PreferenceCategory
      android:title="First Category">
      <CheckBoxPreference
          android:title="Checkbox Preference"
          android:defaultValue="false"
          android:summary="This preference can be true or false"
          android:key="checkboxPref" />
      <ListPreference
          android:title="List Preference"
          android:summary="Select an item in a array"
          android:key="listPref"
          android:defaultValue="digiGreen"
          android:entries="@array/listArray"
          android:entryValues="@array/listValues" />
  </PreferenceCategory>
  <PreferenceCategory
      android:title="Second Category">
  <EditTextPreference
      android:name="EditText Preference"
      android:summary="This allows you to enter a string"
      android:defaultValue="Nothing"
      android:title="Edit This Text"
      android:key="editTextPref" />
  <PreferenceScreen
    android:key="SecondPrefScreen"
    android:title="Second PreferenceScreen"
    android:summary="This is a second PreferenceScreen">
    <EditTextPreference
        android:name="An other EditText Preference"
        android:summary="PreferenceScreen"
        android:title="Edit text"
        android:key="SecondEditTextPref" />
  </PreferenceScreen>
  <Preference
    android:title="Custom Preference"
    android:summary="This works almost like a button"
    android:key="customPref" />
  </PreferenceCategory>
</PreferenceScreen>
```

##### arrays.xml

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
<string-array name="listArray">
   <item>Number 1</item>
   <item>Number 2</item>
   <item>Number 3</item>
   <item>Number 4</item>
</string-array>
 
<string-array name="listValues">
   <item>1</item>
   <item>2</item>
   <item>3</item>
   <item>4</item>
</string-array>
</resources>
```

Для того, чтобы показать пользователю экран с настройками, небходимо создать активити, унаследованное от PreferenceActivity:

```
public class Preferences extends PreferenceActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.preferences);

        Preference customPref = 
            (Preference) findPreference("customPref");

        customPref.setOnPreferenceClickListener(
            new OnPreferenceClickListener() {
                public boolean onPreferenceClick(Preference preference) {
                    SharedPreferences customSharedPreference 
                        = getSharedPreferences(
                            "myCustomSharedPrefs", Activity.MODE_PRIVATE);
                    SharedPreferences.Editor editor = 
                        customSharedPreference.edit();
                    editor.commit();
                    return true;
                }
            });
    }
}
```

Вызов активити с настройками:

```
Intent settingsActivity = 
  new Intent(getBaseContext(), Preferences.class);
startActivity(settingsActivity);
```

Получение установленных значений:

```
boolean CheckboxPreference;
String editTextPreference;
String ringtonePreference;
String secondEditTextPreference;
String customPref;

private void getPrefs() {
    SharedPreferences prefs = 
        PreferenceManager.getDefaultSharedPreferences(getBaseContext());
    CheckboxPreference = prefs.getBoolean("checkboxPref", true);
    editTextPreference = prefs.getString(
        "editTextPref", "Nothing has been entered");
    ringtonePreference = prefs.getString(
        "ringtonePref", "DEFAULT_RINGTONE_URI");
    secondEditTextPreference = prefs.getString(
        "SecondEditTextPref", "Nothing has been entered");

SharedPreferences mySharedPreferences = getSharedPreferences(
        "myCustomSharedPrefs", Activity.MODE_PRIVATE);
    customPref = mySharedPreferences.getString("myCusomPref", "");
}
```

Добавление в манифест настроек:

```
<activity
    android:name=".Preferences"
    android:label="@string/set_preferences">
</activity>
```