- This is used to multiple infos for one element
- Example: One user has many phone numbers

## How to create?

- Run `rails g model Phone number:string contact:references`

- Go to model contacts and include assotiations

```ruby
class Contact < ApplicationRecord
  belongs_to :kind, optional: true
  has_many :phones # here

  def author
    "Lucca Rodrigues"
  end

  def kind_description
    self.kind.description
  end

  def as_json(options={})
    super(methods: [:author, :kind_description],
    )
  end
end

```

- Go to file `lib => tasks => dev.rake` to create fake numbers

```ruby
namespace :dev do
  desc "Configure to development environment data mocks"
  task setup: :environment do

  ###################

    puts "Creating type contacts..."
    kinds = %w(Amigo Colega Comercial)
    kinds.each do |kind|
      Kind.create!(description: kind)
    end
    puts "type contacts created successfully!"

  ###################

    puts "Creating fake contacts..."
    # This generate 100 items
    10.times do |i|
      Contact.create!(
        name: Faker::Name.name,
        email: Faker::Internet.email,
        birthdate: Faker::Date.birthday(min_age: 18, max_age: 65),
        kind: Kind.all.sample
      )
    end
    puts "fake contacts created successfully!"

    ###################

    puts "Creating phone numbers..."
    5.times do |i|
      Contact.all.each do |contact|
        Random.rand(5).times do |i|
          phone = Phone.create!(number:Faker::PhoneNumber.cell_phone)
          contact.phones << phone
          contact.save!
      end
    end
    puts "Phone numbers created successfully!"
  end
end
```

- Run `rails db:drop db:create db:migrate dev:setup` to re-create data.
