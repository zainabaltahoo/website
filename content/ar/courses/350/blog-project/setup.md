---
# Page title
# عنوان الصفحة
title: Django Project and App Setup
العنوان: مشروع جانغو واعداد التطبيق
# Title for the menu link if you wish to use a shorter link title, otherwise remove this option.
# عنوان رابط القائمة اذا كنت ترغب في استخدام عنوان ارتباط اقصر, والا فقم بازالة هذا الخيار.
linktitle: Setup
عنوان الرابط: اعداد
# Date page published
# تاريخ نشر الصفحة
date: 2021-03-23
التاريخ: 32-3-2021
# Academic page type (do not modify).
# عنوان الصفحة الاكاديمية (لاتعدل عليه)
type: book
النوع: كتاب
# Position of this page in the menu. Remove this option to sort alphabetically.
# مكان هذة الصفحة في القائمة. قم بازالة هذا الخيار للترتيب ابجديا.
weight: 1
الوزن: 1
draft: False
المسودة: خطأ

---

{{% callout note %}}
Switch to branch **1-setup** from **malmarz/isom350-blog** github repo to see this step's implementation
{{% /callout %}}
{{%مذكرة شرح%}}
 انتقل الى الفرع **1-setup** من **malmarz/isom350-blog** github repo لرؤية تنفيذ هذه الخطوات
{{%مذكرة الشرح%}}

To setup our blog project, create a replit using **Django Template**. You will initially get a code structure that looks like the following:
لاعداد مشروع المدونة الخاص بنا , قم بانشاء replit باستخدام **قالب جانغو** 

{{< figure src="courses/350/project-structure.png" caption="Project Structure" >}}

We must then create an app directory for our code because in Django, we must create at least a sinlge app in our project to be able to write code. We use the shell commands provided by Django to easily generate the app directory that will hold our code by first openning the shell:
يجب علينا بعد ذلك انشاء دليل تطبيق لرمزنا لانه في  جانغو , يجب علينا على الاقل انشاء تطبيق واحد في مشروعنا لنستطيع كتابة التعليمات البرمجية. نحن نستخدم اوامر shell التي يوفرها جانغو لانشاء دليل التطبيق الذي سيحمل الكود الخاص بنا عن طريق فتح shell اولا 

{{< figure src="courses/350/shell.png" caption="Using the Shell" >}}

Now in the shell, type the following command:
الان في shell اطبع الاوامر التالية

```bash
python manage.py startapp blog
```

The system will perform a few tasks and you will notice that a new **blog** directory is created in your project containing a set of files:
سيقوم النظام ببعض المهام وستلاحظ انه تم انشاء دليل مدونة جديد في مشروعك يحتوي على مجموعة من الملفات:

{{< figure src="courses/350/app.png" caption="Blog App Directory" >}}

**If you do get an error** when typing the command click on the Run{{< icon name="play" pack="fas" >}} button up top and make sure everything is running correctly, then stop the server and type the startapp shell command again and it should work this time. If your project was setup correctly, you should see the following screen:
**ادا تلقيت خطأ** عند كتابة الأوامر اضغط فوق الزر تشغيل في الاعلى وتأكد من ان كل شيء يعمل بشكل صحيح, ثم اوقف الخادم واكتب امر startapp shell مرة اخرى ويجب ان يعمل هدة المرة. اذا تم اعداد مشروعك بشكل صحيح, فستظهر لك الشاشة التالية:

{{< figure src="courses/350/dev-server.png" caption="Django Development Server Running" >}}

The app directory will contain the standard files you will need to put your code in. They are:
1. **admin.py:** Using to configure the admin interface for managing all the data.
2. **models.py:** Where you put the data definitions for your blog application.
3. **views.py:** Where you put all the functions to handle HTTP requests and generate the HTTP responses.
سيحتوي دليل التطبيق على الملفات القياسية التي ستحتاجها لوضع التعليمات  البرمجية الخاصة بك. وهي:

1. **admin.py**: يستخدم لتكوين واجهة المسؤول لادارة جميع البيانات.
2. **models.py**: حيث تضع تعريفات البيانات لتطبيق المدونة الخاص بك.
3. **views.py**: حيث تضع جميع الوظائف لمعالجة طلبات HTTP وتوليد استجابات HTTP.

These are the most important ones that you need to know at this time, and you will also need to create a few others as we progress in the project. 
هذه هي اهم الاشياء التي تحتاج الى معرفتها في هذا الوقت , وستحتاج ايضا الى انشاء عدد قليل منهم اثناء تقدمنا في المشروع.

Typically, we keep related features in their own app directoy. Every project must have at least a single app directory to hold the functionaloty created by the developer. If for example we need to include a shopping cart in our blog or an ecommerce component, we can create another app in our project named **cart** and place all ecommerce functionality in that directory. Similarly, we we introduce authentication and user management we would create an **accounts** directory and include all user management functionality there. So the apps are a matter of organization. 
عادة, نحتفظ بالميزات ذات الصلة في دليل التطبيق الخاص بهم. يجب ان يحتوي كل مشروع على دليل تطبيق واحد على الاقل للاحتفاظ بالوظيفة التي أنشأها المطور. اذا احتجنا على سبيل المثال الى تضمين عربة تسوق في مدونتنا او احد مكونات التجارة الالكترونية, فيمكننا انشاء تطبيق اخر في مشروعنا يسمى عربة التسوق ووضع جميع وظائف التجارة الالكترونية في هذا الدليل. وبالمثل نقدم المصادقة وادارة المسنخدم, وسننشى دليل حسابات ونضمن جميع وظائف ادارة المستخدمين هناك. لذا فان التطبيقات هي مسألة تنظيم. 

The general rule is to organize related functionality in the same directory. Developers will differ in how they organize functionality and how related they see things are. With experience, you will improve in organizing your project. At this stage of your career, how you organize your code will not have a significant impact on your project. It is mostly related to the reusability of the app in other projects, which might be important to you in the future.
القاعدة العامة هي تنظيم الوظائف ذات الصلة في نفس الدليل. سيختلف المطورون في كيفية تنظيمهم للوظائف ومدى ارتباطهم بالاشياء. ومع الخبرة, سوف تتحسن في تنظيم مشروعك. في هذة المرحلة من حياتك المهنية, لن يكون لكيفية تنظيم الكود الخاص بك تأثير كبير على مشروعك. يرتبط في الغالب بامكانية اعادة استخدام التطبيق في مشاريع اخرى , والتي قد تكون مهمه بالنسبة لك في  المستقبل.