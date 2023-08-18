- Run `rails g scaffold Kind description:string`, this generate crud to Kind and include field `description:string`

- Run the command to execute migrations: `rails g migration add_kind_to_contact kind:references`

- Go to `db => migrate` and view your migrations

- Run `rails db:migrate` to execute new migration on database

- To generate fake infos, go to `lib => tasks => dev.rake` and insert the creation of kinds. Example:

```ruby
namespace :dev do
  desc "Configure to development environment data mocks"
  task setup: :environment do
  # HERE
    puts "Creating type contacts..."
    kinds = %w(Amigo Colega Comercial)
    kinds.each do |kind|
      Kind.create!(description: kind)
    end
    puts "type contacts created successfully!"

    puts "Creating fake contacts..."
    # This generate 100 items
    100.times do |i|
      Contact.create!(
        name: Faker::Name.name,
        email: Faker::Internet.email,
        birthdate: Faker::Date.birthday(min_age: 18, max_age: 65),
        kind: Kind.all.sample

      )
    end
    puts "fake contacts created successfully!"


  end
end

```

- Go to `models => contact.rb` and insert the relationship. Example:

```ruby
class Contact < ApplicationRecord
  belongs_to :kind

  def author
    "Lucca Rodrigues"
  end

  def as_json(options={})
    super(methods: :author)
  end
end

```

- Run `rails db:drop db:create db:migrate` to recreate database with new data

- Run `dev:setup` to re-generate fake data
