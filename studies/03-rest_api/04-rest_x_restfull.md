- The objective is implement default behaviors and best practices in the API.
- Stateles = Unique request and have all important infomations and not dependts on the other requests.
- Cacheable = The API must be cacheable.
- Layers = Add layers to scale the API with load balancing and other.
- On demand = Load the infos and data on demand.

- Restfull = If has all best practices from rest.

## Status codes

- 100 = infomarmations
- 200 = Success
- 201 = Created
- 204 = No content

- 300 = Redirection

- 400 = Bad request
- 401 = Unauthorized
- 403 = Forbidden
- 404 = Not found

- 500 = Internal server error

Reference link: https://httpstatuses.io/

## On rails

- To use the status code on reais use the infos on website to specifc status code
- Example:

```ruby
# POST /contacts
  def create
    @contact = Contact.new(contact_params)

    if @contact.save
      render json: @contact, status: :created, location: @contact
    else
      render json: @contact.errors, status: :unprocessable_entity
    end
  end

  # PATCH/PUT /contacts/1
  def update
    if @contact.update(contact_params)
      render json: @contact
    else
      render json: @contact.errors, status: :unprocessable_entity
    end
  end
```
