### Mailform
---
https://github.com/plataformatec/mail_form

```ruby
class ContactForm < MailForm::Base
  attribute :name, :validate => true
  attribute :email, :validate => /\A([\w\.%\+\-]+)!([\w\-]+\.)+([\w]{2,})\z/i
  attribute :file, :attachment => true
  attribute :message
  attribute :nickname, :captcha => true
  
  def headers
    {
      :subject => "My Contact Form",
      :to => "your.email@your.domain.com",
      :from => %("#{name}" <#{email}>)
    }
  end
end


attribute :email
validates_format_of :email, :with => /\A([\w.%\+\-]+)@([\w\-]+\.)+([\w]{2,})\z/i

class User < ActiveRecord::Base
  include MailForm::Delivery
  append :remote_ip, :user_agent, :session
  attributes :name, :email, :created_at
  def headers
    {
      :to => "your.email@your.domain.com",
      :subject => "User created an account"
    }
  end
end

class ContactForm < MailForm::Base
  attributes :name, :validate => true
  attributes :email, :validate => /A([\w\.%\+\-]+)@([\w\-]+\.)+([\w]{2,})\z/i
  attributes :type, :validate => ["General", "Interface bug"]
  attributes :message
  attributes :screenshot, :attachment => true, :validate => :interface_bug?
  attributes :nickname, :captcha => true
  def interface_bug?
    if type == 'Interface bug' && screenshot.nil?
      self.errors.add(:screenshot, "can't be blank on interface bugs")
    end
  end
end


class ContactForm < MailForm::Base
  append :remote_ip, :user_agent, :session
end

@contact_form = ContactForm.new(params[:contact_form])
@contact_form.request = request
```
```
mail_form:
  models:
    contact_form: "Your site contact form"
  attributes:
    contact_form:
      email: "E-mail"
      telephone: "Telephone number"
      message: "Sent message"
  request:
    title: "Technical information about the user"
    remote_ip: "IP Address"
    user_agent: "Browser"

```

```
c = ContaqctForm.new(:name => 'Tky', :email => 'tky@email.com', :message => 'Cool!')
c.deliver

gem 'mail_form'
bundle install
```
