- To relationship, you need insert required filed on controller and model to create a new contact. Example:

```ruby
class Contact < ApplicationRecord
  belongs_to :kind, optional: true

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

- To your controller include kind_id field. Example:

```ruby
 private
  # Use callbacks to share common setup or constraints between actions.
  def set_contact
    @contact = Contact.find(params[:id])
  end

  # Only allow a list of trusted parameters through.
  def contact_params
    params.require(:contact).permit(:name, :email, :birthdate, :kind_id)
  end
```
