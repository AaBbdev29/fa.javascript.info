# رشته‌ها

در جاوااسکریپت، داده‌ی متنی به عنوان رشته (string) ذخیره می‌شود. نوع جداگانه‌ای برای یک کاراکتر مفرد وجود ندارد.

فرمت درونی برای رشته‌ها همیشه [UTF-16](https://en.wikipedia.org/wiki/UTF-16) است، و به رمزگذاری صفحه بستگی ندارد.

## کوتیشن‌ها

بیایید انواع کوتیشن‌ها را یادآوری کنیم.

رشته‌ها می‌توانند در کوتیشن‌های تکی، دوتایی یا backtickها محصور شوند:

```js
let single = 'کوتیشن تکی';
let double = "کوتیشن دوتایی";

let backticks = `هاbacktick`;
```

کوتیشن‌های تکی و دوتایی اساسا یکسان هستند. اگرچه، backtickها، با پیچیدن هر عبارتی در `{...}$`، به ما اجازه می‌دهند که آن عبارت را درون رشته قرار دهیم:

```js run
function sum(a, b) {
  return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
```

یکی دیگر از مزایای استفاده از backtickها این است که اجازه می‌دهند تا رشته را در چند خط بنویسیم:

```js run
let guestList = `مهمان‌ها:
 * John
 * Pete
 * Mary
`;

alert(guestList); // لیستی از مهمان‌ها، در چند خط
```

طبیعی به نظر می‌رسد نه؟ اما کوتیشن‌های تکی یا دوتایی این چنین کار نمی‌کنند.

اگر ما با استفاده از آنها تلاش کنیم در چند خط بنویسیم، یک ارور به وجود خواهد آمد:

```js run
let guestList = "Guests: // Error: Unexpected token ILLEGAL
  * John";
```

کوتیشن‌های تکی و دوتایی از زمان بسیار قدیم در زبان وجود داشتند زمانی که نیاز به رشته‌های چند خطی خیلی به چشم نمی‌آمد. Backtickها بعدها به وجود آمدند و به این ترتیب چند کاره هستند.

Backtickها به ما اجازه می‌دهند که یک "تابع الگو" قبل از backtick اول مشخص کنیم. سینتکس اینگونه است: <code>func&#96;string&#96;</code>. تابع `func` به طور خودکار صدا زده می‌شود، رشته را دریافت می‌کند و عبارات را ایجاد می‌کند و می‌تواند با آنها فرایندی انجام دهد. به این "الگوهای برچسب گذاری شده" می‌گویند. این ویژگی پیاده‌سازی الگوهای سفارشی را آسان‌تر می‌کند، اما در عمل خیلی کم استفاده می‌شود. می‌توانید درباره آن در [کتاب راهنما](mdn:/JavaScript/Reference/Template_literals#Tagged_templates) بیشتر بخوانید.

## کاراکترهای خاص

اینکه با کوتیشن‌های تکی و دوتایی رشته‌های چند خطی بسازیم، با استفاده از "کاراکتر خط جدید"، که به صورت `\n` نوشته می‌شود، امکان پذیر است که یک خط جدید را مشخص می‌کند:

```js run
let guestList = "مهمان‌ها:\n * John\n * Pete\n * Mary";

<<<<<<< HEAD
alert(guestList); // لیستی چند خطی از مهمان‌ها
```

برای مثال، این دو خط برابر هستند، فقط به طور متفاوتی نوشته شده‌اند:
=======
alert(guestList); // a multiline list of guests, same as above
```

As a simpler example, these two lines are equal, just written differently:
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

```js run
let str1 = "Hello\nWorld"; // "ایجاد دو خط با استفاده از "نماد خط جدید

// هاbacktick ایجاد دو خط با استفاده از خط جدید و 
let str2 = `Hello
World`;

alert(str1 == str2); // true
```

<<<<<<< HEAD
کاراکترهای "خاص" دیگر و غیر متداول هم هستند.

لیست کامل آنها:
=======
There are other, less common "special" characters:
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

| کاراکتر | توضیحات |
|-----------|-------------|
<<<<<<< HEAD
|`\n`|خط جدید|
|`\r`|Carriage return: به تنهایی استفاده نمی‌شود. فایل‌های متنی ویندوز از ترکیب دو کاراکتر `\r\n` برای نمایش یک خط جدید استفاده می‌کند. 
`\n` به دلیل‌های تاریخی، بیشتر نرم‌افزارهای ویندوزی `\n` را هم می‌شناسند. |
|`\'`, `\"`|کوتیشن‌ها|
|`\\`|Backslash|
|`\t`|Tab|
|`\b`, `\f`, `\v`| Backspace, Form Feed, Vertical Tab -- برای سازگاری نگه داشته شده‌اند، امروزه استفاده نمی‌شوند. |
|`\xXX`|کاراکتر Unicode همراه با Unicode بر پایه 16 (hexadecimal) داده شده، برای مثال `'\x7a'` برابر است با `'z'`.|
|`\uXXXX`|یک نماد Unicode با کدی بر پایه 16 (hex) `XXXX` با کدگذاری UTF-16، برای مثال `\u009A` که یک Unicode برای نماد کپی‌رایت است `©`. باید دقیقا 4 رقم hex داشته باشد. |
|`\u{X…XXXXXX}` (1 تا 6 کاراکتر hex)|یک نماد Unicode با کدگذاری UTF-32 است. بعضی از کاراکترهای کمیاب با دو نماد Unicode کدگذاری می‌شوند و 4 بایت حجم می‌گیرند. به این روش می‌تونیم کدهای طولانی را جایگذاری کنیم. |

مثال‌هایی با Unicode:

```js run
alert( "\u00A9" ); // ©
alert( "\u{20331}" ); // 佫 ،(طولانی Unicode) یک حرف کمیاب چینی
alert( "\u{1F60D}" ); // 😍 ،(طولانی دیگر Unicode یک) یک نماد صورت خندان
```

تمام کاراکترهای خاص با یک کاراکتر backslash `\` شروع می‌شوند. همچنین به آن "کاراکتر فرار (escape)" هم می‌گویند.

اگر بخواهیم یک کوتیشن را درون رشته‌ای قرار دهیم ممکن است از آن استفاده کنیم.
=======
|`\n`|New line|
|`\r`|In Windows text files a combination of two characters `\r\n` represents a new break, while on non-Windows OS it's just `\n`. That's for historical reasons, most Windows software also understands `\n`. |
|`\'`,&nbsp;`\"`,&nbsp;<code>\\`</code>|Quotes|
|`\\`|Backslash|
|`\t`|Tab|
|`\b`, `\f`, `\v`| Backspace, Form Feed, Vertical Tab -- mentioned for completeness, coming from old times, not used nowadays (you can forget them right now). |

As you can see, all special characters start with a backslash character `\`. It is also called an "escape character".

Because it's so special, if we need to show an actual backslash `\` within the string, we need to double it:

```js run
alert( `The backslash: \\` ); // The backslash: \
```

So-called "escaped" quotes `\'`, `\"`, <code>\\`</code> are used to insert a quote into the same-quoted string.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

برای مثال:

```js run
alert( 'I*!*\'*/!*m the Walrus!' ); // *!*I'm*/!* the Walrus!
```

همانطور که می‌بینید، باید قبل از کوتیشن داخلی backslash `\` بیاریم، وگرنه در غیر این صورت کوتیشن پایان رشته را نمایش می‌دهد.

قطعا فقط کوتیشن‌هایی که با کوتیشن‌های پایانی یکسان هستند باید فراری شوند. پس، به عنوان یک راه حل زیباتر، به جای آن می‌توانیم به کوتیشن‌های دوتایی یا backtickها سوییچ کنیم:

```js run
alert( "I'm the Walrus!" ); // I'm the Walrus!
```

<<<<<<< HEAD
در نظر داشته باشید که backslash `\` برای خوانایی درست رشته توسط جاوااسکریپت به کار برده می‌شود، سپس محو می‌شود. رشته‌ای که درون حافظه است `\` ندارد. می‌توانید این موضوع را به صراحت در `alert` مثال بالایی ببینید.

اما اگر نیاز به نمایش یک backslash `\` واقعی در بین رشته داشته باشیم چه کار کنیم؟

این کار شدنی است و ما باید آن را دو برابر کنیم مثل `\\`:

```js run
alert( `The backslash: \\` ); // The backslash: \
```
=======
Besides these special characters, there's also a special notation for Unicode codes `\u…`, we'll cover it a bit later in this chapter.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

## طول رشته

ویژگی `length` دارای طول رشته است:

```js run
alert( `My\n`.length ); // 3
```

در نظر داشته باشید که `\n` یک کاراکتر "خاص" مفرد است، پس طول در واقع `3` است.

```warn header="`length` یک ویژگی است"
بعضی اوقات افرادی که زمینه‌ای در بعضی زبان‌های برنامه نویسی دیگر دارند اشتباها `str.length()` را به جای نوشتن `str.length` صدا می‌زنند. اینگونه کار نمی‌کند.

لطفا در نظر داشته باشید که `str.length` یک ویژگی عددی است نه یک تابع. نیازی به اضافه کردن پرانتر بعد از آن نیست.
```

## دسترسی داشتن به کاراکترها

برای دریافت یک کاراکتر در موقعیت `pos`، از براکت‌ها استفاده کنید یا متد [str.charAt(pos)](mdn:js/String/charAt) را صدا بزنید. اولین کاراکتر از موقعیت صفر شروع می‌شود:

```js run
let str = `Hello`;

// اولین کاراکتر
alert( str[0] ); // H
alert( str.charAt(0) ); // H

// آخرین کاراکتر
alert( str[str.length - 1] ); // o
```

براکت‌ها روش مدرن دریافت کاراکتر هستند، در حالی که `charAt` بنا به دلایلی مربوط به تاریخچه زبان وجود دارد.

تنها تفاوت میان آنها این است که اگر کاراکتری پیدا نشود، `[]` مقدار `undefined` را برمی‌گرداند، و `charAt` یک رشته خالی را برمی‌گرداند:

```js run
let str = `Hello`;

alert( str[1000] ); // undefined
alert( str.charAt(1000) ); // '' (یک رشته خالی)
```

همچنین ما می‌توانیم با استفاده از `for..of` برای کاراکترها حلقه بزنیم:

```js run
for (let char of "Hello") {
  alert(char); // H,e,l,l,o (و غیره "l" سپس ،"e" سپس ،"H" می‌شود char)
}
```

## رشته‌ها تغییرناپذیر هستند

رشته‌ها در جاوااسکریپت نمی‌توانند تغییر کنند. اینکه یک کاراکتر را تغییر دهیم غیر ممکن است.

بیایید برای نشان دادن اینکه این کار نخواهد کرد امتحانش کنیم:

```js run
let str = 'Hi';

str[0] = 'h'; // ارور می‌دهد
alert( str[0] ); // کار نمی‌کند
```

یک راه حل این است که رشته‌ای کاملا جدید بسازیم و `str` را به جای رشته‌ی قدیمی برابر با آن قرار دهیم.

برای مثال:

```js run
let str = 'Hi';

str = 'h' + str[1]; // رشته را جایگزین می‌کنیم

alert( str ); // hi
```

در بخش‌های بعدی مثال‌های بیشتری از این خواهیم دید.

## تغییر بزرگی و کوچکی حروف

متدهای [toLowerCase()](mdn:js/String/toLowerCase) و [toUpperCase()](mdn:js/String/toUpperCase) بزرگی و کوچکی حروف را تغییر می‌دهند:

```js run
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
```

یا اگر بخواهیم یک کاراکتر را به حرف کوچک آن تبدیل کنیم اینگونه عمل می‌کنیم:

```js run
alert( 'Interface'[0].toLowerCase() ); // 'i'
```

## جستجو برای یک زیر رشته

چند راه برای گشتن به دنبال یک زیر رشته در یک رشته وجود دارد.

### متد str.indexOf

متد اول [str.indexOf(substr, pos)](mdn:js/String/indexOf) است.

این متد به دنبال `substr` درون `str` می‌گردد، و از موقعیت `pos` داده شده شروع می‌کند، و موقعیتی که زیر رشته مورد نظر پیدا شد یا اگر چیزی پیدا نشد `-1` را برمی‌گرداند.

برای مثال:

```js run
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0 ،در شروع رشته پیدا شد 'Widget' چون
alert( str.indexOf('widget') ); // -1 ،چیزی پیدا نشد، جستجو به بزرگی یا کوچکی حروف حساس است

alert( str.indexOf("id") ); // 1 ،(است id دارای ..idget) در موقعیت 1 پیدا شد "id"
```

پارامتر اختیاری دوم به ما اجازه جستجو از موقعیت داده شده را می‌دهد.

برای مثال، اولین `"id"` که وجود دارد در موقعیت `1` است. برای پیدا کردن بعدی، بیایید جستجو را از موقعیت `2` شروع کنیم:

```js run
let str = 'Widget with id';

alert( str.indexOf('id', 2) ) // 12
```

اگر ما مشتاق این هستیم که تمام آنها را پیدا کنیم، می‌توانیم `indexOf` را دورن یک حلقه اجرا کنیم. تمام صدازدن‌های جدید با موقعیتی بعد از موقعیت زیر رشته‌ی پیدا شده قبلی انجام می‌شود:

```js run
let str = 'As sly as a fox, as strong as an ox';

let target = 'as'; // بیایید به دنبال آن بگردیم

let pos = 0;
while (true) {
  let foundPos = str.indexOf(target, pos);
  if (foundPos == -1) break;

  alert( `Found at ${foundPos}` );
  pos = foundPos + 1; // جستجو را از موقعیت بعدی ادامه بده
}
```

الگوریتم یکسان را می‌توان کوتاه‌تر نوشت:

```js run
let str = "As sly as a fox, as strong as an ox";
let target = "as";

*!*
let pos = -1;
while ((pos = str.indexOf(target, pos + 1)) != -1) {
  alert( pos );
}
*/!*
```

```smart header="`متد str.lastIndexOf(substr, position)`"
یک متد مشابه [str.lastIndexOf(substr, position)](mdn:js/String/lastIndexOf) هم وجود دارد که از انتهای رشته تا آغاز آن جستجو می‌کند.

این متد زیر رشته‌های پیدا شده را با ترتیب برعکس لیست می‌کند.
```

یک چیز ناخوشایند در رابطه با `indexOf` در `if` وجود دارد. ما نمی‌توانیم آن را اینگونه درون `if` بگذاریم:

```js run
let str = "Widget with id";

if (str.indexOf("Widget")) {
    alert("We found it"); // !کار نمی‌کند
}
```

در مثال بالا `alert` نمایش نمی‌دهد زیرا `str.indexOf("Widget")` مقدار `0` را برمی‌کرداند (به این معنی که زیر رشته مورد نظر را در موقعیت آغازین پیدا کرد). درست است، اما `if` مقدار `0` را با `false` برابر فرض می‌کند.

بنابراین، ما باید در واقع `-1` را بررسی کنیم، به این شکل:

```js run
let str = "Widget with id";

*!*
if (str.indexOf("Widget") != -1) {
*/!*
    alert("We found it"); // !حالا کار می‌کند
}
```

<<<<<<< HEAD
### ترفند bitwise NOT

یکی از ترفندهای قدیمی که اینجا استفاده می‌شود عملگر [bitwise NOT](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_NOT) `~` است. این عملگر عدد را به یک عدد صحیح 32 بیتی تبدیل می‌کند (و بخش اعشاری را در صورت وجود حذف می‌کند) و سپس تمام بیت‌ها را در نمایش دودویی خودش معکوس می‌کند.

در عمل، این به معنی یک چیز ساده است: برای اعداد صحیح 32 بیتی `~n` برابر است با `-(n+1)`.

برای مثال:

```js run
alert( ~2 ); // -3, the same as -(2+1)
alert( ~1 ); // -2, the same as -(1+1)
alert( ~0 ); // -1, the same as -(0+1)
*!*
alert( ~-1 ); // 0, the same as -(-1+1)
*/!*
```

همانطور که می‌بینیم، `~n` تنها فقط وقتی که `n == -1` باشد برابر با صفر است (برای هر عدد صحیح 32 بیتی تخصیص داده شده‌ی `n`).

بنابراین، آزمایش `if ( ~str.indexOf("...") )` فقط زمانی که نتیجه `indexOf` برابر با `-1` نباشد truthy است. به عبارتی دیگر، زمانی که یک زیر رشته پیدا شود.

افراد از آن برای کوتاه کردن بررسی `indexOf` استفاده می‌کنند:

```js run
let str = "Widget";

if (~str.indexOf("Widget")) {
  alert( 'Found it!' ); // کار می‌کند
}
```

اینکه از ویژگی‌های زبان با روشی که واضح نباشد استفاده کنیم معمولا پیشنهاد نمی‌شود، اما این ترفند مخصوص در کدهای قدیمی بسیار استفاده می‌شود، پس ما باید آن را متوجه شویم.

فقط به یاد داشته باشید: `if (~str.indexOf(...))` به صورت «اگر پیدا شد» خوانده می‌شود.

اگر بخواهیم دقیق باشیم، همانطور که اعداد بزرگ هم توسط عملگر `~` 32 بیتی می‌شوند، اعداد دیگری هم وجود دارند که نتیجه `0` را می‌دهند، کوچک‌ترین آنها `~4294967295=0` است. این روش چنین بررسی‌ای را فقط زمانی که رشته آنقدر طولانی نباشد به درستی انجام می‌دهد.

در حال حاضر ما این روش را فقط در کدهای قدیمی می‌بینیم، چون جاوااسکریپت مدرن متد `.includes` را فراهم کرده است (قسمت پایینی).

### متدهای includes، startsWith، endsWith
=======
### includes, startsWith, endsWith
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

متد مدرن‌تر [str.includes(substr, pos)](mdn:js/String/includes) با وابستگی به اینکه رشته `str` درون خودش دارای زیر رشته‌ی `substr` است یا نه مقدار `true/false` را برمی‌گرداند.

اگر نیاز داشته باشیم که وجود یک زیر رشته را بررسی کنیم، اما به موقعیت آن نیازی نداریم این متد انتخاب مناسبی است:

```js run
alert( "Widget with id".includes("Widget") ); // true

alert( "Hello".includes("Bye") ); // false
```

آرگومان دوم و اختیاری `str.includes` موقعیتی است که جستجو از آن شروع می‌شود:

```js run
alert( "Widget".includes("id") ); // true
alert( "Widget".includes("id", 3) ); // false وجود ندارد پس "id" از موقعیت 3 هیج
```

متدهای [str.startsWith](mdn:js/String/startsWith)(بررسی شروع شدن رشته با یک زیر رشته) و [str.endsWith](mdn:js/String/endsWith)(بررسی پایان یافتن رشته با یک زیر رشته) دقیقا کاری را که می‌گویند انجام می‌دهند:

```js run
alert( "*!*Wid*/!*get".startsWith("Wid") ); // true شروع می‌شود پس "Wid" با "Widget"
alert( "Wid*!*get*/!*".endsWith("get") ); // true پایان می‌یابد پس "get" با "Widget"
```

## گرفتن یک زیر رشته

در جاوااسکریپت 3 متد برای گرفتن یک زیر رشته وجود دارد: `substring`، `substr` و `slice`.

`str.slice(start [, end])`
: قسمتی از رشته را از موقعیت `start` تا `end` (شامل `end` نمی‌شود) را برمی‌گرداند.

    برای مثال:

    ```js run
    let str = "stringify";
    alert( str.slice(0, 5) ); // 'strin' :زیر رشته از 0 تا 5 (شامل 5 نمی‌شود)
    alert( str.slice(0, 1) ); // 's' :از 0 تا 1، اما شامل 1 نمی‌شود، پس فقط کاراکتری که در 0 است
    ```

    اگر هیچ آرگومان دومی در کار نباشد، سپس `slice` تا آخر رشته می‌رود:

    ```js run
    let str = "st*!*ringify*/!*";
    alert( str.slice(2) ); // 'ringify' :از موقعیت دوم تا آخر
    ```

    مقدارهای منفی برای `start/end` هم ممکن هستند. آنها به این معنی هستند که موقعیت از آخر رشته شمارش می‌شود:

    ```js run
    let str = "strin*!*gif*/!*y";

    // از موقعیت 4 از سمت راست شروع می‌شود، در موقعیت 1 از سمت راست پایان می‌یابد
    alert( str.slice(-4, -1) ); // 'gif'
    ```

`str.substring(start [, end])`
<<<<<<< HEAD
: قسمتی از رشته *بین* `start` و `end` را برمی‌گرداند.

    این متد تقریبا مشابه با `slice` است، اما این اجازه را می‌دهد که `start` بیشتر از `end` باشد.
=======
: Returns the part of the string *between* `start` and `end` (not including `end`).

    This is almost the same as `slice`, but it allows `start` to be greater than `end` (in this case it simply swaps `start` and `end` values).
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

    برای مثال:

    ```js run
    let str = "st*!*ring*/!*ify";

    // یکسان هستند substring این دو برای
    alert( str.substring(2, 6) ); // "ring"
    alert( str.substring(6, 2) ); // "ring"

    // ...اینطور نیست slice اما برای
    alert( str.slice(2, 6) ); // "ring" (یکسان است)
    alert( str.slice(6, 2) ); // "" (یک رشته خالی)

    ```

    آرگومان‌های منفی (برخلاف slice) پشتیبانی نمی‌شوند، با آنها مانند `0` رفتار می‎شود.

`str.substr(start [, length])`
: قسمتی از رشته از `start`، تا `length` (طول) داده شده را برمی‌گرداند.

    در تضاد با متدهای قبلی، این متد به ما اجازه می‌دهد که به جای موقعیت پایانی `length` (طول) را تعیین کنیم:

    ```js run
    let str = "st*!*ring*/!*ify";
    alert( str.substr(2, 4) ); // 'ring' :از موقعیت دوم 4 کاراکتر را بگیر
    ```

    اولین آرگومان می‌تواند برای شمارش از آخر، منفی باشد:
    

    ```js run
    let str = "strin*!*gi*/!*fy";
    alert( str.substr(-4, 2) ); // 'gi' :از موقعیت چهارم 2 کاراکتر را بگیر
    ```

بیایید این متدها را برای جلوگیری از هر گمراهی خلاصه کنیم:

| متد | انتخاب می‌کند... | منفی‌ها |
|--------|-----------|-----------|
<<<<<<< HEAD
| `slice(start, end)` | از `start` تا `end` (شامل `end` نمی‌شود) | منفی‌ها مجازند |
| `substring(start, end)` | بین `start` و `end` | مقدار منفی به معنای `0` است |
| `substr(start, length)` | از `start` به تعداد `length` کاراکتر می‌گیرد | `start` منفی مجاز است |
=======
| `slice(start, end)` | from `start` to `end` (not including `end`) | allows negatives |
| `substring(start, end)` | between `start` and `end` (not including `end`)| negative values mean `0` |
| `substr(start, length)` | from `start` get `length` characters | allows negative `start` |
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

```smart header="کدام را انتخاب کنیم؟"
تمام آنها می‌توانند کار را انجام دهند. به طور رسمی، `substr` یک اشکال جزئی دارد: این متد در هسته مشخصات جاوااسکریپت تعریف نشده است، اما در Annex B تعریف شده، که فقط ویژگی‌های مختص به مرورگر را پوشش می‌دهد که به دلایلی مربوط به تاریخچه زبان وجود دارد. پس محیط‌هایی که مرورگر نباشند ممکن است از آن پشتیبانی نکنند. اما در عمل این متد همه‌جا کار می‌کند.

<<<<<<< HEAD
از بین دو متد دیگر، `slice` مقداری قابل انعطاف‌تر است، و آرگومان‌های منفی را مجاز می‌داند و برای نوشتن کوتاه‌تر است. پس فقط به یاد داشتن `slice` از بین این سه متد کافی است.
=======
Of the other two variants, `slice` is a little bit more flexible, it allows negative arguments and shorter to write.

So, for practical use it's enough to remember only `slice`.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4
```

## مقایسه رشته‌ها

همانطور که از فصل <info:comparison> (مقایسه‌ها) می‌دانیم، رشته‌ها با ترتیب الفبایی کاراکتر به کاراکتر مقایسه می‌شوند.

گرچه، جزییاتی وجود دارد.

1. یک حرف کوچک انگلیسی همیشه از حرف بزرگ، بزرگتر است:

    ```js run
    alert( 'a' > 'Z' ); // true
    ```

2. حروفی که علامت دارند "بدون ترتیب" هستند:

    ```js run
    alert( 'Österreich' > 'Zealand' ); // true
    ```

    اگر ما اسم این کشورها را مرتب کنیم این موضوع ممکن است باعث ایجاد نتایج عجیب شود. معمولا مردم توقع داشند که `Zealand` بعد از `Österreich` در لیست بیاید.

برای فهمیدن اینکه چه چیزی رخ می‌دهد، بیایید نمایش داخلی رشته‌ها را در جاوااسکریپت مرور کنیم.

تمام رشته‌ها با استفاده از [UTF-16](https://en.wikipedia.org/wiki/UTF-16) کدگذاری شده‌اند. یعنی اینکه: هر کاراکتر یک کد عددی متناظر دارد. متدهای خاصی هستند که گرفتن کد از کاراکتر و برعکس را ممکن می‌سازند.

`str.codePointAt(pos)`
<<<<<<< HEAD
: کد کاراکتر را در موقعیت `pos` برمی‌گرداند:

    ```js run
    // حروف با بزرگی یا کوچکی متفاوت کدهای متفاوت دارند
    alert( "z".codePointAt(0) ); // 122
=======
: Returns a decimal number representing the code for the character at position `pos`:

    ```js run
    // different case letters have different codes
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4
    alert( "Z".codePointAt(0) ); // 90
    alert( "z".codePointAt(0) ); // 122
    alert( "z".codePointAt(0).toString(16) ); // 7a (if we need a more commonly used hex value of the code)
    ```

`String.fromCodePoint(code)`
: یک کاراکتر با استفاده از `کد` عددی آن می‌سازد:

    ```js run
    alert( String.fromCodePoint(90) ); // Z
    alert( String.fromCodePoint(0x5a) ); // Z (we can also use a hex value as an argument)
    ```

    همچنین ما می‌توانیم کاراکترهای Unicode را از طریق کد آنها با استفاده از `\u` که بعد از آن کد hex می‌آید اضافه کنیم:

    ```js run
    // 5a عدد 90 در سیستم عددی بر پایه 16 برابر است با
    alert( '\u005a' ); // Z
    ```

حال بیایید با ساختن یک رشته از کاراکترهایی که کد `65..220` دارند آنها را نگاه بیاندازیم (حروف الفبای لاتین و کمی بیشتر):

```js run
let str = '';

for (let i = 65; i <= 220; i++) {
  str += String.fromCodePoint(i);
}
alert( str );
// ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
// ¡¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ
```

می‌بینید؟ کاراکترهای حروف بزرگ اول هستند، سپس چند حرف خاص، سپس کارکترهای حروف کوچک، و `Ö` نزدیک به پایان خروجی است.

حالا واضح شد که چرا `a > Z`.

کاراکترها از طریق کدهای عددی خود مقایسه می‌شوند. کد بزرگتر به معنای بزرگتر بودن کاراکتر است. کد `a` (97) بزرگتر از کد `Z` (90) است.

- تمام حروف کوچک انگلیسی بعد از حروف بزرگ واقع هستند چون کدهای آنها بزرگتر هستند.
- بعضی از حروف مانند `Ö` از حروف الفبای اصلی جدا هستند. اینجا، کد آن از هر چیزی بین `a` تا `z` بزرگتر است.

### مقایسه‌های صحیح [#correct-comparisons]

الگوریتم "درست" برای انجام مقایسه رشته‌ها پیچیده‌تر از چیزی است که بنظر می‌آید، چون الفبا برای زبان‌های مختلف متفاوت است.

پس، مرورگر نیاز دارد که زبان را برای مقایسه کردن بداند.

خوشبختانه، تمام مرورگرهای مدرن (IE10 به کتابخانه اضافی [Intl.js](https://github.com/andyearnshaw/Intl.js/) احتیاج دارد) از استاندارد بین‌المللی‌کردن [ECMA-402](http://www.ecma-international.org/ecma-402/1.0/ECMA-402.pdf) پشتیبانی می‌کنند.

این استاندارد یک متد خاص را برای مقایسه رشته‌ها در زبان‌های مختلف را مهیا می‌کند که از قوانین خودشان پیروی می‌شود.

صدازدن [str.localeCompare(str2)](mdn:js/String/localeCompare) یک عدد صحیح را برمی‌گرداند که نشان می‌دهد آیا `str` با توجه به قوانین زبان، کمتر، مساوی یا برابر از `str2` هست یا نه:

- اگر `str` کمتر از `str2` باشد یک عدد منفی برمی‌گرداند.
- اگر `str` بزرگتر از `str2` باشد یک عدد مثبت برمی‌گرداند.
- اگر آنها برابر باشند `0` را برمی‌گرداند.

برای مثال:

```js run
alert( 'Österreich'.localeCompare('Zealand') ); // -1
```

این متد دو آرگومان اضافی دارد که در [مستندات](mdn:js/String/localeCompare) مشخص شده‌اند که به ما اجازه می‌دهند تا زبان را مشخص کنیم (به طور پیش‌فرض از شرایط فعلی بدست می‌آید، ترتیب حروف به زبان بستگی دارد) و قوانین اضافی را ایجاد کنیم مثل حساسیت بزرگی یا کوچکی حرف یا اینکه به یک صورت با `"a"` و `"á"` رفتار شود و غیره.

## داخلی‌ها، Unicode

<<<<<<< HEAD
```warn header="اطلاعات پیشرفته"
این بخش بیشتر درون رشته‌ها پیش می‌رود. این اطلاعات در صورتی که شما قصد داشته باشید با اموجی، کاراکترهای تصویری نادر ریاضی یا نشانه‌های نادر دیگر کار کنید برای شما مفید خواهد بود.

اگر قصد فرا گرفتن آنها را ندارید می‌توانید از این بخش بگذرید.
=======
```warn header="Advanced knowledge"
The section goes deeper into string internals. This knowledge will be useful for you if you plan to deal with emoji, rare mathematical or hieroglyphic characters or other rare symbols.
```

## Unicode characters

As we already mentioned, JavaScript strings are based on [Unicode](https://en.wikipedia.org/wiki/Unicode).

Each character is represented by a byte sequence of 1-4 bytes.

JavaScript allows us to specify a character not only by directly including it into a stirng, but also by its hexadecimal Unicode code using these three notations:

- `\xXX` -- a character whose Unicode code point is `U+00XX`.

    `XX` is two hexadecimal digits with value between `00` and `FF`, so `\xXX` notation can be used only for the first 256 Unicode characters (including all 128 ASCII characters).

    These first 256 characters include latin alphabet, most basic syntax characters and some others. For example, `"\x7A"` is the same as `"z"` (Unicode `U+007A`).
- `\uXXXX` -- a character whose Unicode code point is `U+XXXX` (a character with the hex code `XXXX` in UTF-16 encoding).

    `XXXX` must be exactly 4 hex digits with the value between `0000` and `FFFF`, so `\uXXXX` notation can be used for the first 65536 Unicode characters. Characters with Unicode value greater than `U+FFFF` can also be represented with this notation, but in this case we will need to use a so called surrogate pair (we will talk about surrogate pairs later in this chapter).
- `\u{X…XXXXXX}` -- a character with any given Unicode code point (a character with the given hex code in UTF-32 encoding).

    `X…XXXXXX` must be a hexadecimal value of 1 to 6 bytes between `0` and `10FFFF` (the highest code point defined by Unicode). This notation allows us to easily represent all existing Unicode characters.

Examples with Unicode:

```js run
alert( "\uA9" ); // ©, the copyright symbol

alert( "\u00A9" ); // ©, the same as above, using the 4-digit hex notation
alert( "\u044F" ); // я, the cyrillic alphabet letter
alert( "\u2191" ); // ↑, the arrow up symbol

alert( "\u{20331}" ); // 佫, a rare Chinese hieroglyph (long Unicode)
alert( "\u{1F60D}" ); // 😍, a smiling face symbol (another long Unicode)
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4
```

### جفت‌های جایگیر

تمام کاراکترهایی که اکثر اوقات استفاده می‌شوند کدهای 2 بایتی دارند. حروف در اکثر زبان‌های اروپایی، اعداد، و حتی اکثر حروف تصویری، یک نمایش 2 بایتی دارند.

<<<<<<< HEAD
اما 2 بایت فقط 65536 ترکیب را ممکن می‌سازد و این مقدار برای هر نشانه موجود کافی نیست. پس نشانه‌های نادر با جفتی از کاراکترهای 2 بایتی که "جفت جایگیر" (surrogate pair) هم نامیده می‌شوند کدگذاری می‌شوند.

طول چنین نشانه‌هایی `2` است:
=======
Initially, JavaScript was based on UTF-16 encoding that only allowed 2 bytes per character. But 2 bytes only allow 65536 combinations and that's not enough for every possible symbol of Unicode.

So rare symbols that require more than 2 bytes are encoded with a pair of 2-byte characters called "a surrogate pair".

As a side effect, the length of such symbols is `2`:
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

```js run
alert( '𝒳'.length ); // 2، X اسکریپت ریاضی حرف بزرگ 
alert( '😂'.length ); // 2، صورت با اشک شوق
alert( '𩷶'.length ); // 2، یک حرف تصویری نادر چینی
```

<<<<<<< HEAD
در نظر داشته باشید که جفت‌های جایگیر زمانی که جاوااسکریپت ساخته شد وجود نداشتند، و به این دلیل در حال حاضر توسط زبان به درستی پردازش نمی‌شوند!

ما در واقع در هر یک از رشته‌های بالا یک نشانه مفرد داریم، اما `length` طول `2` را نشان می‌دهد.

`String.fromCodePoint` و `str.codePointAt` دو متد نادر هستند که با جفت‌های جایگیر به درستی کار می‌کنند. آنها اخیرا به زبان اضافه شدند. قبل آنها، فقط [String.fromCharCode](mdn:js/String/fromCharCode) و [str.charCodeAt](mdn:js/String/charCodeAt) وجود داشتند. این متدها در واقع با `fromCodePoint/codePointAt` یکی هستند، اما با جفت‌های جایگیر کار نمی‌کنند.

گرفتن یک نشانه می‌تواند آسان نباشد، چون با جفت‌های جایگیر مثل دو کاراکتر رفتار می‌شود:

```js run
alert( '𝒳'[0] ); // ...نشانه‌های عجیب
alert( '𝒳'[1] ); // قطعه‌هایی از جفت جایگیر...
```

توجه کنید که قطعه‌های جفت جایگیر بدون یکدیگر هیچ معنی‌ای ندارند. پس alertها در مثال بالا در واقع چیزهای بدرد نخور نمایش می‌دهند.
=======
That's because surrogate pairs did not exist at the time when JavaScript was created, and thus are not correctly processed by the language!

We actually have a single symbol in each of the strings above, but the `length` property shows a length of `2`.

Getting a symbol can also be tricky, because most language features treat surrogate pairs as two characters.

For example, here we can see two odd characters in the output:

```js run
alert( '𝒳'[0] ); // shows strange symbols...
alert( '𝒳'[1] ); // ...pieces of the surrogate pair
```

Pieces of a surrogate pair have no meaning without each other. So the alerts in the example above actually display garbage.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

به طور فنی، جفت‌های جایگیر هم با کدهای خود قابل شناسایی هستند: اگر یک کاراکتر کدی در فاصله `0xd800..0xdbff` داشته باشد، پس قطعه اول یک جفت جایگیر است. کاراکتر بعدی (قطعه دوم) باید کدی در فاصله `0xdc00..0xdfff` داشته باشد. این بازه‌ها به طور اختصاصی برای جفت‌های جایگیر رزرو شده‌اند.

<<<<<<< HEAD
در مورد بالایی:

```js run
// جفت‌های جایگیر را نمی‌شناسد، پس کدهای قطعه‌ها را به ما می‌دهد charCodeAt
=======
So the methods `String.fromCodePoint` and `str.codePointAt` were added in JavaScript to deal with surrogate pairs.

They are essentially the same as [String.fromCharCode](mdn:js/String/fromCharCode) and [str.charCodeAt](mdn:js/String/charCodeAt), but they treat surrogate pairs correctly.

One can see the difference here:

```js run
// charCodeAt is not surrogate-pair aware, so it gives codes for the 1st part of 𝒳:
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

alert( '𝒳'.charCodeAt(0).toString(16) ); // d835

// codePointAt is surrogate-pair aware
alert( '𝒳'.codePointAt(0).toString(16) ); // 1d4b3, reads both parts of the surrogate pair
```

That said, if we take from position 1 (and that's rather incorrect here), then they both return only the 2nd part of the pair:

```js run
alert( '𝒳'.charCodeAt(1).toString(16) ); // dcb3
alert( '𝒳'.codePointAt(1).toString(16) ); // dcb3
// meaningless 2nd half of the pair
```

شما راه‌های بیشتری را برای کارکردن با جفت‌های جایگیر را در فصل <info:iterable> می‌آموزید. همچنین احتمالا کتابخانه‌های خاصی برای آنها وجود دارد، اما هیج کدام به اندازه کافی معروف نیستند تا اینجا معرفی شوند.

<<<<<<< HEAD
### نشانه‌های تفکیک کننده و عادی‌سازی
=======
````warn header="Takeaway: splitting strings at an arbitrary point is dangerous"
We can't just split a string at an arbitrary position, e.g. take `str.slice(0, 4)` and expect it to be a valid string, e.g.:

```js run
alert( 'hi 😂'.slice(0, 4) ); //  hi [?]
```

Here we can see a garbage character (first half of the smile surrogate pair) in the output.

Just be aware of it if you intend to reliably work with surrogate pairs. May not be a big problem, but at least you should understand what happens.
````

### Diacritical marks and normalization
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

در بسیاری از زبان‌ها نشانه‌هایی وجود دارند که ترکیبی از یک کاراکتر پایه و یک علامت در بالا/پایین آن هستند.

<<<<<<< HEAD
برای مثال، حرف `a` حرف پایه برای `àáâäãåā` است. اکثر کاراکترهای «ترکیب‌شده» متداول کد خود را در جدول UTF-16 دارند. اما نه همه آنها، چون ترکیبات ممکن بسیار زیادی وجود دارد.

برای پشتیبانی از ترکیبات دلخواه، UTF-16 به ما اجازه می‌دهد که از چند کاراکتر Unicode استفاده کنیم: کاراکتر پایه که بعد از آن یک یا چند کاراکتر «علامت» می‌آید که آن را «زیبا می‌کند».
=======
For instance, the letter `a` can be the base character for these characters: `àáâäãåā`.

Most common "composite" characters have their own code in the Unicode table. But not all of them, because there are too many possible combinations.

To support arbitrary compositions, Unicode standard allows us to use several Unicode characters: the base character followed by one or many "mark" characters that "decorate" it.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

برای مثال، اگر ما یک حرف `S` داشته باشیم که بعد از آن کاراکتر خاص «نقطه بالا» آمده باشد (کد `\u0307`)، به صورت Ṡ نمایش داده می‌شود.

```js run
alert( 'S\u0307' ); // Ṡ
```

اگر ما نیاز به یک علامت اضافی در بالای حرف داشته باشیم (یا پایین آن)، مشکلی نیست، فقط کاراکتر علامت مورد نیاز را اضافه می‌کنیم.

برای مثال، اگر ما یک کاراکتر «نقطه پایین» (کد `\u0323`) را ضمیمه کنیم، سپس ما «حرف S با نقطه‌هایی در بالا و پایین آن» خوهیم داشت: `Ṩ`.

برای مثال:

```js run
alert( 'S\u0307\u0323' ); // Ṩ
```

این روش انعطاف زیادی را مهیا می‌کند، اما یک مشکل جالب هم دارد: دو کاراکتر ممکن است که ظاهر یکسانی داشته باشند، اما با ترکیبات Unicode متفاوت نمایش داده شوند.

برای مثال:

```js run
let s1 = 'S\u0307\u0323'; // Ṩ ،نقطه بالا + نقطه پایین + S
let s2 = 'S\u0323\u0307'; // Ṩ ،نقطه پایین + نقطه بالا + S

alert( `s1: ${s1}, s2: ${s2}` );

alert( s1 == s2 ); // (!؟)می‌شود false با اینکه کاراکترها مشابه هستند اما
```

برای رفع این مشکل، یک الگوریتم «عادی‌سازی Unicode» وجود دارد که هر رشته را به یک شکل «عادی» درمی‌آورد.

این الگوریتم با [str.normalize()](mdn:js/String/normalize) پیاده‌سازی می‌شود.

```js run
alert( "S\u0307\u0323".normalize() == "S\u0323\u0307".normalize() ); // true
```

موضوع بامزه‌ای است که در این مورد ما `normalize()` در واقع یک دنباله از 3 کاراکتر را به یک کاراکتر تبدیل می‌کند: `\u1e68` (S به همراه دو نقطه).

```js run
alert( "S\u0307\u0323".normalize().length ); // 1

alert( "S\u0307\u0323".normalize() == "\u1e68" ); // true
```

<<<<<<< HEAD
در واقعیت، همیشه این مورد پیش نمی‌آید. به دلیل اینکه نماد `Ṩ` «به اندازه کافی متداول» است، پس سازندگان UTF-16 آن را در جدول اصلی آوردند و به آن یک کد دادند.
=======
In reality, this is not always the case. The reason being that the symbol `Ṩ` is "common enough", so Unicode creators included it in the main table and gave it the code.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

اگر شما می‌خواهید درباره قوانین و انواع عادی‌سازی بدانید، آنها در ضمیمه استاندارد Unicode تعریف شده‌اند: [شکل‌های عادی‌سازی Unicode](http://www.unicode.org/reports/tr15/)، اما برای اکثر کارهای عملی و کاربردی اطلاعات این بخش کافی است.

## خلاصه

<<<<<<< HEAD
- 3 نوع کوتیشن وجود دارد. Backtickها به ما این امکان را می‌دهند که رشته را به چند خط تقسیم کنیم و عبارت‌هایی را درون رشته جایگذاری کنیم `${…}`.
- رشته‌ها در جاوااسکریپت با استفاده از UTF-16 کدگذاری شده‌اند.
- ما می‌توانیم از کاراکترهای خاص مانند `\n` استفاده کنیم و حروف را از طریق کد Unicode آنها با استفاده از `\u...` بنویسیم.
- برای گرفتن یک کاراکتر، از `[]` استفاده کنید.
- برای گرفتن یک زیر رشته از `slice` یا `substring` استفاده کنید.
- برای تغییر بزرگی یا کوچکی حروف انگلیسی یک رشته، از `toLowerCase/toUpperCase` استفاده کنید.
- برای گشتن به دنبال یک زیر رشته از `indexOf` یا برای بررسی‌های ساده از `includes/startsWith/endsWith` استفاده کنید.
- برای مقایسه رشته‌ها با توجه به زبان آنها، از `localeCompare` استفاده کنید، در غیر این صورت آنها توسط کدهای کاراکتر مقایسه می‌شوند.
=======
- There are 3 types of quotes. Backticks allow a string to span multiple lines and embed expressions `${…}`.
- Strings in JavaScript are encoded using UTF-16, with surrogate pairs for rare characters (and these cause glitches).
- We can use special characters like `\n` and insert letters by their Unicode using `\u...`.
- To get a character, use: `[]`.
- To get a substring, use: `slice` or `substring`.
- To lowercase/uppercase a string, use: `toLowerCase/toUpperCase`.
- To look for a substring, use: `indexOf`, or `includes/startsWith/endsWith` for simple checks.
- To compare strings according to the language, use: `localeCompare`, otherwise they are compared by character codes.
>>>>>>> ff4ef57c8c2fd20f4a6aa9032ad37ddac93aa3c4

چند متد دیگر هم برای رشته‌ها وجود دارد:

- `str.trim()` -- فاصله را از ابتدا و انتهای رشته حذف می‌کند («می‌تراشد»).
- `str.repeat(n)` -- رشته را `n` بار تکرار می‌کند.
- ...و متدهای بیشتری در [مستندات](mdn:js/String) وجود دارند.

رشته‌ها متدهایی را برای جستجو/جایگزین‌کردن عبارات با قاعده (regular expression) دارند. اما این یک بحث بزرگ است، پس در یک قسمت جدای این آموزش <info:regular-expressions> توضیح داده شده است.