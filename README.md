# Update TimeZone Database

<div dir="rtl" style="direction: rtl">

در سال ۱۴۰۲ شمسی، دولت ایران تصمیم گرفت که دیگر ساعت تابستانی یک ساعت به جلو نرود. به همین دلیل، در سیستم عامل‌ها و نرم‌افزارهای مختلف، نیاز به بروزرسانی پایگاه داده‌ی منطقه‌ی زمانی است. در این ریپازیتوری، در تلاشیم که نحوه‌ی بروزرسانی پایگاه داده‌ی منطقه‌ی زمانی برای زبان‌ها و سیستم‌عامل‌های مختلف را در کنار هم جمع‌آوری کنیم.

این ریپازیتوری متن‌باز است و کاملا از اصلاحات و pull requestهای شما برای تکمیل آن استقبال می‌شود.
</div>


# OSs

## Windows

## Linux

### Ubuntu/Debian (apt based)
<div dir="rtl" style="direction: rtl">

در لینوکس، عموما بسته‌ی `tzdata` وظیفه‌ی نگهداری اطلاعات تایم‌زون‌های مختلف را بر عهده دارد. برای آپگرید آن می‌توانید دستورات زیر را در ترمینال بزنید:
</div>

```
sudo apt update
sudo apt install tzdata
```

<div dir="rtl" style="direction: rtl">

اگر در محیط Docker و مثلا در Dockerfile نیاز به آپدیت دارید، لازم است که در حالت غیر تعاملی (non interactive) دستورات را اجرا کنید
</div>

```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install tzdata
```

<div dir="rtl" style="direction: rtl">

برای بررسی عدم تغییر ساعت در سال ۱۴۰۲، مثلا دستور زیر را اجرا کنید:
</div>

```bash
TZ=Asia/Tehran date --date='@1679589000'
```

<div dir="rtl" style="direction: rtl">

خروجی باید مقدار زیر باشد:
</div>

```
Thu Mar 23 08:00:00 PM +0330 2023
```


## Android
<div dir="rtl" style="direction: rtl">
اگر گوشی شما root شده نیست و دسترسی superuser ندارید، طبق جستجوی من، تنها راه بروزرسانی پایگاه داده‌ی منطقه‌های زمانی، بروزرسانی نسخه‌ی اندروید گوشی است و اگر نسخه‌ی جدید برای اندروید شما منتشر نشود، راه چاره‌ای برای بروزرسانی منطقه‌های زمانی به جز روت کردن گوشی نیست.

البته می‌توانید تنظیمات تنظیم خودکار ساعت براساس اینترنت و منطقه‌ی زمانی را غیر فعال کنید و به شکل دستی، ساعت خود را تغییر دهید.

اما اگر گوشی شما روت‌شده باشد، می‌توان با ابزاری مثل ریپازیتوری [https://github.com/meefik/tzupdater](https://github.com/meefik/tzupdater) فایل‌های tzdata را بروزرسانی کرد. البته ما این نرم‌افزار را تست نکردیم و اطلاعی از عواقب استفاده از آن (مانند بوت نشدن گوشی بعد از استفاده!) را نمی‌دانیم.
</div>

# Languages / Frameworks
## Python
<div dir="rtl" style="direction: rtl">

طبق 
[داکیومنت پایتون](docs.python.org/3/library/zoneinfo.html)، اطلاعات مربوط به منطقه‌های زمانی از سیستم گرفته می‌شود و اگر این دیتا موجود نباشد، از پکیج `tzdata` گرفته می‌شود.
در نتیجه، در قدم اول، بروزرسانی اطلاعات تایم‌زون‌ها رو سیستم عامل‌ها را ببینید و برای بروزرسانی پکیج tzdata از pypi، از دستور زیر استفاده کنید:
</div>

```bash
pip install -U tzdata
```

<div dir="rtl" style="direction: rtl">

برای تست اینکه بروزرسانی به دسترسی انجام شده، مثلا بررسی اینکه عدم تغییر ساعت سال ۱۴۰۲ شمسی اعمال شده، 
می‌توانید با کد زیر امتحان کنید:
</div>

```python
from datetime import datetime
from zoneinfo import ZoneInfo

print(datetime(2023, 3, 23, 16, 30, tzinfo=ZoneInfo('UTC')).astimezone(ZoneInfo('Asia/Tehran')).isoformat())
# outputs: 2023-03-23T20:00:00+03:30

```


### Django
<div dir="rtl" style="direction: rtl">

از جنگوی نسخه‌ی ۳.۲ به قبل، جنگو از پکیج `pytz` برای اطلاعات منطقه‌ی زمانی استفاده می‌کرد. در جنگوی ۳.۲، امکان استفاده از پیاده‌سازی‌های دیگر مثل zoneinfo اضافه شد و از جنگوی ۴.۰، استفاده از zoneinfo که پیش‌فرض پایتون است به عنوان پیاده‌سازی پیش‌فرض مورد استفاده قرار گرفت.

با توجه به توضیح بند قبل، اگر از لایبرری pytz استفاده می‌کنید، با دستور زیر باید آن را بروزرسانی کنید:
</div>

```bash
pip install -U pytz
```
## Java
<div dir="rtl" style="direction: rtl">

در زبان جاوا، `JRE` تایم‌زون پیش‌فرض را از سیستم عامل می‌گیرد، با این حال، خودش نیز یک پایگاه داده از منطقه‌های زمانی را نگهداری می‌کند که در آن مشخصات و تنظیمات مربوط به DST موجود است. پایگاه داده‌ی منطقه‌های زمانی جاوا در 
`<install_dir>/jre/lib/zi`
ذخیره شده است و ابزاری به نام `tzupdater` توسط oracle برای بروزرسانی آن نوشته شده است. دستورهای راهنمای بعد برای لینوکس نوشته شده است، در دیگر سیستم عامل‌ها دستورات معادل را برای دانلود فایل و اجرای جاوا استفاده کنید.

این ابزار، متن باز نیست، اما شرکت Azul یک نسخه‌ی معادل متن‌باز برای آن منتشر کرده است. این ابزار، با ورودی گرفتن دیتابیس منطقه‌های زمانی، آن را در جاوا بروزرسانی می‌کند. در ادامه، آموزش دانلود tzupdater و استفاده از آن برای بروزرسانی منطقه‌ی زمانی در جاوا را آورده‌ایم:

ابتدا ابزار tzupdater را دانلود کنید، اطلاعات بیشتر درباره‌ی آن در 
[این لینک](https://www.azul.com/products/open-source-tools/ziupdater-time-zone-tool/)
آمده است.
</div>

```bash
wget https://cdn.azul.com/tools/ziupdater1.1.1.1-jse8+7-any_jvm.tar.gz
tar -xzf ziupdater1.1.1.1-jse8+7-any_jvm.tar.gz
```

<div dir="rtl" style="direction: rtl">

سپس، آخرین نسخه از دیتابیس منطقه‌های زمانی را دانلود کنید. وب‌سایت 
[iana.org](https://www.iana.org/time-zones)
یکی از مراجع نگهداری اطلاعات zoneinfo است.
</div>

```
wget https://www.iana.org/time-zones/repository/tzdata-latest.tar.gz
```

<div dir="rtl" style="direction: rtl">

و سپس، ابزار `tzupdater` را با دستور زیر اجرا کنید.
</div>

```
java -jar ziupdater-1.1.1.1.jar -l file://$(pwd)/tzdata-latest.tar.gz
```

<div dir="rtl" style="direction: rtl">

برای بررسی اینکه دیتابیس تایم‌زون‌ها برای سال ۱۴۰۲ شمسی بروز شده باشد، می‌توانید با کد جاوایی زیر زمان را تست کنید:

```java
import java.util.*;

public class TestTimeZone {
    public static void main(String[] args) {
        Calendar calendar = Calendar.getInstance(TimeZone.getTimeZone("Asia/Tehran"));
        calendar.setTimeInMillis(1679589000000L);
        System.out.println(String.format("%tFT%<tR", calendar));
        // output: 2023-03-23T20:00
    }
}
```

# Softwares
## Databases
### Mysql

### Postgresql
<div dir="rtl" style="direction: rtl">

در پستگره، اطلاعات مربوط به منطقه‌های زمانی، به همراه باینری پستگره است و با جستجو روشی جز بروزرسانی خود پستگره برای آپدیت آن پیدا نکردیم. پستگره به شکل مداوم، در نسخه‌های minorش، آپدیت برای tzdata هم ارائه می‌دهد. می‌توانید 
[release note](https://www.postgresql.org/docs/release/)‌های 
پستگره را در این رابطه بخوانید.

اگر از نسخه‌های قدیمی پستگره که بروزرسانی‌ای برای آن ارائه نمی‌شود استفاده می‌کنید، یک راه‌کار بیلد دستی نسخه‌ی جدید با تایم‌زون‌های آپدیت شده است. در سورس کد پستگره، یک فایل `tzdata.zi` وجود است که اطلاعات منطقه‌های زمانی در آن ذخیره شده است. مثلا در نسخه‌ی ۱۵.۲، این فایل در اینجا قرار دارد: https://github.com/postgres/postgres/blob/REL_15_2/src/timezone/data/tzdata.zi

آخرین نسخه‌ی فایل tzdata.zi را از دیتابیس iana می‌توانید از اینجا دانلود کنید: https://data.iana.org/time-zones/tzdb/tzdata.zi

آموزش نصب پستگره از سورس کد نیز در این لینک قرار دارد: https://www.postgresql.org/docs/15/installation.html
</div>

# SEO
<div dir="rtl" style="direction: rtl">
این بخش برای بهبود سئوی این صفحه درست شده است. آموزش حل تغییر نکردن، بروز نشدن ساعت در سال جدید، چگونی حل کردن مشکل عوض نشدن ساعت، یک ساعت جلو بودن یا عقب بودن در این صفحه نوشته شده است.
</div>