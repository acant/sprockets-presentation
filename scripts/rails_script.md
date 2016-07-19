# Sprockets in rails walk-through

1. Start a new application:
```
gem install rails
rails new example
cd example
bundle install
bundle exec rails s
```

2. Browse to [http://localhost:3000].

3. Review initial assets related paths:
```
ls
find app/assets
find vendor/assets
cat app/assets/config/manifest.js
cat app/assets/javascript/applications.js
cat app/assets/stylesheets/application.css
```

4. Add a simple page:
```
bundle exec rails generate controller Home index
cat app/views/home/index.html.erb
cat app/assets/javascripts/home.coffee
cat app/assets/stylesheets/home.scss
```

% Ignoring the other files for the presentation, because we are only worried about assets
% mention coffeescript and scss, as the current rails defaults

6. browse to [http://localhost:3000/home/index]

7. Add some other tags to the app/views/home/index.html.erb and refresh:
```
<p>Where is the pipline?</p>
```

8. Add some images to the page:
```
cp ../../assets/images/*.jpg app/assets/images
```

9. Add images to the app/views/home/index.html.erb:
```
<div class="pictures">
  <%= image_tag('under.jpg', class: 'under', alt: 'Under a pipe') %>
</div>
```

10. Add some colour to app/assets/stylesheets/home.scss:
```
h1 { border-bottom: thick dotted #ff0000 }
```

11. Add an image to app/assets/stylesheets/home.scss:
```
.pictures { background-image: url(<%= asset_path 'trees.jpg' %>) top right /200px no-repeat }
```

12. Derp! That raises an error because it needs to be an ERB template:
```
mv app/assets/stylesheets/home.scss app/assets/stylesheets/home.scss.erb
```

13. Want to do the same thing with Javascript? Convert to an ERB template:
```
mv app/assets/javascripts/home.coffee app/assets/javascripts/home.coffee.erb
```

14. Then add some images through Javascript, app/assets/javascripts/home.coffee.erb:
```
$ ->
  $(".pictures").append("<img src=\"<%= asset_path('water.jpg') %>\">")
```

14. Lets add an asset! [fullcalendar-rails](https://github.com/bokmann/fullcalendar-rails)
  - add to Gemfile
    ```
    gem 'fullcalendar-rails'
    gem 'momentjs-rails'
    ```
  - add to app/assets/javascripts/application.js
    ```
    //= require moment
    //= require fullcalendar
    ```
  - add to app/assets/stylesheets/application.css
    ```
    *= require fullcalendar
    ```
  - add to app/views/home/index.html.erb
    ```
    <div id="calendar"></div>
    ```
  - add to app/assets/javascripts/home.coffee.erb
    ```
      $("#calendar").fullCalendar({})
    ```

15. Install and restart, to re-load the gems
```
bundle install
bundle exec rails server
```

16. Lets add the bourbon asset gem...
  - but first convert to use SCSS in our application stylesheet to allow
    SCSS '@import' instead of sprockets require
  - https://blog.pivotal.io/pivotal-labs/labs/structure-your-sass-files-with-import

  - rename the style sheet
    ```
    app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
    ```
  - add to app/assets/stylesheets/application.scss
    ```
    @import "home";
    ```
  - remove the **require_tree** directive app/assets/stylesheets/application.scss


17. Add bourbon
  - add to the Gemfile
    ```
    gem 'bourbon'
    ```
  - add to app/assets/stylesheets/application.scss
    ```
    @import "bourbon"; # make sure it come before everything else
    ```
  - install and restart the server
    ```
    bundle install
    bundle exec rails server
    ```

18. And add some simple bourbon styling to app/assets/stylesheets/home.scss.erb
```
p { @include linear-gradient(to left, red, orange) }
```

19. Lets look at the asset gems

```
gem contents fullcalendar
gem contents bourbon
```

20. Test production
```
RAILS_ENV=production bundle exec rails assets:precompile
RAILS_ENV=production bundle exec rails server
```
