# Sprockets in Sinatra

1. Download the [gitdocs gem](https://rubygems.org/gems/gitdocs)
```
git clone https://github.com/nesquena/gitdocs.git
cd gitdocs
bundle install
bundle exec rake server:copy_config
bundle exec rake server
```

2. Browse to [http://127.0.0.1:9393/] to see the interface.

3. Add [sinatra-asset-pipeline](https://rubygems.org/gems/sinatra-asset-pipeline) to **gitdocs.gemspec**.
```
  s.add_dependency 'sinatra-asset-pipeline', '~> 0.7.0'
```
  - comment out rake dependency
  - comment out tilt dependency
  - comment out "require 'tile/redcarpet' from lib/gitdocs/rendering_helper.rb

4. Install again
```
bundle install
```

5. 
