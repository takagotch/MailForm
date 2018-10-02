### Mailform
---
https://github.com/plataformatec/mail_form

```ruby
class ContactForm < MailForm::Base
  attribute :name, :validate => true
  
  
  def headers
    {
      :subject => "",
      :to => "",
      :from => %("" <>)
    }
  end
end

```


