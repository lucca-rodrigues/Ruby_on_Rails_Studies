- Go to Gemfile and insert faker lib:

```
group :development, :test do
  # See https://guides.rubyonrails.org/debugging_rails_applications.html#debugging-with-the-debug-gem
  gem "debug", platforms: %i[ mri mingw x64_mingw ]

  #Faker helps you generate realistic test data, and populate your database with more than a couple of records while you're doing development.
gem 'faker'
end
```

- Run `eval "$(rbenv init - zsh)"`set the global ruby versions `rbenv global 3.2.2`

- Run `bundle` to updte packages
- Run `rails s -b 0.0.0.0` to restart server and acess `http://localhost:3000`.

## Task generator fake data

- Run `rails g task dev setup` to generate setup data to dev
- This generate the folder `lib => tasks => dev`
- Configure to generate fake data

```
namespace :dev do
  desc "Configure to development environment data mocks"
  task setup: :environment do
    puts "Creating fake contacts..."
    # This generate 100 items
    100.times do |i|
      Contact.create!(
        name: Faker::Name.name,
        email: Faker::Internet.email,
        birthdate: Faker::Date.birthday(min_age: 18, max_age: 65),
      )
    end
    puts "fake contacts created successfully!"
  end
end

```

- Run `rails -T` to view all tasks generated and `rails -T dev` to view your task created
- Run `rails dev:setup` to generate data.
