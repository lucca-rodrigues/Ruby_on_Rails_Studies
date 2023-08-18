- The methods are to be implement dynamically custom fields to all locales. Example:
- Go to app => models => contact.rb
- Add this code:

```ruby
  class Contact < ApplicationRecord
    def author
      "Lucca Rodrigues"
    end

    def as_json(options={})
      super(methods: :author)
    end
  end
```

- Now this is added to all locales where the module is available

```
[
	{
    "id": 1,
    "name": "João",
    "email": "joao@email.com",
    "birthdate": "1990-01-05",
    "created_at": "2023-08-17T23:40:40.216Z",
    "updated_at": "2023-08-18T00:43:30.705Z",
    "author": "Lucca Rodrigues"
	},
]
```
