---
wts:
  title: 10 - إنشاء جهاز ظاهري باستخدام PowerShell (10 دقائق)
  module: 'Module 03: Describe core solutions and management tools'
ms.openlocfilehash: a6c6e26b535658ebb01beac8037adcb5c15dc6e8
ms.sourcegitcommit: 26c283fffdd08057fdce65fa29de218fff21c7d0
ms.translationtype: HT
ms.contentlocale: ar-SA
ms.lasthandoff: 01/27/2022
ms.locfileid: "137907192"
---
# <a name="10---create-a-vm-with-powershell-10-min"></a>10 - إنشاء جهاز ظاهري باستخدام PowerShell (10 دقائق)

في هذا المعاينة، سنكوّن Cloud Shell، ونستخدم وحدة Azure PowerShell لإنشاء مجموعة موارد وجهاز ظاهري ومراجعة توصيات Azure Advisor. 

# <a name="task-1-configure-the-cloud-shell"></a>المهمة 1: تكوين Cloud Shell 

في هذه المهمة، سنكوّن Cloud Shell. 

1. سجل الدخول إلى [مدخل Azure](https://portal.azure.com).** يمكنك العثور على بيانات اعتماد تسجيل الدخول الخاصة بك ضمن علامة التبويب resources (بجوار علامة التبويب Instructions هذه مباشرة!) **
2. من مدخل Azure، افتح **Azure Cloud Shell** بالنقر فوق الأيقونة الموجودة في الجزء العلوي الأيمن من مدخل Azure.

    ![لقطة شاشة لأيقونة Azure Cloud Shell في مدخل Azure.](../images/1002.png)

3. عندما يُطلب منك تحديد إما **Bash** أو **PowerShell**، حدد **PowerShell**.

4. في شاشة **ليس لديك مساحة تخزين مثبتة**، حدد **إظهار الإعدادات المتقدمة**، ثم املأ المعلومات أدناه

    | الإعدادات | القيم |
    |  -- | -- |
    | مجموعة الموارد | **إنشاء مجموعة موارد جديدة** |
    | حساب التخزين (إنشاء حساب جديد واستخدام اسم فريد عالميًا (على سبيل المثال: cloudshellstoragemystorage)) | **cloudshellxxxxxxx** |
    | مشاركة ملف (إنشاء جديد) | **shellstorage** |

5. حدد **إنشاء تخزين**

# <a name="task-2-create-a-resource-group-and-virtual-machine"></a>المهمة 2: إنشاء مجموعة موارد وجهاز ظاهري

في هذه المهمة، سنستخدم PowerShell لإنشاء مجموعة موارد وجهاز ظاهري.  

1. تأكد من تحديد **PowerShell** في القائمة المنسدلة العلوية اليسرى من جزء Cloud Shell.

2. تحقق من مجموعة الموارد الجديدة الخاصة بك عن طريق تشغيل الأمر التالي في نافذة Powershell. اضغط على **Enter** لتشغيل الأمر.

    ```PowerShell
    Get-AzResourceGroup | Format-Table
    ```

3. أنشئ جهازًا ظاهريًا عن طريق لصق الأمر التالي في النافذة الطرفية. 

    ```PowerShell
    New-AzVm `
    -ResourceGroupName "myRGPS" `
    -Name "myVMPS" `
    -Location "East US" `
    -VirtualNetworkName "myVnetPS" `
    -SubnetName "mySubnetPS" `
    -SecurityGroupName "myNSGPS" `
    -PublicIpAddressName "myPublicIpPS"
    ```
    
4. عندما يُطلب منك ذلك، قدّم اسم المستخدم (**azureuser** وكلمة المرور **Pa$$w0rd1234**) التي سيتم تكوينها كحساب المسؤول المحلي على تلك machines.azureadmin الظاهرية

5. بمجرد إنشاء الجهاز الظاهري، أغلق جزء جلسة Cloud Shell في جلسة PowerShell.

6. في مدخل Azure، ابحث عن **الأجهزة الظاهرية** وتحقق من تشغيل **myVMPS**. قد يستغرق ذلك بضع دقائق.

    ![لقطة شاشة لصفحة الأجهزة الظاهرية مع وجود myVMPS في حالة تشغيل.](../images/1001.png)

7. قم بالوصول إلى الجهاز الظاهري الجديد وراجع النظرة العامة وإعدادات الشبكات للتحقق من توزيع معلوماتك بشكلٍ صحيح. 

# <a name="task-3-execute-commands-in-the-cloud-shell"></a>المهمة 3: تنفيذ الأوامر في Cloud Shell

في هذه المهمة، سنتدرب على تنفيذ أوامر PowerShell من Cloud Shell. 

1. من مدخل Azure، افتح **Azure Cloud Shell** بالنقر فوق الأيقونة الموجودة في الجزء العلوي الأيمن من مدخل Azure.

2. تأكد من تحديد **PowerShell** في القائمة المنسدلة العلوية اليسرى من جزء Cloud Shell.

3. استرد معلومات عن جهازك الظاهري بما في ذلك الاسم ومجموعة الموارد والموقع والحالة. لاحظ أن PowerState **قيد التشغيل**.

    ```PowerShell
    Get-AzVM -name myVMPS -status | Format-Table -autosize
    ```

4. أوقف الجهاز الافتراضي باستخدام الأمر التالي. 

    ```PowerShell
    Stop-AzVM -ResourceGroupName myRGPS -Name myVMPS
    ```
5. عندما يُطلب منك تأكيد (نعم) على الإجراء. انتظر حالة **تم بنجاح**.

6. تحقق من حالة جهازك الظاهري. ينبغي الآن إلغاء تخصيص **PowerState**. يمكنك أيضًا التحقق من حالة الجهاز الظاهري في المدخل. أغلق Cloudshell.

    ```PowerShell
    Get-AzVM -name myVMPS -status | Format-Table -autosize
    ```

# <a name="task-4-review-azure-advisor-recommendations"></a>المهمة 4: راجع توصيات Azure Advisor

**ملاحظة:** هذه المهمة نفسها موجودة في معمل إنشاء جهاز ظاهري باستخدام Azure CLI. 

في هذه المهمة، سنراجع توصيات Azure Advisor لجهازنا الظاهري. 

1. من نافذة **جميع الخدمات**، ابحث عن **Advisor** وحدده. 

2. في نافذة **Advisor**، حدد **نظرة عامة**. يتم تجميع توصيات الإعلامات حسب Reliability وSecurity وPerformance وCost. 

    ![لقطة شاشة لصفحة نظرة عامة على Advisor. ](../images/1003.png)

3. حدد **جميع التوصيات** استغرق الوقت الكافي لعرض كل توصية والإجراءات المقترحة. 

    **ملاحظة:** اعتمادًا على مواردك، ستكون توصياتك مختلفة. 

    ![لقطة شاشة لصفحة جميع التوصيات في Advisor. ](../images/1004.png)

4. لاحظ أنه يمكنك تنزيل التوصيات كملف بتنسيق CSV أو PDF. 

5. لاحظ أنه يمكنك إنشاء تنبيهات. 

6. إذا كان لديك الوقت الكافي، فاستمر في تجربة Azure PowerShell. 

تهانينا! لقد كوّنت Cloud Shell وأنشأتَ جهاز ظاهري باستخدام PowerShell وتدربتَ على أوامر PowerShell واستعرضتَ توصيات Advisor.

**ملاحظة**: لتجنب التكاليف الإضافية، يمكنك اختياريًا إزالة مجموعة الموارد هذه. ابحث عن مجموعات الموارد، وانقر فوق مجموعة الموارد الخاصة بك، ثم انقر فوق **حذف مجموعة الموارد**. تحقق من اسم مجموعة الموارد ثم انقر فوق **حذف**. راقب **الإعلامات** لترى كيف تجري عملية الحذف.
