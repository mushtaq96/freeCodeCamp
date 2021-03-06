---
title: Git Stash
localeTitle: جيت ستاش
---
## جيت ستاش

تحتوي Git على منطقة تسمى Stash حيث يمكنك تخزين لقطة من التغييرات مؤقتًا دون إلزامها بالمستودع. إنه منفصل عن دليل العمل أو ناحية التدريج أو المستودع.

هذه الوظيفة مفيدة عندما قمت بإجراء تغييرات على فرع لست مستعدًا للالتزام به ، ولكنك تحتاج إلى التبديل إلى فرع آخر.

### خبأ التغييرات

لحفظ تغييراتك في المخبأ ، شغّل الأمر:

 `git stash save "optional message for yourself" 
` 

هذا يحفظ التغييرات الخاصة بك ويعيد دليل العمل إلى ما بدا لأحدث الالتزام. تتوفر التغييرات المحززة من أي فرع في هذا المستودع.

لاحظ أن التغييرات التي ترغب في تخزينها يجب أن تكون على ملفات متتبعة. إذا أنشأت ملفًا جديدًا وحاولت أن تخمد تغييراتك ، فقد تحصل على الخطأ `No local changes to save` .

### عرض التغييرات Stashed

لمعرفة ما يوجد في خبأتك ، شغّل الأمر:

 `git stash list 
` 

يؤدي هذا إلى إرجاع قائمة من اللقطات المحفوظة الخاصة بك بتنسيق الصيغة `stash@{0}: BRANCH-STASHED-CHANGES-ARE-FOR: MESSAGE` . الجزء `stash@{0}` هو اسم المخبأ ، والرقم الموجود في الأقواس المتعرجة ( `{ }` ) هو فهرس ذلك المخبأ. إذا كانت لديك مجموعات تغيير متعددة مخزنة ، فسيكون لكل مجموعة فهرس مختلف.

إذا نسيت التغييرات التي تم إجراؤها في المخبأ ، فيمكنك الاطلاع على ملخص لها باستخدام `git stash show NAME-OF-STASH` . إذا كنت ترغب في رؤية تخطيط تصحيح نمط diff النموذجية (مع + و s الخاص بالتغييرات سطر - بواسطة - خط) ، يمكنك تضمين الخيار `-p` (من أجل التصحيح). إليك مثال على ذلك:

 `git stash show -p stash@{0} 
 
 # Example result: 
 diff --git a/PathToFile/fileA b/PathToFile/fileA 
 index 2417dd9..b2c9092 100644 
 --- a/PathToFile/fileA 
 +++ b/PathToFile/fileA 
 @@ -1,4 +1,4 @@ 
 -What this line looks like on branch 
 +What this line looks like with stashed changes 
` 

### استرداد التغييرات الثابتة

لاسترداد التغييرات خارج المخزن وتطبيقها على الفرع الحالي الذي أنت فيه ، لديك خياران:

1.  `git stash apply STASH-NAME` التغييرات ويترك نسخة في المخبأ
2.  `git stash pop STASH-NAME` يطبق التغييرات ويزيل الملفات من المخبأ

قد يكون هناك تعارضات عند تطبيق التغييرات. يمكنك حل التعارضات المشابهة للدمج ( [راجع دمج Git للحصول على التفاصيل](https://guide.freecodecamp.org/git/git-merge/) ).

### حذف التغييرات الثابتة

إذا كنت تريد إزالة التغييرات المظللة دون تطبيقها ، فقم بتشغيل الأمر:

 `git stash drop STASH-NAME 
` 

لمسح المخبأ بالكامل ، قم بتشغيل الأمر:

 `git stash clear 
` 

### معلومات اكثر:

*   الأمر `git merge` : [fCC Guide](https://guide.freecodecamp.org/git/git-merge/)
*   وثائق جيت: [خبأ](https://git-scm.com/docs/git-stash)