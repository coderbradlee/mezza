1. Add moderna to project

That's a simple step.

You should go to site with theme (for moderna it's here ) and download it. It will be a Django App, probably zipped into archive.
If app is zipped, unzip it.
Move it to your Mezzanine project folder (the one, which got created by command mezzanine-project myproject)
Folder structure should become:
myproject/
+-deploy/
+-static/
+-templates/    [in case you chose to collect them]
+-moderna/      [our new theme]
|
+-__init__.py
+-settings.py
+-urls.py
+-manage.py
+-wsgi.py
|
+-[some other things]
2. Change settings.py

open settings.py of your Mezzanine project
add moderna/templates to TEMPLATE_DIRS in settings.py 1st recor. The point is to give new directions to template loaders - now they 1st look for templates in moderna. Should now look like this:
TEMPLATES = (
    os.path.join(PROJECT_ROOT, "moderna/templates"),
    os.path.join(PROJECT_ROOT, "templates"),
)
add moderna app to INSTALLED_APPS in settings.py above all (I presume, that's for Moderna's views, models etc. - backend for templates)
3. New Static Files

collectstatic again - now it will grab moderna's static
4. URLConf

in urls.py, use DIRECT_TO_TEMPLATE selected for / (root url), it should look like this:
urlpatterns += patterns('',
    url("^$", direct_to_template, {"template": "index.html"}, name="home"),
("^", include("mezzanine.urls")),
...
5. Reload

I guess some servers would pick up new settings and urls automatically. Those which don't should be reloaded manually to catch up and start showing your beautiful new theme.

6. Customization begins

Now you can start customizing Moderna theme via base.html and index.html files in myproject/moderna/templates/ folder.

python manage.py collectstatic

运行哪个模板就在最上面
os.path.join(PROJECT_ROOT, "moderna/templates"),
os.path.join(PROJECT_ROOT, "flat/templates"),
os.path.join(PROJECT_ROOT, "nova/templates"),
os.path.join(PROJECT_ROOT, "solid/templates"),

python manage.py runserver 0.0.0.0:80


pip install -U drum
mezzanine-project -a drum bbs
$ cd project_name
$ python manage.py createdb --noinput
$ python manage.py runserver



