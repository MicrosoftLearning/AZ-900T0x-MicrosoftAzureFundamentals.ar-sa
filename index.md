---
title: تعليمات مستضافة عبر الإنترنت
permalink: index.html
layout: home
ms.openlocfilehash: c8816b7d9de9c19fbd4c6b3f373d6e4336c6ca5a
ms.sourcegitcommit: 26c283fffdd08057fdce65fa29de218fff21c7d0
ms.translationtype: HT
ms.contentlocale: ar-SA
ms.lasthandoff: 01/27/2022
ms.locfileid: "137907297"
---
# <a name="content-directory"></a>دليل المحتوى

ارتباطات تشعبية لكل معاينة من المعاينات. قد يختار المعلمون استخدام المعاينة كعرض توضيحي أو معمل للطلاب. 

## <a name="walkthroughs"></a>تجول

{% assign wts = site.pages | where_exp:"page", "page.url contains '/Instructions/Walkthroughs'" %}
| الوحدة النمطية | معاينة |
| --- | --- | 
{% for activity in wts %}| {{ activity.wts.module }} | [{{ activity.wts.title }}{% if activity.wts.type %} - {{ activity.wts.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}

