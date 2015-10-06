# Official IDFL Styleguide
Official IDFL code style guide. Contains basic project/app structure and general code styles that should be followed when developing for IDFL.

## Table of Contents

  1. [Django](#django)
  1. [AngularJS 1.x](#angularjs-1x)
  1. [Frontend Styling](#frontend-styling)
  1. [General](#general)
  1. [Workflow](#workflow)
  1. [Pro Tips](#pro-tips)
  1. [Resources](#resources)

## Django

In general, we follow the PEP 0008 style guide for all Python code, with a few modifications for clarity and to promote consistency. See the [IDFL PEP 0008 style guide](https://github.com/idfl/styleguide/blob/master/pep-0008.md) for full details.

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
All custom project and app specific styling should be written and compiled using SCSS. We use the new SCSS over the original SASS syntax. See the [Sass Basics](http://sass-lang.com/guide) for basic API details. The following Sass styling tips are based on the Sass Style Guide at [css-tricks.com](https://css-tricks.com/sass-style-guide/).

#### Order of Styles
  - @extend(s)
  - @include(s)
  - "Regular" Styles
  - Nested Pseudo Classes
  - Nested Pseudo Elements
  - Nested Selectors
  
##### Example
```
.weather {
  @extend %module; 
  @include transition(all 0.3s ease);
  background: LightCyan;
  &:hover {
    background: DarkCyan;
  }
  &::before {
    content: "";
    display: block;
  }
  > h3 {
    @include transform(rotate(90deg));
    border-bottom: 1px solid white;
  }
}
```

#### Never Write Vendor Prefixes
Vendor prefixes are a time-sensitive thing. As browsers update over time, the need for them will fall away. If you use [Autoprefixer](https://css-tricks.com/autoprefixer/), when compiling Sass, then you should never have to write them.

#### Maximum Nesting: Three Levels Deep
```
.weather {
  .cities {
    li {
      // no more!
    }
  }
}
```
Chances are, if you're deeper than that, you're writing a crappy selector. Crappy in that it's too reliant on HTML structure (fragile), overly specific (too powerful), and not very reusable (not useful). It's also on the edge of being difficult to understand.

If you really want to use tag selectors because the class thing is getting too much for you, you may want to get pretty specific about it to avoid undesired cascading. And possibly even make use of @extend so it has the benefit on the CSS side of re-usability.

#### Maximum Nesting: 50 Lines
If a nested block of Sass is longer than that, there is a good chance it doesn't fit on one code editor screen, and starts becoming difficult to understand. The whole point of nesting is convenience and to assist in mental grouping. Don't use it if it hurts that.

#### Global and Root SCSS Files are just Table of Contents
All styles should be defined in Sass partials, the base Sass file should just import all these partials.
```
/* Vendor Dependencies */
@import "compass";

/* Authored Dependencies */
@import "global/colors";
@import "global/mixins";

/* Patterns */
@import "global/tabs";
@import "global/modals";

/* Sections */
@import "global/header";
@import "global/footer";
```

#### Many Files is Better than One File
Each element/component should have its own file or folder. Each partial
should have one specific purpose.
```
--- global.scss ---
@import "global/header/";

--- _header.scss ---
@import "global/header/logo/";
@import "global/header/dropdowns/";
@import "global/header/nav/";
@import "global/header/really-specific-thingy/";
```
 ##### Basic Project Structure
```
/scss
    app.base.scss
    /variables
        _variables.scss
        _variables.scss
    /mixins
        _mixins.scss
        _mixins.scss
    /component1
        _component.scss
        _component.scss
    /component2
        _component.scss
        _component.scss
    ...
```

#### Partials are named `_partial.scss`
This is a common naming convention that indicates this file isn't meant to be compiled by itself. It likely has dependencies that would make it impossible to compile by itself. Personally I like dashes in the "actual" filename though, like _dropdown-menu.scss.

#### Variablize All Common Numbers, and Numbers with Meaning
If you find yourself using a number other than 0 or 100% over and over, it likely deserves a variable. Since it likely has meaning and controls consistency, being able to tweak it en masse may be useful.

#### Variablize All Colors
Except perhaps white and black. Chances are a color isn't one-off, and even if you think it is, once it's in a variable you might see uses for it elsewhere. Variations on that color can often be handled by the Sass color functions like lighten() and darken() - which make updating colors easier (change in one place, whole color scheme updates).

#### Nest and Name Your Media Queries
The ability to nest media queries in Sass means 1) you don't have to re-write the selector somewhere else which can be error prone 2) the rules that you are overriding are very clear and obvious, which is usually not the case when they are at the bottom of your CSS or in a different file.

**[Back to top](#table-of-contents)**

## General
This section contains general rules of thumb. Unless explicitly stated, they apply in a general sense to any and all language used at IDFL.

### Variable Names
In general, follow the naming conventions as specified by the specific language you are working in. Be specific in variable names, others should be able to immediately know what they represent. Avoid unnecessary abbreviations when possible. All variables must be more than 1 character long, except when used as an iterator. 

```
  Good:
      username = 'fariz.idfl'
      name = 'Fariz'
      
  Bad:
      usrnm = 'fariz.idfl'
      nm = 'Fariz'
      c = 42
```

**[Back to top](#table-of-contents)**

## Workflow
This is the suggested workflow for adding code to the IDFL code base. 
  1. Pick a task.
  2. Start a new branch
      ```
      git checkout -b new-branch-name
      ```
  3. Do Work.
  4. Open Pull Request through GitHub.
  5. Merge branch with staging and push to development server.
      ```
      git checkout stage
      git merge new-branch-name
      git push
      ```
  5. Ask team member for a code review and QA check.
  6. Merge Pull Request with master.
  7. Delete development branch.
  8. ?????
  9. Profit.
  
### Issue Tracking
Track all sprint tasks through Trello boards. Specific commits and bug fixes that contain important contextual information should have a GitHub issue attached to them.

##### Example Information for GitHub Issues
  - Who requested bug/feature.
  - Date requested.
  - Email exchange containing bug/feature request.
  - etc.

All commit messages should be meaningful, or link to a specific GitHub issue that contains more details.

Commit, and commit often.

## Pro Tips
This section will contain any and all useful functions/techniques that we wish someone had told us about when starting out.

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
