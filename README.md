# PatternQueryHelper

Ruby Gem developed and used at Pattern to paginate, sort, filter, and include associations on sql and active record queries.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'pattern_query_helper'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install pattern_query_helper

## Use

To run an active record query execute
```ruby
PatternQueryHelper.run_sql_query(active_record_call, query_helpers, single_record)
```
active_record_call: Valid active record syntax (i.e. ```Object.where(state: 'Active')```)
query_helpers: See docs below
single_record: Default is false.  Pass in true to format payload as a single object instead of a list of objects

To run a custom sql query execute
```ruby
PatternQueryHelper.run_sql_query(model, query, query_params, query_helpers, single_record)
```
model: A valid ActiveRecord model
query: A string containing your custom SQL query
query_params: a symbolized hash of binds to be included in your SQL query
query_helpers: See docs below
single_record: Default is false.  Pass in true to format payload as a single object instead of a list of objects

## Query Helpers
query_helpers is a symbolized hash passed in with information about pagination, associations, filtering and sorting.

### Pagination
There are two pagination keys you can pass in as part of the query_helpers objects

```ruby
{
  page: 1,
  per_page: 20
}
```

If at least one of these keys is present, paginated results will be returned.

### Sorting
Sorting is controlled by the `sort` key in the query_helpers object

```ruby
{
    sort: "column_name:sort_direction"
}
```
Sort direction can be either asc or desc.  If you wish to lowercase string before sorting include the following:
```ruby
{
    sort: "name:desc:lowercase"
}
```

## Payload Formats

The PatternQueryHelper gem will return results in one of three formats

Paginated List Payload:
```json
{
  "pagination": {
    "count": 18,
    "current_page": 1,
    "next_page": 2,
    "previous_page": null,
    "total_pages": 6,
    "per_page": 3,
    "first_page": true,
    "last_page": false,
    "out_of_range": false
  },
  "data": [
    {
      "id": 1,
      "attribute_1": "string_attribute",
      "attribute_2": 12345,
      "attribute_3": 0.3423212
    },
    {
      "id": 2,
      "attribute_1": "string_attribute",
      "attribute_2": 12345,
      "attribute_3": 0.3423212
    },
    {
      "id": 3,
      "attribute_1": "string_attribute",
      "attribute_2": 12345,
      "attribute_3": 0.3423212
    },
  ]
}
```

List Payload:
```json
{
  "data": [
    {
      "id": 1,
      "attribute_1": "string_attribute",
      "attribute_2": 12345,
      "attribute_3": 0.3423212
    },
    {
      "id": 2,
      "attribute_1": "string_attribute",
      "attribute_2": 12345,
      "attribute_3": 0.3423212
    },
    {
      "id": 3,
      "attribute_1": "string_attribute",
      "attribute_2": 12345,
      "attribute_3": 0.3423212
    },
  ]
}
```

Single Record Payload:
```json
{
  "data": {
    "id": 1,
    "attribute_1": "string_attribute",
    "attribute_2": 12345,
    "attribute_3": 0.3423212
  }
}
```



## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/pattern_query_helper. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the PatternQueryHelper project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/pattern_query_helper/blob/master/CODE_OF_CONDUCT.md).
