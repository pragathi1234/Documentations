### Building a website using Django

1. Create a project
2. Create an application
3. Plan the project
4. Add URLs in both project and application level
5. Add views in application level folder
6. Adding templates (html)
7. Add project level template path in settings.py in DIRS
8. To add application level templates, specify app name in INSTALLED_APPS in settings.py file
9. To add css files, create a static folder in both project and application level
10. Register global level css files in settings.py

STATICFILES_DIRS = [

    BASE_DIR / "static"
]
11. Images are also considered as static files, Create an folder called images and paste all images

### Adding Models to blog

