### validates_timeliness
---

https://github.com/adzap/validates_timeliness

```ruby
gem 'validates_timeliness', '~> 5.0.0.alpha3'
bundle install
rails g validates_timeliness:install

validates_datetime :occurred_at
validates_date :date_of_birth, :before => lambda { 18.years.ago },
                               :before_message => "must be at least 18 years old"
validates_date :booked_at, :on => :create, :on_or_after => :today
validates_time :booked_at, :between => ['9:00am', '5:00pm']
validates_time :booked_at, :between => '9:00am'...'5:00pm'
validates_time :booked_at, :between => '9:00am'...'5:00pm'
validates_time :breakfast_time, :on_or_after => '6:00am',
                                :on_or_after_message => 'must be after opening time',
                                :before => :lunchtime,
                                :before_message => 'must be before lunch time'
class Person < ActiveRecord::Base
  validates_date :date_of_birth, :on_or_before => lambda { Date.current }
  validates :date_of_birth, :timeliness => {:on_or_before => lambda { Date.current }, :type => :date}
end
@person.validates_date :date_of_birth, :on_or_before => lambda { Date.current }
validates_date - validate value as date
validates_time - validate value as time only i.e. '12:20pm'
validates_datetime - validate value as a full date and time
validates          - use the :timeliness key and the type in the hash.

:is_at 
:before
:on_or_before
:after
:on_or_after
:between

:allow_nil
:allow_blank
:if
:unless
:on

:ignore_usec
:format

ValidatesTimeliness.setup do |config|
  config.extend_orms = [ :active_record ]
end

config.use_plugin_parser = true

validates_date :birth_date, :on_or_before => :today

config.restriction_shorthand_symbols.update(
  :yesterday => lambda { 1.day.ago }
)

config.default_timezone = :utc

config.dummy_date_for_time_type = [2009, 1, 1]

config.ignore_restriction_errors = true

config.enable_multiparameter_extension!

config.enable_date_time_select_extension!

:invalid_date_message
:invalid_time_message
:invalid_datetime_message
:is_at_message
:before_message
:on_or_before_message
:after_message
:on_or_after_message

```

```
en:
  errors:
    messages:
      invalid_date: "is not a vaild date"
      invalid_time: "is not a valid time"
      invalid_datetime: "is not a valid datetime"
      is_at: "must be at %{restriction}"
      before: "must be before %{restriction}"
      on_or_before: "must be on or before %{restriction}"
      after: "must be after %{restriction}"
      on_or_after: "must be on or after %{restriction}"
```
