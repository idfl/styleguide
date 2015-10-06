# Official IDFL Styleguide
Official IDFL code style guide. Contains basic project/app structure and general code styles that should be followed when developing for IDFL.

## Table of Contents

  1. [Django](#django)
  1. [AngularJS 1.x](#angularjs-1x)
  1. [Frontend Styling](#frontend-styling)
  1. [Resources](#resources)

## Django

### Django REST
All apps should utilize the Django REST framework to handle their API. See the [Django REST API](http://www.django-rest-framework.org/#api-guide) for features and implementation details.

### Class-Based Views
All views in Django should be written as classes following the [Class-based views](https://docs.djangoproject.com/en/1.8/topics/class-based-views/) structure.

### Project Structure
```
/Project
    /App
        /migrations
        /static
            /App
                /js
                    /module
                      module.controller.js
                      module.factory.js
                      module.service.js
                /scss
                    /module
                        _style.scss
                        _style.scss
                    base.scss
                    
        /templates
            /App
                /directives
                    example.directive.html
                    example.directive.html
                /partials
                    example.partial.html
                index.html
        /views
            view.py
        /permissions
            permission.py
        /serializers
            serializer.py
        /urls
            urls.py
```

#### URL Structure

* Each app should use `.../app/api/...` as the root url for RESTful API.
* Each app should use `../app/templates/...` as the root url for all templates/partials.


**[Back to top](#table-of-contents)**



## AngularJS 1.x

All AngularJS code should follow the basics outlined in the John Papa style guide. The complete AngularJS guide can be found [here](https://github.com/idfl/idfl-styleguide/tree/master/angular-1.x).
For basic implementation examples, see the [code snippets](https://github.com/idfl/idfl-styleguide/blob/master/angular-1.x/snippets.md).

**[Back to top](#table-of-contents)**


## Frontend Styling

### Bootstrap 3
We use Bootstrap 3 for the basic styling of all applications. See the [Bootstrap docs](http://getbootstrap.com/) for more details on implementation.

### FontAwesome
We use FontAwesome for all icons. See [FontAwesome](http://fontawesome.io/) docs for list of all available icons.

### SCSS
All custom project and app specific styling should be written and compiled using SCSS. We use the new SCSS over the original SASS syntax. See the [Sass Basics](http://sass-lang.com/guide) for basic API details.

**[Back to top](#table-of-contents)**


## Resources

* [AngularJS Tutorial](https://docs.angularjs.org/tutorial)
* [AngularJS API](https://docs.angularjs.org/api)
* [Django REST tutorial](http://www.django-rest-framework.org/#tutorial)
* [Django REST API](http://www.django-rest-framework.org/#api-guide)
* [Bootstrap 3 docs](http://getbootstrap.com/)
* [Font Awesome Icons](http://fontawesome.io/)
* [SCSS](http://sass-lang.com/guide)

**[Back to top](#table-of-contents)**
