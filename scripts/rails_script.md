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
7. Add some other tags to the HTML:
```
echo "<p>Where is the pipline?</p>" >> app/views/home/index.html.erb
```
8. Refresh browser
9. Add some images to the page:
```
cp ../../assets/images/*.jpg app/assets/images
```

10. Add images to the HTML and refresh:
```
echo '<div class="pictures">'
echo "  <%= image_tag('under.jpg', class: 'under', alt: 'Under a pipe') %>" >> app/views/home/index.html.erb
echo "</div>"
```

12. Add come colour:
```
echo "h1 { border-bottom: thick dotted #ff0000 }" >> app/assets/stylesheets/home.scss
```

11. Add an image in the SCSS
```
echo ".pictures { background-image: url(<%= asset_path 'trees.jpg' %>) top right /200px no-repeat }" >> app/assets/stylesheets/home.scss
```

12. Derp! That raise an error needs to use an ERB template as well:
```
mv app/assets/stylesheets/home.scss app/assets/stylesheets/home.scss.erb
```

13. Want to do the same thing with Javascript?
```
app/assets/javascripts/home.coffee app/assets/javascripts/home.coffee.erb
echo '$ ->' >> app/assets/javascripts/home.coffee.erb
echo '$(".pictures").append("<img src=\"<%= asset_path('water.jpg') %>\">")' >> app/assets/javascripts/home.coffee.erb
```

14. Lets add a javascript gem! [fullcalendar-rails](https://github.com/bokmann/fullcalendar-rails)
```
echo "gem 'fullcalendar-rails'" >> Gemfile
echo "gem 'momentjs-rails'" >> Gemfile
bundle install
# restart the server to load the gems
echo "//= require moment" >> app/assets/javascripts/application.js
echo "//= require fullcalendar" >> app/assets/javascripts/application.js
# add to "*= require fullcalendar" to app/assets/stylesheets/application.css
echo '<div id="calendar"></div>' >> app/views/home/index.html.erb
echo '  $("#calendar").fullCalendar({})' >> app/assets/javascripts/home.coffee.erb
```

13. Lets add the bourbon asset gem...

14. But first convert to use '@import' instead of require...

```
mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
echo '@import "home";' >> app/assets/stylesheets/application.scss
# remove the require_tree directive
```

https://blog.pivotal.io/pivotal-labs/labs/structure-your-sass-files-with-import

15. back to the bourbon

```
echo "gem 'bourbon'" >> Gemfile
bundle install
# add '@import "bourbon";' before the home import

```

16. And add some bourbon styling
```
echo 'p { @include linear-gradient(to left, red, orange) }' >> app/assets/stylesheets/home.scss.erb
```

17. Lets look at the asset gems

```
gem contents fullcalendar
gem contents bourbon
```

