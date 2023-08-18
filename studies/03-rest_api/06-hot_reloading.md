- To resolve hot reloading problem, go to file `config => environment => development.rb` and add this line:

```ruby
  # Enable hot reloading
  config.file_watcher = ActiveSupport::FileUpdateChecker

```
