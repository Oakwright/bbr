If you need to flush your DNS cache so you can test domains, on ubuntu run:
    
    resolvectl flush-caches

If you are installing stuff for an older version of python, you may need to add deadsnakes:

    sudo add-apt-repository ppa:deadsnakes/ppa

Create environment, this may not be optimal! I'm running python 3.8 for this project

    conda create -n cond38 python=3.8.13
    conda activate cond38
    python --version
    which python

Things to try:

    conda install -c conda-forge uwsgi
    mkvirtualenv -p /home/apossum/anaconda3/envs/cond38/bin/python bbr38
    apt-get install build-essential python3.6-dev
    https://anaconda.org/conda-forge/uwsgi

pip install uwsgi
    
    conda activate cond38
    workon bbr38
    pip install uwsgi
    cd repos/bbr/bbrsite/
    pip install -r requirements.txt
    

Create bbrsite.conf file
    
    sudo touch bbrsite.conf
    sudo nano bbrsite.conf

Set up uwsgi params

    cd /home/apossum/repos/bbr/bbrsite
    touch uwsgi_params

To set an available site to enabled, create a symlink in the sites-enabled directory that 
points to the conf file in sites-available

    sudo ln -s /etc/nginx/sites-available/bbrsite.conf /etc/nginx/sites-enabled/

To set an active site to inactive, delete it's symlink in /etc/nginx/sites-enabled/

    sudo rm /etc/nginx/sites-enabled/default

To edit bbrsite conf file for nginx:

    sudo nano /etc/nginx/sites-available/bbrsite.conf

Restart nginx:

    sudo /etc/init.d/nginx restart

To see command line history:

    history

If it keeps giving Bad Gateway and Forbidden errors, it might be because nginx is running under a user that doesn't
have permissions, or under a non-existent user. 
https://stackoverflow.com/questions/21820444/nginx-error-13-permission-denied-while-connecting-to-upstream
As a hack, you can add an actual user to the conf file and thus give
the service all of the same permissionsn as the user:

    cd /etc/nginx
    sudo nano nginx.conf

To run uwsgi so so that nginx can grab it's socket:

    uwsgi --socket bbrsite.sock --module bbrsite.wsgi --chmod-socket=666

To run uwsgi on a specific port:

    uwsgi --http :8001 --module bbrsite.wsgi

nginx logs:

    /var/log/nginx/

https://uwsgi-docs.readthedocs.io/en/latest/Install.html
https://tonyteaches.tech/django-nginx-uwsgi-tutorial/
https://www.youtube.com/watch?v=ZpR1W-NWnp4

To run uwsgi as daemon using ini file:

    uwsgi --ini bbrsite_uwsgi.ini

    ps aux