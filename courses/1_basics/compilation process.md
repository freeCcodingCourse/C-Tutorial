<div dir="rtl">
<h1>از سورس کد تا اجرا </h1>

در ادامه قصد داریم نگاهی عمیق تر به روند اجرای یک برنامه به زبان سی داشته باشیم، اینکه چگونه کدهایی که برای ما خواناست تبدیل زبان ماشین شده و قابل اجرا میشود.

قبل ازینکه به ادامه بحث بپردازیم نیاز داریم که به یک سری مفاهیم اشاره کنیم ،‌ یکی از آن مفاهیم کد ماشین هست. کد ماشین درواقع یک ترتیب خاص از توالی ۰ ها و ۱ ها است که برای ماشین و سخت افزار قابل فهم است درواقع تنها چیزی که برای یک ماشین قابل درک است ۰ و ۱ است.

حال این پرسش نمایان میشود که چگونه کدهایی که ما با نمادهای قابل فهم برای خودمان مینویسیم توسط ماشین اجرا میشود؟

اینجا جایی است که دقیقا اهمیت کامپایلر نمایان میشود. همانطور که به طور خلاصه در قسمت قبل مشاهده کردید (و البته به طور جدی تر در آینده مشاهده خواهید کرد) زبان سی و دستور نحو آن مجموعه ای از کلید واژه ها و نماد های قابل فهم است طوری که ما با کمترین تلاش میتوانیم کلیت آن را درک کنیم. از این جهت از سی به همراه برخی دیگر از زبان ها به عنوان زبان سطح بالا یاد میشود.

از این جهت برنامه ای که به زبان سی نوشته میشود نیازمند این است که به کد ماشین متناظر آن تبدیل شود به گونه ای که ماشین یا سخت افزار ما قادر به اجرای آن باشد.

> درواقع به اون روندی که کد ما به کد ماشین تبدیل میشه کامپایل گفته میشه

به عنوان یک نکته باید توجه داشته باشیم که کد ماشین تولید شده بسیار مرتبط است با نوع معماری سخت افزار و نوع سیستم عامل. از این جهت کد ماشینی که در یک سیستم عامل توسط کامپایلر ایجاد شده برای یک سیستم عامل دیگر سازگار و قابل اجرا نیست.

>  به همین دلیله که موقع نصب کامپایلر با نسخه های مختلف اون برای سیستم عامل های مختلف مواجه میشید. پس حتما به این موضوع توجه کنید.

> یکی از مناسبترین کامپایلر ها جی سی سی هست که استاندارد های زیادی رو ساپورت میکنه و ما به احتمال زیاد از اون استفاده میکنیم

روند کامپایل شدن یک برنامه به زبان سی چهار مرحله رو طی میکنه :

+ preprocessing
+ compiling
+ assembling
+ linking

برای توضیح این چهار مرحله بگذارید از کدی که در قسمت قبلی بررسی شد استفاده کنیم :

</div>

```c
#include <stdio.h>

int main(){
   
   /* my first program in C */
   
   printf("Hello World! \n");

   return 0;
}
```

<div dir="rtl">
فرض کنیم اسم فایلی که این تکه کد در آن قرار دارد main.c است. پسوند .c در واقع پسوندی است که برای فایل هایی که به زبان سی نوشته شده اند استفاده میشود.

اولین خط بیانگر یک دستور پیش پردازنده است که کار آن در این کد در دسترس قرار دادن کتابخانه stdio.h است.
> ینی چی در دسترس قرار دادن کتابخانه؟ اصلا کتابخانه چیه؟
>
> به زبان ساده کتابخانه مجموعه ایه از یک سری کدهای از قبل آماده شده است که ما میتونیم از اونها استفاده کنیم بدون اینکه نیاز باشه از اول خودمون اون کد رو بزنیم. به عنوان مثال با دستور printf به طور مختصر در قسمت قبل آشنا شدید ،‌این دستور خودش یکی از دستورات کتابخانه stdio.h هست که در پشت صحنه این دستور شامل جزییاتی در پیاده سازیه که در کتابخانه stdio.h قرار گرفته. تصور کنید از قبل این دستور رو پیاده سازی نکرده بودند، اتفاقی که میفتاد این بود که هربار میخواستیم یک عبارت ساده رو روی اسکرین نمایش بدیم کلی باید کد میزدیم که بتونیم برای این موضوع با سیستم عامل حرف بزنیم.اما نویسنده های این زبان این کار هارو از قبل کردن که ما نخوایم اینکار رو تکرار کنیم و هربار نیاز شد صرفا خود این دستور رو فراخوانی کنیم. حالا اگر اول کدمون این کتابخانه را با این شکل فراخوانی نکنیم خروجی ای برای ما چاپ نمیشه ، چرا؟ چون اون دستور خاص نمیدونه از کجا پیدا کنه.

نقطه شروع اجرای هر برنامه ای تابع main هست (با مفهوم تابع جلوتر آشنا میشید) در واقع برنامه با اجرا کردن دستورات در این تابع اجرا میشود.
در مثال ما تابع main شامل دو عبارت اجرا شدنی و یک کامنت هست (کامنت ها هم جلوتر بررسی میشن) تابع printf اون عبارتی که بهش دادیم را در صفحه نمایش به عنوان خروجی چاپ میکند و عبارت بعدی برنامه را ملزم به این میکند که اگر به شکل درست اجرا شد و به پایان رسید مقدار صفر را برگرداند.

برای درک بهتر خوب است که پروسه کامپایل رو مرحله به مرحله رصد کنیم:
## preprocessor

هنگامی که این بخش تکه کد ما را تحویل میگیرد دو کار مهم را انجام میدهد:

۱.تمام کامنت های موجود در کد را پاک میکند چرا که کامنت ها صرفا برای داکیومنت کردن هستند و نیازی به اجرا ندارند.(همانطور که گفته شد با کامنت ها جلوتر آشنا میشید)

۲.سورس کد هر یک از کتابخانه هایی را که در کد تعیین شده را در دسترس قرار میدهد.(یه نمونه ش همون کتابخانه stdio.h)

در این قسمت کار های بیشتری انجام میشود که با آنها در بخش پیش پردازنده آشنا خواهید شد.



## compiling

در این مرحله کامپایلر gcc یک سری تغییرات روی کد از پیش پردازش شده میدهد و آن را برای assembler آماده میکند. البته شایان ذکر هست که برخی دیگر از کامپایلر ها در این مرحله کد اسمبلی را تولید میکنند.

## assembling

در این مرحله assembler کد های آماده شده در مرحله قبل را تحویل میگیرد و با استفاده از آن کد های قابل فهم برای ماشین را تولید میکند.
یک مرحله به اجرا نزدیک تر...


## linking

در این مرحله فایل اجرایی نهایی آماده میشود . در واقع همانطور که از اسم این مرحله پیداست ، در این مرحله کد های باینری تولید شده از هر فایل سورس در مرحله قبل ، بهم لینک یا به عبارتی یکپارجه میشوند تا برنامه به درستی اجرا شود.


بعد از اجرای این چهار مرحله یک فایل main.exe در اختیار ما قرار میگیرد که یک فایل قابل اجرا از کد ماست و میشود آن را اجرا کرد.

لازم به ذکر است که کامپایلر gcc شامل آپشن هاییست که به ما این امکان را میدهد که در هر مرحله پروسه کامپایل را متوقف کرده و خروجی را در آن مرحله پیگیری کنیم. جلوتر به این مورد پرداخته میشود


> هدف از این بخش این بود که بتونیم درک درستی از روند اجرا و کامپایل بهتون منتقل کنیم. اما باید این نکته رو خاطر نشان کنیم که مباحث این بخش پیچیده تر از اونیه که بشه کامل توضیح داد. اما اگه جزییات این مطالب براتون مبهم بود جای نگرانی نیست صرفا هدف این بود که شما با کلیت این موضوع در این مرحله آشنا بشید. جزییات بیشتر به مرور در جلسات بعدی در ذهنتون جا باز میکنن.
</div>