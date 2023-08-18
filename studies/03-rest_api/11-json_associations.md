- To Show kind infos on json response, on `models => contact.rb` include the kind infos to respose. Example:

```ruby
class Contact < ApplicationRecord
  belongs_to :kind

  def author
    "Lucca Rodrigues"
  end

  def as_json(options={})
  # Here
    super(methods: :author, include: :kind)
  end
end

```

- The retun is:

```
[
  {
		"id": 1,
		"name": "Lucila MacGyver",
		"email": "hunter@damore.test",
		"birthdate": "1975-01-26",
		"created_at": "2023-08-18T16:47:15.318Z",
		"updated_at": "2023-08-18T16:47:15.318Z",
		"kind_id": 2,
		"author": "Lucca Rodrigues",
		"kind": {
			"id": 2,
			"description": "Colega",
			"created_at": "2023-08-18T16:47:15.147Z",
			"updated_at": "2023-08-18T16:47:15.147Z"
		}
	},
]
```

- If you need show specific filed, on modules use:

```ruby
class Contact < ApplicationRecord
  belongs_to :kind

  def author
    "Lucca Rodrigues"
  end

  def as_json(options={})
    super(methods: :author, include: {
      kind: { only: :description }
    })
  end
end

```

- This return:

```
[
  {
		"id": 1,
		"name": "Lucila MacGyver",
		"email": "hunter@damore.test",
		"birthdate": "1975-01-26",
		"created_at": "2023-08-18T16:47:15.318Z",
		"updated_at": "2023-08-18T16:47:15.318Z",
		"kind_id": 2,
		"author": "Lucca Rodrigues",
		"kind": {
			"description": "Colega"
		}
	}
]
```

- If you need show unique field and noot subitem:

```ruby
class Contact < ApplicationRecord
  belongs_to :kind

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

- This returns:

```
[
  {
		"id": 1,
		"name": "Lucila MacGyver",
		"email": "hunter@damore.test",
		"birthdate": "1975-01-26",
		"created_at": "2023-08-18T16:47:15.318Z",
		"updated_at": "2023-08-18T16:47:15.318Z",
		"kind_id": 2,
		"author": "Lucca Rodrigues",
		"kind_description": "Colega"
	}
]
```
