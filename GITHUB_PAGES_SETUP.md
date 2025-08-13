# 🚀 دليل إعداد GitHub Pages

دليل شامل لنشر مشروع قوالب السير الذاتية على GitHub Pages خطوة بخطوة.

## 📋 المتطلبات الأساسية

- حساب GitHub نشط
- مستودع GitHub (Repository) 
- ملفات المشروع جاهزة للرفع

## 🔧 الطريقة الأولى: الإعداد من واجهة GitHub

### الخطوة 1: إنشاء مستودع جديد

1. **اذهب إلى GitHub.com** وسجل الدخول
2. **انقر على "New Repository"** أو الزر الأخضر "+"
3. **اختر اسم المستودع**:
   ```
   cv-templates
   ```
   أو أي اسم تفضله
4. **اجعل المستودع عام (Public)** - مطلوب لـ GitHub Pages المجاني
5. **أضف وصف**:
   ```
   مجموعة قوالب السير الذاتية الاحترافية للمجالات المهنية المختلفة
   ```
6. **انقر "Create Repository"**

### الخطوة 2: رفع ملفات المشروع

#### الطريقة أ: رفع مباشر من الواجهة
1. **انقر "uploading an existing file"**
2. **اسحب مجلد المشروع كاملاً** أو انقر "choose your files"
3. **تأكد من رفع**:
   - مجلد `docs/` بالكامل
   - مجلد `word_templates/`
   - جميع ملفات `.md`
   - ملف `LICENSE`
4. **اكتب رسالة commit**:
   ```
   إضافة قوالب السير الذاتية الاحترافية
   ```
5. **انقر "Commit changes"**

#### الطريقة ب: استخدام Git
```bash
# استنساخ المستودع الفارغ
git clone https://github.com/your-username/cv-templates.git
cd cv-templates

# نسخ ملفات المشروع
cp -r /path/to/cv_templates_github_pages/* .

# إضافة الملفات
git add .
git commit -m "إضافة قوالب السير الذاتية الاحترافية"
git push origin main
```

### الخطوة 3: تفعيل GitHub Pages

1. **اذهب إلى إعدادات المستودع**:
   - انقر على تبويب "Settings" في أعلى الصفحة
   
2. **انتقل إلى قسم Pages**:
   - في القائمة الجانبية، انقر على "Pages"
   
3. **اختر مصدر النشر**:
   - **Source**: اختر "Deploy from a branch"
   - **Branch**: اختر "main" (أو "master" إذا كان هو الافتراضي)
   - **Folder**: اختر "/docs" - **هذا مهم جداً!**
   
4. **احفظ الإعدادات**:
   - انقر "Save"
   
5. **انتظر النشر**:
   - سيظهر رابط أخضر مثل: `https://your-username.github.io/cv-templates/`
   - قد يستغرق 5-10 دقائق للنشر الأول

### الخطوة 4: التحقق من النشر

1. **افتح الرابط** الذي ظهر في إعدادات Pages
2. **يجب أن ترى**:
   - صفحة الفهرس الجميلة مع جميع القوالب
   - إحصائيات المشروع
   - بطاقات القوالب مع أزرار المعاينة والتحميل
3. **اختبر الروابط**:
   - انقر على "معاينة مباشرة" لأي قالب
   - تأكد من ظهور القالب بشكل صحيح

## 🔧 الطريقة الثانية: GitHub Actions (متقدم)

### إنشاء ملف Workflow

إنشئ ملف `.github/workflows/pages.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v3
      
    - name: Setup Pages
      uses: actions/configure-pages@v2
      
    - name: Upload artifact
      uses: actions/upload-pages-artifact@v1
      with:
        path: './docs'
        
    - name: Deploy to GitHub Pages
      id: deployment
      uses: actions/deploy-pages@v1

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true
```

### تفعيل GitHub Actions

1. **اذهب إلى Settings > Pages**
2. **اختر Source**: "GitHub Actions"
3. **احفظ الإعدادات**

## 🎯 نصائح مهمة

### ✅ تأكد من هذه النقاط

1. **مجلد docs**:
   - يجب أن يحتوي على `index.html` في الجذر
   - مجلد `templates/` يحتوي على جميع قوالب HTML
   
2. **الروابط النسبية**:
   - تأكد من أن جميع الروابط في `index.html` تستخدم مسارات نسبية
   - مثال: `templates/tech_template.html` وليس `/templates/tech_template.html`
   
3. **أسماء الملفات**:
   - تجنب المسافات والأحرف الخاصة
   - استخدم الشرطة السفلية `_` أو الشرطة العادية `-`

### ❌ أخطاء شائعة

1. **اختيار مجلد خاطئ**:
   - إذا اخترت "/ (root)" بدلاً من "/docs"، ستظهر صفحة README
   
2. **ملف index.html مفقود**:
   - يجب وجود `docs/index.html` وليس `index.html` في الجذر
   
3. **المستودع خاص**:
   - GitHub Pages المجاني يتطلب مستودع عام

## 🔧 استكشاف الأخطاء

### المشكلة: تظهر صفحة README بدلاً من الموقع

**الحل**:
1. تأكد من اختيار "/docs" في إعدادات Pages
2. تأكد من وجود `docs/index.html`
3. انتظر 5-10 دقائق للتحديث

### المشكلة: الروابط لا تعمل (404)

**الحل**:
1. تحقق من أسماء الملفات في مجلد `templates/`
2. تأكد من أن الروابط في `index.html` صحيحة
3. تأكد من عدم وجود مسافات في أسماء الملفات

### المشكلة: التصميم لا يظهر

**الحل**:
1. تحقق من أن CSS مضمن في ملفات HTML
2. تأكد من عدم وجود روابط خارجية مكسورة
3. افتح أدوات المطور في المتصفح للتحقق من الأخطاء

## 📱 تخصيص الدومين (اختياري)

### استخدام دومين مخصص

1. **اشتر دومين** من أي مزود (GoDaddy, Namecheap, إلخ)
2. **أضف ملف CNAME** في مجلد `docs/`:
   ```
   your-domain.com
   ```
3. **في إعدادات DNS** للدومين، أضف:
   ```
   CNAME: your-username.github.io
   ```
4. **في GitHub Pages Settings**:
   - أضف الدومين المخصص
   - فعل "Enforce HTTPS"

## 🚀 تحسين الأداء

### تحسين سرعة التحميل

1. **ضغط الصور**:
   ```bash
   # استخدم أدوات ضغط الصور
   imageoptim *.png
   ```

2. **تصغير CSS**:
   ```bash
   # استخدم أدوات تصغير CSS
   cleancss -o style.min.css style.css
   ```

3. **تفعيل التخزين المؤقت**:
   ```html
   <!-- أضف في <head> -->
   <meta http-equiv="Cache-Control" content="max-age=31536000">
   ```

### تحسين SEO

1. **أضف meta tags**:
   ```html
   <meta name="description" content="قوالب سير ذاتية احترافية">
   <meta name="keywords" content="سيرة ذاتية, قوالب, CV, Resume">
   <meta property="og:title" content="قوالب السير الذاتية">
   <meta property="og:description" content="مجموعة شاملة من القوالب">
   <meta property="og:image" content="preview.png">
   ```

2. **أضف ملف sitemap.xml**:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
     <url>
       <loc>https://your-username.github.io/cv-templates/</loc>
       <changefreq>weekly</changefreq>
       <priority>1.0</priority>
     </url>
   </urlset>
   ```

## 📊 تتبع الزوار (اختياري)

### Google Analytics

1. **أنشئ حساب Google Analytics**
2. **أضف الكود في جميع صفحات HTML**:
   ```html
   <!-- Google Analytics -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'GA_TRACKING_ID');
   </script>
   ```

## 🔄 التحديثات المستقبلية

### إضافة قوالب جديدة

1. **أضف ملف HTML جديد** في `docs/templates/`
2. **حدث `docs/index.html`** لإضافة بطاقة القالب الجديد
3. **ارفع التغييرات**:
   ```bash
   git add .
   git commit -m "إضافة قالب جديد: [اسم المجال]"
   git push origin main
   ```

### تحديث التصميم

1. **عدل ملفات HTML/CSS**
2. **اختبر محلياً** قبل الرفع
3. **ارفع التحديثات**

## 📞 الدعم والمساعدة

### مصادر مفيدة

- **[وثائق GitHub Pages الرسمية](https://docs.github.com/en/pages)**
- **[دليل GitHub Actions](https://docs.github.com/en/actions)**
- **[مجتمع GitHub](https://github.community/)**

### حل المشاكل

إذا واجهت أي مشاكل:

1. **تحقق من Status Page**: https://www.githubstatus.com/
2. **ابحث في GitHub Community**
3. **افتح Issue في المستودع**
4. **راسلنا على**: support@cv-templates.com

---

**🎉 تهانينا! موقعك الآن منشور ومتاح للعالم!**

**🔗 لا تنس مشاركة الرابط مع أصدقائك وعملائك!**

