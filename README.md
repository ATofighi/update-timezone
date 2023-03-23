# Update TimeZone Database

<div dir="rtl" style="direction: rtl">
در سال ۱۴۰۲ شمسی، دولت ایران تصمیم گرفت که دیگر ساعت تابستانی یک ساعت به جلو نرود. به همین دلیل، در سیستم عامل‌ها و نرم‌افزارهای مختلف، نیاز به بروزرسانی پایگاه داده‌ی منطقه‌ی زمانی است. در این ریپازیتوری، در تلاشیم که نحوه‌ی بروزرسانی پایگاه داده‌ی منطقه‌ی زمانی برای زبان‌ها و سیستم‌عامل‌های مختلف را در کنار هم جمع‌آوری کنیم.
</div>


# OSs

## Windows

## Linux

### Ubuntu/Debian (apt based)
<div dir="rtl" style="direction: rtl">

در لینوکس، عموما بسته‌ی `tzdata` وظیفه‌ی نگهداری اطلاعات تایم‌زون‌های مختلف را بر عهده دارد. برای آپگرید آن می‌توانید دستورات زیر را در ترمینال بزنید:

```
sudo apt update
sudo apt install tzdata
```

اگر در محیط Docker و مثلا در Dockerfile نیاز به آپدیت دارید، لازم است که در حالت غیر تعاملی (non interactive) دستورات را اجرا کنید

```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install tzdata
```

برای بررسی عدم تغییر ساعت در سال ۱۴۰۲، مثلا دستور زیر را اجرا کنید:

```bash
TZ=Asia/Tehran date --date='@1679589000'
```

خروجی باید مقدار زیر باشد:
```
Thu Mar 23 08:00:00 PM +0330 2023
```

</div>

## Android


# Languages / Frameworks
## Python

### Django

## Java

# Softwares
## Databases
### Mysql

### Postgresql


# SEO
<div dir="rtl" style="direction: rtl">
این بخش برای بهبود سئوی این صفحه درست شده است. آموزش حل تغییر نکردن، بروز نشدن ساعت در سال جدید، چگونی حل کردن مشکل عوض نشدن ساعت، یک ساعت جلو بودن یا عقب بودن در این صفحه نوشته شده است.
</div>