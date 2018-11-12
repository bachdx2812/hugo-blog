---
title: "Rails Tip & Trick #1"
date: 2018-11-12
showDate: true
tags: ["tip&trick", "experience", "programing", "rails", "ruby"]
draft: false
---
# ActiveRecord Query Reduce

#### shipping_history.rb
```ruby
belongs_to :shipping
scope :shipped, -> { where(new_value: 'shipped') }
```

#### shipping.rb
```ruby
has_many :shipping_history

def shipped_time
  return nil unless shipped?
  puts "shipped_time"
  shipping_histories.shipped.last.created_at
end

def shopify_update_available?
  return false unless shipped_time
  Time.current - shipped_time >= 1.hour
end
```

```bash:rails c
Shipping.shipped.last.shopify_update_available?
```

generated SQL:
```sql
  Shipping Load (16.7ms)
	SELECT
		`shippings`. *
	FROM
		`shippings`
	WHERE
		`shippings`.`shipping_status` = 40
	ORDER BY
		`shippings`.`id` DESC LIMIT 1

  ShippingHistory Load (16.2ms)
	SELECT
		`shipping_histories`. *
	FROM
		`shipping_histories`
	WHERE
		`shipping_histories`.`shipping_id` = 5847
		AND `shipping_histories`.`new_value` = 'shipped'
	ORDER BY
		`shipping_histories`.`id` DESC LIMIT 1
  ShippingHistory Load (12.5ms)
	SELECT
		`shipping_histories`. *
	FROM
		`shipping_histories`
	WHERE
		`shipping_histories`.`shipping_id` = 5847
		AND `shipping_histories`.`new_value` = 'shipped'
	ORDER BY
		`shipping_histories`.`id` DESC LIMIT 1
```

After I changed `shipping.rb` to this
#### shipping.rb
```ruby
def shopify_update_available?
  shipping_shipped_time = shipped_time
  return false unless shipping_shipped_time
  Time.current - shipping_shipped_time >= 1.hour
end
```
Then the SQL become this

```sql
  Shipping Load (2.9ms)
	SELECT
		`shippings`. *
	FROM
		`shippings`
	WHERE
		`shippings`.`shipping_status` = 40
	ORDER BY
		`shippings`.`id` DESC LIMIT 1
shipped_time
  ShippingHistory Load (35.7ms)
	SELECT
		`shipping_histories`. *
	FROM
		`shipping_histories`
	WHERE
		`shipping_histories`.`shipping_id` = 5847
		AND `shipping_histories`.`new_value` = 'shipped'
	ORDER BY
		`shipping_histories`.`id` DESC LIMIT 1
```
Imagine when you have to deal with 100, 1000 records at a time, each one generate 1 extra 1 sql then you will have 100, 1000 more. Sound fair enough?
