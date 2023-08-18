- The methods are to be implement dynamically custom fields. Example:
- Go to app => models => contact.rb
- Add this code:

```ruby
  class Contact < ApplicationRecord
    def author
      "Lucca Rodrigues"
    end
  end
```

- On your controller add the created method. Example:

```ruby
  # GET /contacts
  def index
    @contacts = Contact.all

    render json: @contacts, methods: :author
  end
```
