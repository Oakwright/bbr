# bbr

## Install steps

    git switch focus
    git pull
    mkvirtualenv -p 3.8 bbr38


    pip install django==3.2
    pip install wagtail==2.9
    pip install puput

pip freeze

    anyascii==0.3.1
    asgiref==3.5.2
    backports.zoneinfo==0.2.1
    beautifulsoup4==4.9.3
    certifi==2022.6.15
    charset-normalizer==2.1.0
    Django==3.2
    django-colorful==1.3
    django-el-pagination==3.3.0
    django-filter==21.1
    django-modelcluster==5.3
    django-permissionedforms==0.1
    django-social-share==2.3.0
    django-taggit==2.1.0
    django-treebeard==4.5.1
    djangorestframework==3.13.1
    draftjs-exporter==2.1.7
    et-xmlfile==1.1.0
    html5lib==1.1
    idna==3.3
    l18n==2021.3
    openpyxl==3.0.10
    Pillow==9.2.0
    puput==1.1.3
    pytz==2022.2.1
    requests==2.28.1
    six==1.16.0
    soupsieve==2.3.2.post1
    sqlparse==0.4.2
    tablib==3.2.1
    telepath==0.2
    urllib3==1.26.11
    wagtail==2.16.2
    webencodings==0.5.1
    Willow==1.4.1
    xlrd==2.0.1
    XlsxWriter==3.0.3
    xlwt==1.3.0

Install wagtail

    wagtail start bbrsite
    cd bbrsite
    python manage.py migrate
    python manage.py createsuperuser

Add to installedapps in settings/base.py

    'wagtail.contrib.sitemaps',
    'wagtail.contrib.routable_page',
    'django_social_share',
    'puput',
    'colorful',

add to bottom of settings/base.py

    PUPUT_AS_PLUGIN = True

in urls.py add

    from django.conf.urls import url
    from puput import urls as puput_urls
    ...
    url(r'',include(puput_urls)),

run:
    
    python manage.py migrate
