<div id="readme" class="Box-body readme blob js-code-block-container p-5 p-xl-6 gist-border-0" dir="rtl">
    <article class="markdown-body entry-content container-lg" itemprop="text"><table>
  <thead>
  <tr>
  <th>wts</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div><table>
  <thead>
  <tr>
  <th>title</th>
  <th>module</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div>21 - حساب اتفاقيات مستوى الخدمة المركبة (5 دقائق)</div></td>
  <td><div>الوحدة 06: وصف إدارة التكاليف واتفاقيات مستوى الخدمة في Azure</div></td>
  </tr>
  </tbody>
</table>
</div></td>
  </tr>
  </tbody>
</table>
       
# 21 - حساب اتفاقيات مستوى الخدمة المركبة (5 دقائق)

في هذه المعاينة، سنحدد مدى توفر اتفاقية مستوى الخدمة لخدمات Azure ثم نحسب التوفر المتوقع المستند إلى اتفاقية مستوى الخدمة المركبة للتطبيق.

يتكون تطبيق المثال الخاص بنا من خدمات Azure هذه. لن نتناول التكوين والاعتبارات المعمارية العميقة، ولكن يتمثل الهدف هنا في تقديم مثال رفيع المستوى.

+ **خدمة التطبيق**: لاستضافة التطبيق.
+ **شركة إلى عميل Azure AD**: لمصادقة تسجيلات دخول المستخدم وإدارة ملفات التعريف.
+ **بوابة التطبيق**: لإدارة الوصول إلى التطبيق والتحجيم. 
+ **قاعدة بيانات Azure SQL**: لتخزين بيانات التطبيق. 

# المهمة 1: تحديد قيم النسبة المئوية لوقت تشغيل اتفاقية مستوى الخدمة للتطبيق

1. في المستعرض، انتقل إلى صفحة [ملخص اتفاقية مستوى الخدمة لخدمات Azure](https://azure.microsoft.com/ar-sa/support/legal/sla/summary/).

2. حدد موقع قيمة وقت تشغيل اتفاقية مستوى الخدمة الخاصة **بخدمة التطبيق** ، **99.95%**. انقر فوق **عرض التفاصيل الكاملة**، ثم قم بتوسيع **تفاصيل اتفاقية مستوى الخدمة**. لاحظ **النسب المئوية لوقت التشغيل الشهري** و**أرصدة الخدمة**.

3. ارجع إلى صفحة ويب اتفاقية مستوى الخدمة وحدد موقع خدمة **شركة إلى عميل Azure Active Directory** وحدد قيمة وقت تشغيل اتفاقية مستوى الخدمة، **99.9%**. 

4. حدد موقع قيمة وقت تشغيل اتفاقية مستوى الخدمة الخاصة **ببوابة التطبيق** ، **99.95%**. 

5. تستخدم قاعدة بيانات Azure SQL مستويات Premium ولكن لم يتم تكوينها لعمليات التوزيع المتكررة في المنطقة. حدد موقع قيمة وقت تشغيل اتفاقية مستوى الخدمة الخاصة **بقاعدة بيانات Azure SQL** ، **99.99%**. 

    **ملاحظة**: هناك قيم مختلفة لوقت التشغيل للتكوينات وعمليات التوزيع المختلفة لقاعدة بيانات Azure SQL. من المهم أن تكون واضحًا بشأن قيم وقت التشغيل المطلوبة، عند التخطيط وتحديد تكلفة التوزيع والتكوين. يمكن أن تؤثر التغييرات الصغيرة في وقت التشغيل على تكاليف الخدمة بالإضافة إلى احتمال زيادة التعقيد في التكوين. قد تتضمن بعض الخدمات الأخرى التي قد تكون ذات أهمية في صفحة ويب ملخص اتفاقية مستوى الخدمة من Azure **الأجهزة الظاهرية** و**حسابات التخزين** و**قاعدة بيانات Cosmos**.

# المهمة 2: حساب النسبة المئوية لوقت تشغيل اتفاقية مستوى الخدمة المركبة للتطبيق

1. في حالة عدم توفر أي من الخدمات التي يتألف منها تطبيقنا، فلن يتاح تطبيقنا للمستخدمين لتسجيل الدخول إليه واستخدامه. على هذا النحو، يتكون إجمالي وقت التشغيل لتطبيقنا مما يلي:

    **النسبة المئوية لوقت تشغيل خدمة التطبيق** X **النسبة المئوية لوقت تشغيل شركة إلى عميل Azure AD** X **النسبة المئوية لوقت تشغيل بوابة تطبيق Azure** X **النسبة المئوية لوقت تشغيل قاعدة بيانات Azure SQL** = **إجمالي النسبة المئوية لوقت التشغيل**

    وهي من حيث النسبة المئوية على النحو التالي:

    **99.95%** X **99.9%** X **99.95%** X **99.99%** = **99.79%**

    هذا هو التوفر المتوقع المستند إلى اتفاقية مستوى الخدمة لتطبيقنا مع الخدمات والبنية الحالية.

تهانينا! لقد حددتَ وقت التشغيل المستند إلى اتفاقية مستوى الخدمة لكل خدمة من الخدمات الموجودة في عينة التطبيق لدينا، ثم حسبتَ التوفر المتوقع المستند إلى اتفاقية مستوى الخدمة المركبة للتطبيق.
