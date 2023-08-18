- To handle specific files on response json user use `only`. Example:

```ruby
 # GET /contacts
  def index
    @contacts = Contact.all

    render json: @contacts, only: [:id, :name, :email, :birthdate]
  end
```

- To ignore fiels use `except`. Example:

```ruby
 # GET /contacts
  def index
    @contacts = Contact.all

    render json: @contacts, except: [:birthdate]
  end
```

- To insert fields when not contains on objet use `merge`. Example:

```ruby
    # GET /contacts
   def index
    @contacts = Contact.all

    render json: @contacts.map {|contact| contact.attributes.merge({ author: "Lucca Rodrigues"})}
  end
```

- To Insert on show to one object. Example:

```ruby
 # GET /contacts/1
  def show
    render json: @contact.attributes.merge({ author: "Lucca Rodrigues"})
  end
```
