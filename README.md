<div dir="rtl">
    <h1>تطوير موقع استضافة فيديوهات</h1>
    <p>الشيفرة المصدرية لتطبيق موقع استضافة فيديوهات من دورة "تطوير تطبيقات الويب باستخدام PHP" المقدمة من أكاديمية حسوب</p>

<a href="https://academy.hsoub.com/learn/php-web-application-development/">دورة تطوير تطبيقات الويب باستخدام  PHP</a>
---

# خطوات تشغيل المشروع

* إنشاء الحزم اللازمة لتشغيل المشروع بتنفيذ :
<h6 dir="ltr">

`composer install`

</h6>

<h6 dir="ltr">

`npm install`

</h6>

* إنشاء ملف باسم `env.` في المسار الأساسي للمشروع.
* تعبئة الملف `env.` بالبيانات، و نستطيع نسخ هذه البيانات من الملف `env.example.` ولصقها بداخل الملف `env.` و التعديل عليها.
* تغيير اسم قاعدة البيانات في الملف `env.` باسم مشابه تمامًا لقاعدة البيانات التي أنشأناها.
* في ملف `env.` نحدد نوع التخزين ب `s3`
<h6 dir="ltr">

`FILESYSTEM_DRIVER=s3`

</h6>

* مقاطع الفيديو التي تُرفع على الموقع تُخزن في `amazon s3`، لذلك يجب إنشاء حساب في `amazon s3` وربطه مع المشروع
<h6 dir="ltr">

`AWS_ACCESS_KEY_ID=`

</h6>

<h6 dir="ltr">

`AWS_SECRET_ACCESS_KEY=`

</h6>

<h6 dir="ltr">

`AWS_DEFAULT_REGION=`

</h6>
<h6 dir="ltr">

`AWS_BUCKET=`

</h6>


* يحتوي المشروع على نظام إشعارات، استخدمنا خدمة الاستضافة `pusher` لإنشاء إشعارات في الوقت الحالي، لذلك لكي تعمل الإشعارات لديك يجب إنشاء حساب في موقع `pusher.com` وربط ال api مع المشروع
<h6 dir="ltr">

`PUSHER_APP_ID=`

</h6>

<h6 dir="ltr">

`PUSHER_APP_KEY=`
`
</h6>

<h6 dir="ltr">

`PUSHER_APP_SECRET=`

</h6>

* بعدها لإنشاء مفتاح خاص بالمشروع ننفذ الأمر:
<h6 dir="ltr"> 

`php artisan key:generate`

</h6>

* بعدها لإنشاء وصلة مع المجلد storage الذي يحتوي على الصور ومقاطع الفيديو ننفذ الأمر:
<h6 dir="ltr"> 

`php artisan storage:link`

</h6>

* الآن أصبح المشروع جاهز للتشغيل ننفذ الأمر:
<h6 dir="ltr">

`php artisan serve`

</h6>

* ننسخ الرابط الذي ظهر ونلصقه بالمتصفح.

* لتشغيل المهمة `job` التي تعمل على معالجة مقاطع الفيديو في الخلفية ننفذ الأمر التالي في نافذة `Console` جديدة
<h6 dir="ltr">

`php artisan queue:work`

</h6>

# ملاحظة: 
نستطيع أيضًا تحويل المشروع ليعمل على القرص المحلي وذلك باتباع بعض الخطوات البسيطة:

* من ملف `env.` نغير قيمة `FILESYSTEM_DRIVER` من `s3` إلى `public`
<h6 dir="ltr">

`FILESYSTEM_DRIVER=public`

</h6>


* ولا ننسى إيقاف عمل المهمة `job` بالضغط على `Ctrl+c` وإعادة تشغيلها من جديد

* الآن بعد أن أصبح المشروع يعمل على القرص المحلي نستطيع ملىء قاعدة البيانات بالبذور
<h6 dir="ltr">

`php artisan migrate:fresh --seed`

</h6>
</div>